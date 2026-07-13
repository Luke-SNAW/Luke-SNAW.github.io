---
id: si4tf7rsjlnd19p5l3lilkl
title: Dendron Vault 분리 및 비공개(Private) 설정 정리
desc: ""
updated: 1783929862768
created: 1783929849567
---

일기(daily journal)처럼 발행하고 싶지 않은 노트를 별도 vault로 분리하는 방법 정리.

## 1. 새 Vault 생성

명령 팔레트에서 `Dendron: Vault Add` 실행 → **local** 또는 **remote** 선택

### Local

- 워크스페이스 폴더 안에 새 폴더를 만들어 vault로 등록
- Git 저장소 연결 없음, 단순 파일 시스템 디렉토리
- `dendron.yml`:
  ```yaml
  vaults:
    - fsPath: private-journal
  ```

### Remote

- 기존/신규 git 저장소 URL을 입력받아 clone 후 vault로 등록
- 독립된 `.git`을 가진 완전히 별도의 저장소
- `dendron.yml`:
  ```yaml
  vaults:
    - fsPath: private-journal
      remote:
        type: git
        url: "git@github.com:username/private-journal.git"
  ```

## 2. `.gitignore` 자동 추가 (Local Vault 기본 동작)

- `Vault Add`로 local vault를 만들면 Dendron이 **기본적으로 해당 vault 경로를 `.gitignore`에 자동 추가**함 (의도된 동작)
- 이유: 나중에 별도 repo(remote vault)로 전환할 가능성을 열어두기 위함
- 하나의 repo에서 같이 관리하고 싶다면 `.gitignore`에서 해당 줄을 **수동으로 제거**한 뒤 커밋

```gitignore
# 이 줄을 지우면 private-journal도 상위 repo에 커밋됨
private-journal
```

## 3. Local → Remote 전환 (별도 repo로 분리)

1. vault 폴더 안에서 별도 git repo 초기화
   ```bash
   cd private-journal
   git init
   git add .
   git commit -m "initial commit"
   git remote add origin <REPO_URL>
   git push -u origin HEAD
   ```
2. `Dendron: Convert Vault` 명령으로 local → remote 전환 (기존 파일 유지, git만 연결)

### 주의: repo가 여러 개면 commit/push는 자동 통합되지 않음

- 상위 workspace repo와 remote vault repo는 **완전히 독립된 저장소**
- VS Code Source Control에서 각각 따로 commit/push 필요
- `Dendron: Workspace Sync` 명령은 여러 vault를 한 번에 **pull**하는 데는 도움되지만, commit/push 자동화는 아님

## 4. `visibility: private` — 발행(Publish) 제외

```yaml
vaults:
  - fsPath: vault
  - fsPath: private-journal
    visibility: private
```

- 이 설정은 **정적 사이트 생성(publish) 시에만** 영향
- `private-journal` vault 안의 모든 노트는 사이트 빌드 결과물에서 통째로 제외됨
- 개별 노트마다 `published: false`를 걸 필요 없음

### ⚠️ 핵심 주의사항: `visibility: private` ≠ Git 상에서 비공개

| 설정                  | 의미                                                          |
| --------------------- | ------------------------------------------------------------- |
| `visibility: private` | 정적 사이트에 **발행 안 됨** (HTML 페이지 생성 X)             |
| Git repo가 public     | 저장소를 클론/탐색하면 원본 markdown 파일은 그대로 **노출됨** |

- 하나의 repo로 합쳐서 관리할 경우, **그 repo 자체가 private repository인지 반드시 확인** 필요
- Public repo라면 사이트엔 안 보여도 소스 코드 자체는 그대로 공개됨

## 5. 결론: 상황별 권장 방식

| 목적                                     | 권장 방법                                                 |
| ---------------------------------------- | --------------------------------------------------------- |
| 사이트에만 안 보이면 됨 (소스 공개 무관) | `visibility: private` + 같은 (public) repo                |
| 완전한 비공개 (소스도 숨기고 싶음)       | 같은 repo면 **repo 자체를 private repo로 설정**           |
| 완전히 독립적으로 관리/백업하고 싶음     | Local → Remote 전환, **별도 private repo**로 분리         |
| 관리 단순화가 우선                       | 하나의 repo에서 `.gitignore` 해제 + `visibility: private` |
