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
