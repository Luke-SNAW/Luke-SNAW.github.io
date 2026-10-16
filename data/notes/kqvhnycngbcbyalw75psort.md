
> https://morizbuesing.com/blog/greppability-code-metric/
>
> the concept of "greppability" as a crucial yet often overlooked code metric that enhances the maintainability of codebases. It emphasizes the importance of making code easily searchable, especially when working with unfamiliar code.

---

## [GN](https://news.hada.io/topic?id=16597)

- 낯선 코드베이스를 유지보수할 때 문자열을 검색하는 데 많은 시간을 소비함
- 혼자서 작성한 프로젝트에서도 함수 이름, 오류 메시지, 클래스 이름 등 많은 것을 검색해야 함
- 검색이 잘 되지 않으면 코드베이스에서 참조를 찾지 못해 불필요한 것으로 간주할 위험이 있음
- 이런 상황에서 코드 베이스의 Greppability(그렙 가능성)을 유지하기 위해 적용할 수 있는 몇 가지 규칙을 도출했음

### 식별자를 분할하지 말 것

- 식별자를 분할하거나 동적으로 구성하는 것은 좋지 않은 생각
- `shipping_addresses`와 `billing_addresses`라는 두 개의 데이터베이스 테이블이 있다고 가정할 때, 주문 유형에 따라 동적으로 테이블 이름을 구성하는 것은 좋아 보일 수 있음

```typescript
const getTableName = (addressType: "shipping" | "billing") => {
  return `${addressType}_addresses`
}
```

- 이는 DRY해 보이지만 유지 관리에 좋지 않음. 누군가는 `shipping_addresses` 테이블 이름을 코드 베이스에서 검색할 때 이 부분을 놓칠 수 있음
- 식별자를 하드코딩하는 것이 더 나은 방법
- 검색 가능성을 위해 리팩토링한 코드:

```typescript
const getTableName = (addressType: "shipping" | "billing") => {
  if (addressType === "shipping") {
    return "shipping_addresses"
  }
  if (addressType === "billing") {
    return "billing_addresses"
  }
  throw new TypeError("addressType must be billing or shipping")
}
```

- 열 이름, 객체 필드, 메서드/함수 이름(JavaScript에서는 메서드 이름을 동적으로 구성하는 것이 쉽게 가능함)에도 동일하게 적용

### 스택 전체에서 동일한 이름 사용하기

- 이름 지정 체계에 맞추기 위해 애플리케이션 경계에서 필드 이름을 변경하지 말 것
- 대표적인 예로, PostgreSQL 스타일의 snake_case 식별자를 JavaScript로 가져와 camelCase로 변환하는 것은 좋지 않음
- 이는 검색을 어렵게 만듦. 모든 항목을 찾으려면 하나 대신 두 개의 문자열을 검색해야 함

```typescript
const getAddress = async (id: string) => {
  const address = await getAddressById(id)
  return {
    streetName: address.street_name,
    zipCode: address.zip_code,
  }
}
```

- 차라리 객체를 직접 반환하는 것이 더 나음

```typescript
const getAddress = async (id: string) => {
  return await getAddressById(id)
}
```

### 중첩보다는 평평한 것이 좋음

- Python의 Zen에서 영감을 얻어, 네임스페이스를 다룰 때는 폴더/객체 구조를 중첩하는 것보다 평평하게 만드는 것이 대부분 더 나음
- 번역 파일 설정의 두 가지 선택 사항이 있는 경우:

```json
{
  "auth": {
    "login": {
      "title": "Login",
      "emailLabel": "Email",
      "passwordLabel": "Password"
    },
    "register": {
      "title": "Register",
      "emailLabel": "Email",
      "passwordLabel": "Password"
    }
  }
}
```

```json
{
  "auth.login.title": "Login",
  "auth.login.emailLabel": "Email",
  "auth.login.passwordLabel": "Password",
  "auth.register.title": "Login",
  "auth.register.emailLabel": "Email",
  "auth.register.passwordLabel": "Password"
}
```

- 두 번째 옵션을 선택하는 것이 좋음. 키를 쉽게 찾을 수 있으며, `t('auth.login.title')`와 같이 참조할 수 있음
- React 컴포넌트 구조를 고려할 때:

```bash
./components/AttributeFilterCombobox.tsx
./components/AttributeFilterDialog.tsx
./components/AttributeFilterRating.tsx
./components/AttributeFilterSelect.tsx
```

- 다음과 같은 구조보다 선호됨

```bash
./components/attribute/filter/Combobox.tsx
./components/attribute/filter/Dialog.tsx
./components/attribute/filter/Rating.tsx
./components/attribute/filter/Select.tsx
```

- 검색 관점에서 보면, `Dialog`와 같은 일반적인 이름 대신 `AttributeFilterCombobox`와 같이 네임스페이스가 포함된 전체 컴포넌트를 검색할 수 있기 때문

--

## [HN](https://news.ycombinator.com/item?id=41430772)

- 함수 이름과 클래스 이름 같은 기호를 검색하는 것은 코드의 구문을 이해하는 도구를 사용하는 것에 비해 약함
  - "정의로 이동"과 "사용처 찾기" 기능만으로도 텍스트 검색의 필요성을 크게 줄일 수 있음
  - 지난 10년 동안 주로 사용자에게 보이는 문자열만 검색해왔음
  - 이런 게시물은 저자가 자신의 언어에 맞는 더 나은 도구를 배우는 데 시간을 투자해야 한다는 것을 의미함
  - 좋은 IDE만으로도 많은 시간을 절약할 수 있음
- 'greppable'은 자체적으로 사용되지 않는 단어/개념임
  - 오랫동안 이를 조직 원칙으로 사용해왔음
  - 코드 구조화의 가장 좋은 방법 중 하나임
- 조건부 문자열 보간을 사용한 복잡한 예제를 본 적이 있음
  - 프로젝트에 처음 참여했을 때 UI에서 본 세 단어를 찾는 데 너무 오래 걸렸음
  - 나중에 이 코드를 쉽게 grep할 수 있는 문자열로 모두 바꿈
- 많은 코딩 스타일과 도구는 문자열 상수를 줄 길이와 상관없이 한 줄로 유지함
  - 프로그램 출력에서 문자열을 보고 코드에서 동일한 문자열을 검색할 수 있도록 하기 위함
- Rust, Javascript, Lisp는 함수 정의 앞에 키워드를 두어 검색이 용이함
  - C는 이러한 키워드가 없어 함수 이름만 검색할 수 있음
  - 일부 C 코딩 규칙은 정의를 두 줄로 나누어 검색을 용이하게 함
- greppability에 동의하지만, 경계를 넘어 이름을 동일하게 유지하는 것에는 반대함
  - 하나의 기호가 하나의 도메인에만 존재하는 것이 인지 부하를 줄임
- 코드 검색 가능성은 좋지만, 예제는 의도적으로 오류 가능성을 높임
  - 문자열 조건을 추가하면 입력과 출력 간의 불일치 가능성이 생김
  - 딕셔너리를 평탄화하면 오타가 발생할 가능성이 높아짐
  - 오타는 흔히 발생하며, 여러 코드베이스에 복사된 경우 해결이 어려움
