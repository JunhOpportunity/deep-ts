# deep-ts
타입 스크립트의 기본 개념 정리 및 공부 내용 정리

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

undefined 도 담을 수 없다. (void와 다른 점)

</aside>

```jsx
function func3(): never {
  while(true) {}
}

function func4(): never {
  throw new Error();
}
```
# Section4 - 타입스크립트 이해하기

## 업 캐스팅과 다운 캐스팅

### 업 캐스팅

> 수퍼 타입과 서브 타입 중에서 서브 타입 → 수퍼 타입으로 타입 변환 되는 것
> 

### 다운 캐스팅

> 서브 타입 → 수퍼 타입으로 타입 변환 되는 것
> 

## 대수 타입

> 여러개의 타입을 합성해서 새롭게 만들어낸 타입
합집합 타입과 교집합 타입이 존재한다.
> 

### 합집합 타입 (Union)

```jsx
// 일반 변수
let a: string | number | boolean;
a = 1;
a = "hello"
a = true;

// 배열
let arr: (string | number | boolean) [] = [1, "hello", true];

// 타입 별칭의 합집합
type Dog = {
	name : string;
	color : string;
}

type Person = {
	name : string;
	language : string;
}

type union = Dog & Person;

// 가능
let union1 : Union = {
	name: "a",
	color: "red"
}

let union1 : Union = {
	name: "b",
	language: "blue"
}
let union1 : Union = {
	name: "c"
	color: "green"
	language: "kr"
}

// 불가능!!!
let union1 : Union = {
	name: "d"
}
```

### 교집합 타입

```jsx
type Dog = {
	name : string;
	color : string;
}

type Person = {
	name : string;
	language : string;
}

type Intersection = Dog & Person;

let intersection : Intersection = {
	name: "name"
}
```
## 타입 추론

> 타입을 적지 않아도 타입스크립트가 알아서 타입을 추론하는 것
> 

초기화 할 때 첫 타입을 기준으로 타입을 추론한다.

초기화 할 때 아무 것도 넣지 않으면 any로 적용되고,

### 암묵적 any 타입의 진화

만약 변수에 값을 넣지 않아서 타입 추론이 불가능 할 경우 any 타입이 된다.

이후에 값을 넣으면 계속해서 타입이 변하는데, 이를 암묵적 any 타입 진화라고 한다.

명시적으로 any를 지정해주는 것과는 다르다. (이 경우에는 항상 any 타입이다)

```jsx
let a; // any 타입

a = 10; // number 타입

a = "hello" // string 타입
```

### const로 선언한 경우

const로 변수를 선언해서 타입 추론을 할 경우 해당 값이 바뀔 일이 없기 때문에 리터럴 타입 즉, 자기 자신과 같은 타입으로 타입이 추론된다.

```jsx
const a = 10; // const a : 10
```

## ⭐타입 단언

### const 단언

객체 데이터를 한 번에 readonly로 만드는 효과가 있다.

```jsx
let cat = {
	name: "야옹이",
	color: "black"
} as const;
```

## 타입 좁히기

> 조건문 등을 이용해 넓은 타입에서 좁은 타입으로 상황에 따라 타입을 좁히는 것
> 

```jsx
function func(value: number | string) {
	if(typeof value === "number") {
		console.log(value.toFixed());
	} else if (typeof value == "string") {
		console.log(value.toUpperCase());
	}
}
```

## 서로소 유니온 타입

> 교집합이 없는 타입들로만 만든 유니온 타입

## Section 5 - 함수와 타입

### 함수 타입

```tsx
// 화살표 함수 타입 정의 (반환타입은 알아서 추론한다)
const add = (a: number, b: number) => a + b; 

// 튜플 타입 매개변수
function getSum(...rest: number[]) {
	//...
}

getSum(1, 2, 3);
getSum(1, 2, 3, 4, 5);
```

### 함수 타입 표현식

> 비슷한 기능을 하는 함수를 만들 때 함수 타입 표현식을 선언해두면 타입을 계속 정의하지 않고 재사용 할 수 있다.
> 

```tsx
// 함수 타입 표현식
type Add = (a: number, b: number) => number;

// 사용
const add: Add = (a, b) = > a + b;
```

### 호출 시그니처

```tsx
// 호출 시그니처
type Add = {
	(a: number, b: number) => number;
};

// 사용
const add: Add = (a, b) = > a + b;
```

### 함수 오버로드

> 하나의 함수를 매개변수의 개수나 타입에 따라 여러 가지 버전으로 만드는 문법
> 

```tsx
// 오버로드 시그니처
function add(a: number, b: number): void;
function add(a: number, b: number, c: string): void;

// 구현
function add(a: number, b: number, c?: string): void {
  console.log(a + b);
  if (c) {
    console.log(c);
  }
}
```

### 사용자 정의 타입가드

> 해당 타입이 맞는지 확인하는 함수
> 

```tsx
  function isDog(animal: Animal): animal is Dog {
	  return (animal as Dog).isBark !== undefined;
	}
	
	function wanring(animal: Animal) {
		if(isDog(animal)) {
			// 강아지
		} else {
			// 고양이
		}
	}
```

# Section6 - 인터페이스

- 타입 별칭과는 다르게 여러 타입을 합치거나 유니온으로 만들 수 없다.

```tsx
interface Person{
  readonly name: string;
  age?: number;
  sayHi(): void; // 호출 시그니처 방
}

const person: Person = {
  name: "person",
  sayHi: function() {
    console.log("안녕하세요");
  }
}
```

### 인터페이스 확장(=상속)

- 원본 프로퍼티 타입의 서브 타입으로만 새로 재정의 할 수 있다. 아예 다른걸로는 못함.

```tsx
interface Animal{
	name: string;
	color: string;
}

interface Dog extends Animal {
	isBark: boolean;
}

interface Cat extends Animal {
	name: "ED"; 
}
```

### 인터페이스 다중확장

```tsx
interface DogCat extends Dog, Cat {}
```

### 인터페이스 합치기

> 동일한 인터페이스 이름으로 만든 타입은 서로 합쳐진다.
> 

```tsx
interface Person {
	name: string;
}

interface Person {
	age: string;
}

// 결과
interface Person {
	name: string;
	age: string;
}
```


