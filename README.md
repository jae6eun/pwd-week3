# pwd-week3 Calculator

HTML, CSS, TypeScript를 사용해 구현한 기본 계산기입니다.

이번 실습에서는 계산기 화면 구성, 입력 처리, 계산 로직, 화면 갱신을 서로 다른 역할로 나누어 구현했습니다.

## 실행 방법

1. 필요한 패키지를 설치합니다.

```bash
npm install
```

2. TypeScript 파일을 JavaScript로 컴파일합니다.

```bash
npm run build
```

3. 프로젝트 폴더의 `index.html` 파일을 브라우저에서 엽니다.

TypeScript 코드를 수정한 경우에는 다시

```bash
npm run build
```

를 실행한 뒤 브라우저를 새로고침합니다.

---

## 파일 구성

- `index.html` : 계산기 화면의 구조와 버튼 구성
- `styles.css` : 계산기 배치와 색상, 버튼 스타일
- `operations.ts` : 사칙연산 계산
- `calculator.ts` : 숫자 입력, 연산자 선택, 계산 상태 관리
- `app.ts` : 버튼 클릭 이벤트 처리와 화면 갱신
- `js/` : TypeScript를 컴파일하여 생성된 JavaScript 파일

---

## 동작 확인

### 기본 사칙연산

- `12 + 3 =` → `15`
- `12 - 3 =` → `9`
- `12 × 3 =` → `36`
- `12 ÷ 3 =` → `4`
- `0.1 + 0.2 =` → `0.3`

사칙연산은 `operations.ts`의  
`add()`, `subtract()`, `multiply()`, `divide()` 함수가 담당합니다.

실제 계산은 `calculate()` 함수에서 선택된 연산 함수를 전달받아 실행합니다.

### 숫자 입력과 계산 상태

`calculator.ts`의 `state` 객체에서 현재 입력값, 저장된 숫자, 연산자 등의 상태를 관리합니다.

- 숫자 입력: `inputDigit()`
- 연산자 선택: `selectOperator()`
- `=` 계산: `equals()`
- 전체 입력 처리: `handleKey()`
- AC 초기화: `clear()`

### 기타 기능

- `123 → ⌫` → `12`
  - `calculator.ts`의 `handleKey()`에서 삭제 처리

- `5 → +/−` → `-5`
  - `calculator.ts`의 `handleKey()`에서 부호 전환

- `50 → %` → `0.5`
  - `calculator.ts`의 `handleKey()`에서 현재 숫자를 100으로 나누어 처리

- `6110000` → `6,110,000`
  - `app.ts`의 `formatDisplay()`에서 화면 표시용 쉼표 추가

### 계산식 표시

`12 → + → 3 → =`을 입력하면

- 계산식: `12 + 3 =`
- 결과: `15`

가 표시됩니다.

계산 진행 중인 식은 `calculator.ts`의 `pendingExpression()`에서 만들고,  
`app.ts`의 `render()` 함수가 실제 화면에 표시합니다.

### 오류 처리

`12 ÷ 0 =`을 입력하면

- 결과 화면: `Error`
- 메시지: `0으로 나눌 수 없습니다.`

가 표시됩니다.

`operations.ts`의 `divide()`에서 0으로 나누는 경우 오류를 발생시키고,  
`calculator.ts`의 `handleKey()`에서 오류를 저장한 뒤  
`app.ts`의 `render()`에서 화면에 표시합니다.

이후 숫자를 새로 입력하면 오류 상태가 초기화되고 새로운 계산을 시작할 수 있습니다.

---

## 실습을 통해 확인한 내용

- TypeScript는 브라우저에서 직접 실행되지 않고 JavaScript로 컴파일한 뒤 실행됩니다.
- 계산 기능, 계산 상태, 화면 표시를 서로 다른 파일로 분리할 수 있습니다.
- 버튼 클릭 → 입력 처리 → 상태 변경 → 계산 → 화면 갱신 순서로 계산기가 동작합니다.