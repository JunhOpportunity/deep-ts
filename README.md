# deep-ts
🎁 TypeScript의 중요 개념과 유용한 코드들을 정리해두고 필요할 때 사용해보기.

## 목차
### 중요한 개념
- 문법
> type & interface & Generic
- 타입 종류
> 함수

### 타입스크립트 in React
- 기본
> 함수 선언식 & 함수 표현식


# 추가 내용
## 타입스크립트의 특징
- 타입스크립트가 컴파일되면 최종적으로는 JS 코드만 남고 타입 관련 코드는 사라진다. 따라서, 타입스크립트는 프로그램 실행 자체에는 영향을 미치지 않는다는 것을 알 수 있다.

## 기본 세팅

- 패키지 초기화 : `$ npm init`
- types node 설치 : `$ npm i @types/node`
- 컴파일러 옵션 파일 생성 : tsconfig.json

## 타입스크립트 컴파일러 옵션 설정

TS는 서로 다른 파일을 생성해서 코드를 작성하더라도 결국엔 하나의 파일로 본다.

이렇게 되면 서로 다른 파일에 같은 이름의 변수를 선언한 경우 에러가 발생한다.

따라서, 이를 해결하기 위해서 tsconfig.json 에 moduleDetection 키워드를 추가해야한다.

또는, 한 번이라도 export 하면 된다.

<img width="327" alt="image" src="https://github.com/user-attachments/assets/e4d05163-700e-4bea-8b66-78b7c1e00c77" />

## 원시 타입

임시적으로 null 값을 넣으려고 할 때도 에러가 발생하는데,
이런 경우에는 `strictNullChecks` 키워드를 추가해주면 된다.

### Number Type

`let num: number = 123;`

- 양수, 음수, 실수, 무한대, NaN 등등
- 문자열에 사용하는 toUpperCase() 같은 메소드는 사용 불가능
- 숫자에 사용하는 toFixed() 메소드 사용 가능

### String Type

`let str: string = "hello";`

### Boolean Type

`let bool: boolean = true;`

### null Type

`let null1: null = null;`

### undefined Type

`let unde: undefined = undefined;`

### 리터럴 타입

> 특정 값을 타입인 것 처럼 만들어서 사용할 수 있다.
> 

`let numA: 10 = 10;`

`let strA: “hello” = “hello”;`

`let boolA: true = true;`

## 배열과 튜플

### 일반 배열

> 하나의 타입만을 가진 배열의 경우
> 

```jsx
// 배열
let numArr: number[] = [1, 2, 3];

let strArr: string[] = ["a", "b", "c"];

// 제네릭
let boolArr: Array<boolean> = [true, false, true];
```

### 유니온 타입

> 배열에 들어가는 요소들의 타입이 다양할 경우
> 

```jsx
// 유니온 타입
let multiArr: (number | string)[] = [1, "a", 2, "b"];
```

### 다차원 배열

> 배열 안에 배열이 들어가는 2,3 차원 배열
> 

```jsx
// 다차원 배열
let multiArr2: number[][] = [[1], [2, 3]];
```

### 튜플

> 길이와 타입이 고정된 배열
> 

<aside>
💡

언제 사용할까?

순서가 정해진 배열을 만들 때 주로 사용한다.

</aside>

```jsx
// 튜플
let tuple: [number, string] = [1, "a"];

let users: [string, number][] = [
  ["김준호", 1],
  ["이준호", 2],
  [3, "박준호"], // 에러 발생
];
```
