## 리액트 프로젝트에서 타입 스크립트 사용하기 #1 #TIL



> 이 글은 [리액트 프로젝트에서 타입 스크립트 사용하기 - velopert]( https://velog.io/@velopert/using-react-with-typescript ) 의 글을 보고 공부 목적으로 작성하였습니다. 감사합니다.





### 1. 왜 타입스크립트인가?

Javascript는 Weakly-typed된 언어이기 때문에 한가지 변수에 모든 타입의 값들을 넣을 수 있습니다.

**example**

```javascript
let value = 5;
value = [1,2,3,4,5];
value = null;
vaule = 'dds';
```



이러한 것의 문제점은 **그 값에 어떠한것들이 들어가도 상관없기 때문에 에러 체크하기**가 어렵다는 것입니다.



#### JavaScript의 불편함

- 자동완성 기능이 떨어진다.
- 함수 파라미터 타입 체킹을 안해준다.
- 리덕스 쓸 때 불편하다.
- 리액트 컴포넌트를 쓸 때 어떤 props를 넣어야 하는지 에디터에서 알 방법이 없다.



#### 그래서 써야하는 이유는?

1. IDE를 적극 활용할 수 있다. (타입 체킹, 자동완성)
2. 실수를 줄일 수 있다.
3. 협업시 유용하다.



## 2. 타입스크립 기초



### 타입스크립트 기본 설정.

- 새로운 타입 스크립트 프로젝트를 생성.

```bash
$ mkdir ts-practice
$ cd ts-practice
$ yarn init -y
```



- tsconfig.json 생성.

```javascript
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true,
    "outDir": "./dist"
  }
}
```



> target : 컴파일된 코드가 어떤 환경에서 실행될 지 정의합니다.
>
> module : 컴파일된 코드가 어떤 모듈 시스템을 사용하는지 정의합니다.
>
> strict : 모든 타입 체킹 옵션을 활성화한다는 것을 의미합니다.
>
> esModuleInterop : commonjs 모듈 형태로 이루어진 파일을 es2015 모듈 형태로 불러올 수 있게 해줍니다.
>
> outDir : 컴파일된 파일들이 저장되는 경로를 지정할 수 있습니다.



- typescript 로컬로 설치

````bash
$ npm install --save typescript
````

- 그 후 package.json파일에 scripts부분에 build: tsc 추가.

- `npm run build`로 입력.



### 기본타입

src/practice.ts

```typescript
let count = 0; // 숫자
count += 1;
count = '갑자기 분위기 문자열'; // 이러면 에러가 납니다!

const message: string = 'hello world'; // 문자열

const done: boolean = true; // 불리언 값

const numbers: number[] = [1, 2, 3]; // 숫자 배열
const messages: string[] = ['hello', 'world']; // 문자열 배열

messages.push(1); // 숫자 넣으려고 하면.. 안된다!

let mightBeUndefined: string | undefined = undefined; // string 일수도 있고 undefined 일수도 있음
let nullableNumber: number | null = null; // number 일수도 있고 null 일수도 있음

let color: 'red' | 'orange' | 'yellow' = 'red'; // red, orange, yellow 중 하나임
color = 'yellow';
color = 'green'; // 에러 발생!
```



위와 같이 사전에 지정한 타입이 아닐경우 error발생. 그리고 error발생시 컴파일이 불가능합니다.



**함수에서 타입 정의하기**

```typescript
function sum(x: number, y: number): number {
    return x + y;
}

sum(1, 2);
```



위와 같이 함수 파라미터에 `(x: number, y: number)` 같이 타입을 명시하여 사용할 수 있습니다. 

또한, `): number {` 이렇게 return 타입이 number라는 걸 명시하여 return시 갑작스럽게 null을 반환한다면 오류가 뜨게 됩니다.



또 다른 예로, `sumArray`함수를 작성합니다.

**src/practice.js**

```typescript
function sumArray(numbers: number[]): number {
	return numbers.reduce((acc, current) => acc + current, 0);
}

const total = sumArray([1,2,3,4,5]);  // 15
```



*** 함수타입 작성**

````typescript
let myAdd: (x: number, y: number) => number = 
    function(x: number, y: number): number { return x + y };
````



`=> number` : 함수 반환 타입

즉, `myAdd`라는 변수에 `function(x:number, y:number): number {return  x + y }`를 할당.



#### interface 사용해보기

````typescript
interface Shape {
  getArea(): number;
}

class Circle implements Shape {
  radius: number;

  constructor(radius: number) {
    this.radius = radius;
  }

  getArea() {
    return this.radius * this.radius *Math.PI;
  }
}

class Rectangle implements Shape {
  
  width: number;
  height: number;
  constructor(width: number, height: number) {
    this.width = width;
    this.height = height;
  }

  getArea() {
    return this.width * this.height;
  }
}

const shapes: Shape[] = [new Circle(5), new Rectangle(10, 5)];

shapes.forEach(shape => {
  console.log(shape.getArea());
})
````

- Shape를 implements를 하면 반드시 `getArea()`를 구현해야한다.



위의 예제를 accessor를 통해  작성한다면

````typescript
  width: number;
  height: number;
  constructor(width: number, height: number) {
    this.width = width;
    this.height = height;
  }
````

이 부분을 아래와 같이 나타낼 수 있다.

````typescript
  constructor(private width: number, private height: number) {
    this.width = width;
    this.height = height;
  }
````



`public` accessor의 경우는 `circle.radius`와 같이 직접 접근이 가능한 반면,

`private` accessor의 경우는 `rectangle.width`와 같이 직접 접근하는 것이 불가능 하다.



**일반 객체를 interface로 타입 설정하기**

````typescript
interface Person {
  name: string;
  age?: number; // 물음표가 들어갔다는 것은, 설정을 해도 되고 안해도 되는 값이라는 것을 의미합니다.
}
interface Developer {
  name: string;
  age?: number;
  skills: string[];
}

const person: Person = {
  name: '김사람',
  age: 20
};

const expert: Developer = {
  name: '김개발',
  skills: ['javascript', 'react']
};

````

위의 Developer와 Person은 형태가 비슷하여 extends를 이용하여 상속받아 사용할 수 있습니다.

````typescript
interface Person {
  name: string;
  age?: number; // 물음표가 들어갔다는 것은, 설정을 해도 되고 안해도 되는 값이라는 것을 의미합니다.
}
interface Developer extends Person {
  skills: string[];
}

const person: Person = {
  name: '김사람',
  age: 20
};

const expert: Developer = {
  name: '김개발',
  skills: ['javascript', 'react']
};

const people: Person[] = [person, expert];
````



#### Type Alias 사용하기

`type`은 특정 타입에 별칭을 붙이는 용도로 사용합니다.



```typescript
type Person = {
  name: string;
  age?: number; // 물음표가 들어갔다는 것은, 설정을 해도 되고 안해도 되는 값이라는 것을 의미합니다.
};

// & 는 Intersection 으로서 두개 이상의 타입들을 합쳐줍니다.
// 참고: https://www.typescriptlang.org/docs/handbook/advanced-types.html#intersection-types
type Developer = Person & {
  skills: string[];
};

const person: Person = {
  name: '김사람'
};

const expert: Developer = {
  name: '김개발',
  skills: ['javascript', 'react']
};

type People = Person[]; // Person[] 를 이제 앞으로 People 이라는 타입으로 사용 할 수 있습니다.
const people: People = [person, expert];

type Color = 'red' | 'orange' | 'yellow';
const color: Color = 'red';
const colors: Color[] = ['red', 'orange'];
```



`type`과 `interface` 의 용도는 비슷합니다. 하지만 라이브러리를 작성하거나 다른 라이브러리를 위한 타입 지원 파일 작성시, `interface`가 권장됩니다.



### Generic

 제네릭은 타입스크립트에서 함수, 클래스, `interface`, `type`을 사용하게 될 때 여러 종류의 타입에 대하여 호환을 맞춰야 하는 상황에서 사용하는 문법입니다. 



**example** 

```typescript
function wrap<T>(param: T) {
  return {
    param
  }
}

const wrapped = wrap(10);
```

위와 같이 작성시 10이라는 number 타입이 깨지지 않습니다.



