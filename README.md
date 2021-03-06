# TypeScript_Programming_Book

타입스크립트 프로그래밍 책 학습

## 타입스크립트 장점

- 타입 안전성(type safety) 제공
- 문서화
- 리팩터링 단순화
- 단위 테스트 단순화
- 생산성 증가

## 컴파일 및 실행

TS

1. 타입스크립트 소스 -> 타입스크립트 AST
2. 타입 검사기가 AST를 확인
3. 타입스크립트 AST(Abstract Syntax Tree) -> 자바스크립트 소스

JS 4. 자바스크립트 소스 -> 자바스크립트 AST 5. AST -> 바이트 코드 6. 런타임이 바이트코드를 평가

## 타입 시스템

- 타입 검사기가 프로그램에 타입을 할당하는 데 사용하는 규칙 집합

보통 두 가지 종류

1. 컴파일러에게 명시적으로 타입을 알려줌
2. 컴파일러가 자동으로 타입을 추론

**타입스크립트는 두 가지 모두의 영향을 받았다.**

```typescript
// 타입 명시
let a: number = 1; //a는 number
let b: string = "hi"; // b는 string
let c: boolean[] = [true, false]; // c는 boolean 배열

// 자동 추론
let a = 1; //a는 number
let b = "hi"; // b는 string
let c = [true, false]; // c는 boolean 배열
```

| 타입 시스템 기능            |  자바스크립트  |    타입스크립트     |
| --------------------------- | :------------: | :-----------------: |
| 타입 결정 방식              |      동적      |        정적         |
| 타입이 자동으로 변환되는가? |       O        |      X(대부분)      |
| 언제 타입을 확인하는가?     |     런타임     |     컴파일 타임     |
| 언제 에러를 검출하는가?     | 런타임(대부분) | 컴파일 타임(대부분) |

## 코드 편집기 설정 13p.

```
// 설정
npm init
npm install -D typescript tslint @types/node
./node_modules/.bin/tsc --init
./node_modules/.bin/tslint --init
```

```
// 컴파일 및 실행
./node_modules/.bin/tsc
node ./dist/index.js
```

- ts-node를 설치하면 컴파일 및 실행을 간편하게 할 수 있다.

## 타입(type)

값과 이 값으로 할 수 있는 일의 집합

- Boolean 타입은 참 / 거짓과 수행할 수 있는 모든 연산의(||, &&, ! 등) 집합이다.
- number 타입은 모든 숫자와 적용할 수 있는 모든 연산(+, -, ||, &&, ? 등), 모든 메서드(.toFixed, .toPrecision, .toString 등)의 집합이다.
- string 타입은 모든 문자여롸 수행할 수 있는 모든 연산(+, ||, && emd), 모든 메서드(.concat, .toUpperCase 등)의 집합이다.

어떤 값이 T 타입이라면 이 값을 가지고 어떤 일을 할 수 있고 없는지 알 수 있다.
즉, 어떤 타입을 어떻게 사용하는지를 통해 타입 확인자는 특정 동작이 유효한지 아닌지 판단할 수 있다.

**타입 리터럴(type literal)**

- 오직 하나의 값을 나타내는 타입

평범한 boolean 타입이 아니며 해당 타입이 가질 수 있는 특정한 하나의 값으로 타입을 한정한다.

```typescript
let e: true = true; // true
let f: false = false; // false
```

**타입 지정 방법**

- 타입스크립트가 타입을 추론
- const를 이용해 타입 리터럴을 추론
- 타입을 명시
- 타입 리터럴 명시

```typescript
let num = 123; // number
const PI = 3.14; // 3.14
let num: number = 12345; // number;
const PI: 3.14 = 3.14; // 3.14
```

**객체**

- 인덱스 시그니처(index signature)
  - [key: T]: U 같은 문법을 인덱스 시그니처라 한다.
  - 어떤 객체가 여러 키를 가질 수 있음을 나타낸다. 키 (T)는 반드시 number나 string타입이어야 한다.
  - readonly 한정자를 사용해 특정 필드를 읽기 전용으로 정의할 수 있다.
  - 키 이름은 원하는 이름을 써도 된다.
  ```typescript
  let theater: {
    [seatNumber: string]: string;
  } = {
    "11D": "최승현",
    "12D": "홍길동",
  };
  ```

## 타입 별칭

- 하나의 타입을 두 번 정의할 수는 없다.

```typescript
type Name = "Choi";
type Name = "Lee"; // 에러 TS2300: 'Name' 식별자를 중복 정의함
```

- 블록 영역에 적용된다.

```typescript
type Name = "Choi";

let x = Math.random() < 0.5;

if (x) {
  type Name = "Lee"; // 위의 Name 정의를 덮어씀
  let b: Name = "Lee";
} else {
  let c: Name = "Choi";
}
```

## 유니온과 인터섹션 타입

```typescript
type Cat = { name: string; purrs: boolean };
type Dog = { name: string; barks: boolean; wags: boolean };
type CatOrDogOrBoth = Cat | Dog;
type CatAndDog = Cat & Dog;

// Cat
let a: CatOrDogOrBoth = {
  name: "hamburger",
  purrs: true,
};

// Dog
a = {
  name: "Pizza",
  barks: true,
  wags: true,
};

// Both
a = {
  name: "hamburger",
  purrs: true,
  barks: true,
  wags: true,
};

let b: CatAndDog = {
  name: "Domino",
  purrs: true,
  barks: true,
  wags: true,
};
```
