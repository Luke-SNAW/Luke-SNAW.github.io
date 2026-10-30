
> 작성일: 2026-04-01 | from claude-sonnet-4-6

## 개요

Astro 빌드 시 발생하는 `MissingSharp` 에러의 원인과 해결 방법, 그리고 `sharp` 설치 여부와 캐시 bust의 관계를 정리한다.

## 내용

### MissingSharp 에러

Astro는 `src/assets/`에 위치한 이미지를 빌드 시 최적화할 때 `sharp` 패키지를 사용한다. `sharp`가 설치되지 않은 환경(예: CI/CD)에서 빌드하면 아래 에러가 발생한다.

```
MissingSharp: Could not find Sharp. Please install Sharp (`sharp`) manually
into your project or migrate to another image service.
```

### 해결 방법 비교

| 방법               | 이미지 최적화 | 캐시 bust | 의존성 추가 |
| ------------------ | :-----------: | :-------: | :---------: |
| `sharp` 설치       |       O       |     O     |      O      |
| `noop` 서비스 설정 |       X       |     O     |      X      |
| `public/`으로 이동 |       X       |     X     |      X      |

**방법 1 — `sharp` 설치**

```bash
pnpm add sharp
```

`<Image>` 컴포넌트나 마크다운 이미지 참조 시 WebP 변환, 리사이즈 등 최적화를 수행한다. 빌드마다 최적화가 실행되지만, 변경된 이미지만 재처리되므로 실제 비용은 크지 않다.

**방법 2 — noop 이미지 서비스 설정**

```js
// astro.config.mjs
export default defineConfig({
  image: { service: { entrypoint: "astro/assets/services/noop" } },
  // ...
})
```

이미지 최적화를 건너뛰지만, 파일명 해시(캐시 bust)는 Vite가 담당하므로 그대로 동작한다. `<Image>` 컴포넌트를 사용하지 않는 프로젝트에 적합하다.

### 캐시 bust와 sharp의 관계

- **캐시 bust(해시 파일명)** — Vite의 자산 파이프라인이 처리하며, `sharp`와 무관하게 동작
- **이미지 최적화(WebP 변환, 리사이즈)** — `sharp`가 필요

`src/assets/`에 이미지를 두면 `sharp` 없이도 캐시 bust가 적용된다. `public/`으로 이동하면 파일명이 고정되어 캐시 bust가 되지 않는다.

### 선택 기준

- 이미지 최적화(포맷 변환, 리사이즈)가 필요하면 → `sharp` 설치
- 캐시 bust만 필요하고 최적화는 불필요하면 → `noop` 서비스 설정

### GitHub Actions CI에서의 이미지 최적화 캐시

Astro는 빌드 시 최적화된 이미지를 `.astro/image-cache/`에 저장한다. 로컬에서는 빌드 간 재사용되지만, CI 환경은 매 실행마다 초기화되므로 **별도 캐시 설정이 없으면 이미지를 매번 전부 재최적화**한다.

`actions/setup-node`의 `cache: "pnpm"`은 pnpm store만 캐싱하며 `.astro/`는 포함되지 않는다.

**`.astro/` 디렉토리 캐싱 설정 예시**

```yaml
- uses: actions/cache@668228422ae6a00e4ad889ee87cd7109ec5666a7 # v5.0.4
  with:
    path: .astro
    key: astro-image-cache-${{ hashFiles('src/assets/**') }}
    restore-keys: |
      astro-image-cache-
```

`hashFiles`만 사용하면 이미지 하나가 추가될 때마다 캐시 키가 바뀌어 전체 재처리가 발생한다. `restore-keys`에 prefix를 지정하면 완전 일치 캐시가 없을 때 가장 최근의 부분 일치 캐시를 복원하여, 기존 이미지는 재사용하고 새로 추가된 이미지만 처리한다.

> `noop` 이미지 서비스를 사용하는 경우 이미지 최적화가 비활성화되므로 위 캐시 설정은 불필요하다.

## 참고

- [Astro Image Service API](https://docs.astro.build/en/reference/image-service-reference/)
- [Astro Assets Guide](https://docs.astro.build/en/guides/images/)
- [Dependency caching reference - GitHub Docs](https://docs.github.com/en/actions/reference/workflows-and-actions/dependency-caching)
