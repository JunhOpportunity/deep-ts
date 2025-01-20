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
## 객체

```jsx
// object
let user: {
  id: number;
  name: string;
} = {
  id: 1,
  name: "Kim",
}
```

### 옵셔널 프로퍼티

<aside>
💡

없을 수도 있는 데이터인 경우에 사용. 물음표를 붙인다.

</aside>

<aside>
💡

값을 바꾸지 못하게 하고 싶다면 앞에 readonly 를 붙인다

</aside>

```jsx
let user: {
  id?: number;
  readonly name: string;
} = {
  id: 1,
  name: "Kim",
}
```

## 타입 별칭

> 자주 사용되는 타입을 변수로 저장해서 사용하는 것
> 

```jsx
// 타입 별칭 = 타입 변수
type User = {
  id: number;
  name: string;
  location: string;
}

let user: User = {
  id: 1,
  name: "Kim",
  location: "Korea",
}
```

## 인덱스 시그니처

> 너무 많은 타입 이름을 선언해야 하는 경우 형식만 정의해주는 것
> 

<aside>
💡

만약, 특정 타입은 무조건 들어가야 한다면 평소처럼 그대로 타입을 선언해주면 된다.

여기서 주의할 점은, 특정 타입과 인덱스 시그니처의 타입이 일치해야 한다.

</aside>

```jsx
// 인덱스 시그니처
type CountryNumberCodes = {
  [key: string]: number;
  Korea: number; // Korea는 무조건 있어야 한다. 위 number과 동일타입.
}

let countryNumberCodes : CountryNumberCodes = {
  Korea: 82,
  USA: 1,
  China: 86,
}
```

## Enum

> 여러가지 값들에 각각 이름을 부여해 열거해두고 사용하는 타입
> 

<aside>
💡

enum 타입은 컴파일을 해도 사라지지 않는다. 즉, 값으로 그대로 남는다

</aside>

```jsx
// 기존 사용
const user1 = {
    name: 'Taro',
    role : 0
}
const user2 = {
    name: 'Hanako',
    role : 1
}

// 숫자형 enum 선언 후 사용
enum Role {
    ADMIN = 0,
    USER = 1
}
const user3 = {
    name: 'Jiro',
    role : Role.ADMIN
}
const user4 = {
    name: 'Saburo',
    role : Role.USER
}

// 문자열형 enum
enum Language {
	korean = "ko",
	english = "en",
}
```
## Any와 Unknown

### any

> 특정 변수의 타입을 우리가 확실히 모를 때
> 

<aside>
💡

any 타입은 타입스크리트의 이점을 전혀 사용하지 않겠다는 것과 마찬가지이기 때문에 되도록 사용하지 않는 것이 좋다.

(나중에 런타임시 오류가 발생해서 굉장히 좋지 않음)

</aside>

```jsx
// any

let anyVar: any = 10;

anyVar = true;
anyVar = {}
```

### unknown

> any 타입과 비슷하지만 타입 정제를 거치지 않으면 사용할 수 없는 값이 되어버리기 때문에 런타임 에러를 일으키는 any 타입 보다는 안전하다.
> 

```jsx
let unknownVar: unknown;

unknownVar = "";
unknownVar = 1;
unknownVar = () => {}

// 타입 정제 (이 과정을 거쳐야만 값을 활용할 수 있다.)
if (typeof unknownVar === "number") {
	num = unknownVr;
}
```

## void와 never

### void

> 아무것도 없음을 의미하는 타입. undefined 외에 다른 값은 절대 담을 수 없다.
> 

```jsx
function func2(): void {
  console.log('func2');
}
```

### never

> 반환값 자체가 존재하는 것이 불가능 할 경우 never 사용
> 

<aside>
💡

undefined 도 담을 수 없다.

</aside>

```jsx
function func3(): never {
  while(true) {}
}

function func4(): never {
  throw new Error();
}
```
