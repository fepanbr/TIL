## 리액트 프로젝트에서 타입스크립트 사용하기 #2 #TIL



이 글은 [리액트 프로젝트에서 타입스크립트 사용하기 - velopert]( https://velog.io/@velopert/create-typescript-react-component ) 를 참고하여 작성하였습니다.



### 프로젝트 생성

````bash
$ npx create-react-app ts-react-tutorial --typescript
````



타입스크립트를 사용하는 react 컴포넌트의 경우 `*.tsx`를 사용합니다.

그리고 App.tsx를 보면 

`React.FC = () => {}` 처럼 함수형컴포넌트로 선언되어있는데, 요즘은 function을 쓰는 추세라고 합니다.



### 새로운 컴포넌트 만들기

- **src/Greeting.tsx** 생성

````typescript
import React from 'react';

type GreetingProps = {
  name: string;
}

const Greetings: React.FC<GreetingProps> = ({ name }) => (
  <div>Hello, {name}</div>
);

export default Greetings;
````



#### React.FC의 장단점

React.FC를 사용할 때 props 타입을 **Generics**로 사용합니다. 이 때 얻을 수 있는 이점은 두가지입니다.

1. props에 기본적으로 `children`이 들어가 있다는 것
2. 컴포넌트의 defaultProps, propTypes, contextTypes를 설정할 때 자동완성이 된다는 점.

하지만 반대로 단점도 있습니다.

`children` 이 optional 형태여서 props의 타입이 명백하지 않습니다. 예를 들어 어떤 컴포넌트는 `children`이 무조건 있어야 하는 경우도 있을 것이고, 어떤 컴포넌트는 `children` 이 들어가면 안되는 경우도 있을 것입니다. 결국 그에 대한 처리를 하고 싶다면 Props 타입 안에 `children` 을 명시해야 합니다.



```typescript
type GreetingProps = {
    name: string;
    children: React.ReactNode;
}
```



#### 결국

React.FC를 사용하기 보다, function을 사용하는 것이 좋습니다.

- src/Greetings.tsx

```typescript
import React from 'react';

type GreetingProps = {
  name: string;
  mark: string;
};

function Greetings({ name, mark }: GreetingProps) {
  return (
    <div>
      Hello, {name} {mark}
    </div>
  );
}

Greetings.defaultProps ={
  mark: '!'
};


export default Greetings;
```



#### 컴포넌트에서 생략할 수 있는 props 설정하기



컴포넌트중에 생략해도 되는 props가 있다면 `?` 를 이용합니다.

```typescript
import React from 'react';

type GreetingsProps = {
  name: string;
  mark: string;
  optional?: string;		// 필수적으로 필요한 props가 아님
};

function Greetings({ name, mark, optional }: GreetingsProps) {
  return (
    <div>
      Hello, {name} {mark}
      {optional && <p>{optional}</p>}
    </div>
  );
}

Greetings.defaultProps = {
  mark: '!'
};

export default Greetings;
```



#### 함수 타입의 props 받아오기

특정 함수를 props로 받아오기 위해서는 

- **src/Greetings.tsx**

````typescript
import React from 'react';

type GreetingProps = {
  name: string;
  mark: string;
  optional?: string;      // 필수적인 요소가 아님
  onClick: (name: string) => void;		//onClick시, parameter를 string, return은 void
};

function Greetings({ name, mark, optional, onClick }: GreetingProps) {
    const handleClick = () => onClick(name);
  return (
    <div>
      Hello, {name} {mark}
      {optional && <p>{optional}</p>}
      <div>
          <button>Click Me!</button>
       </div>
    </div>
  );
}

Greetings.defaultProps ={
  mark: '!'
};


export default Greetings;
````

- **src/App.tsx**

````typescript
import React from 'react';
import Greetings from './Greetings';

const App: React.FC = () => {
  const onClick = (name: string) => {
    console.log(`${name} says hello`);
  };
  return <Greetings name="Hello" onClick={onClick} />;
};

export default App;
````



### 정리 

- `React.FC`는 좋지 않다.
- 함수형 컴포넌트를 작성 할 때는 화살표로 작성해도 되고, `function`으로 작성해도 된다.(`function` 권장)
- Props에 대한 타입을 선언 할 땐 `interface` 또는 `type`을 사용하면 되며, **일관성** 있게 진행하는게 중요.



**&#128549; 헷갈리는 점**

**onClick과 같은 eventHandler를 전달하는 방법** 







출처 - [리액트 프로젝트에서 타입스크립트 사용하기 - velopert]( https://velog.io/@velopert/create-typescript-react-component )

