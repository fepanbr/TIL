## 리액트 프로젝트에서 타입스크립트 사용하기 #3 #TIL

**타입 스크립트로 리액트 Hooks 사용하기(useState, useReducer, useRef)**



이 글은 [리액트 프로젝트에서 타입스크립트 사용하기 - velopert]( https://velog.io/@velopert/create-typescript-react-component ) 를 참고하여 작성하였습니다.

-----



### useState 및 이벤트 관리

타입스크립트 환경에서 `uesState`를 사용하는 방법에 대해 알아보고자 합니다.



#### 카운터 만들기

우선 Counter.tsx를 만듭니다.



- **Counter.tsx**

````typescript
import React, { useState } from 'react';

function Counter () {
  const [count, setCount] = useState<number>(0);	// 상태가 어떤값을 가지는지 Generic 형태로 사용
  const onIncrease = () => setCount(count + 1);
  const onDecrease = () => setCount(count - 1);
  return (
    <div>
      <h1>{count}</h1>
      <div>
        <button onClick={onIncrease}>+1</button>
        <button onClick={onDecrease}>-1</button>
      </div>
    </div>
  );
}

export default Counter;
````

그 후, App.tsx에서 랜더링 해봅니다.

- **src/App.tsx**

````typescript
import React from 'react';
import Counter from './Counter';

const App: React.FC = () => {
  return <Counter />;
};

export default App;
````

#### 실습 모습

![Counter 예제사진](C:\Users\fepan\OneDrive\바탕 화면\Counter예제 확인.png)





**😁Tip**

사실 useState에서 Generics을 사용하지 않아도 무방합니다. 하지만 **상태가 `null`일 수 있을 때는 Generics을 활용하시면 좋습니다.** 또는 **까다로운 구조를 가진 객체거나 배열**일 때는 Generics를 명시하는 것이 좋습니다.



- `null`이 예상될 때

```typescript
type Information = { name: string; description: string };
const [info, setInformation] = useState<Information | null>(null);
```

- 까다로운 객체거나 배열일 때

````typescript
type Todo = { id: number; text: string; done: boolean };
const [todos, setTodos] = useState<Todo[]>([]);
````



### 인풋 상태 관리하기



- **src/MyForm.tsx**

````typescript
import React, { useState } from 'react';

type MyFormProps = {
  onSubmit: (form: { name: string; description: string }) => void;
};

function MyForm({ onSubmit }: MyFormProps) {
  const [form, setForm] = useState({
    name: '',
    description: ''
  });

  const { name, description } = form;

  const onChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    const { name, value } = e.target;
    setForm({
      ...form,
      [name]: value
    });
  };

  const handleSubmit = (e: React.FormEvent<HTMLFormElement>) => {
    e.preventDefault();
    onSubmit(form);
    setForm({
      name: '',
      description: ''
    }); // 초기화
  };

  return (
    <form onSubmit={handleSubmit}>
      <input name="name" value={name} onChange={onChange} />
      <input name="description" value={description} onChange={onChange} />
      <button type="submit">등록</button>
    </form>
  )
}

export default MyForm;
````



- src/App.tsx

````typescript
import React from 'react';
import MyForm from './MyForm';

const App: React.FC = () => {
  const onSubmit = (form: { name: string; description: string }) => {
    console.log(form);
  };
  return <MyForm onSubmit={onSubmit} />;
};

export default App;
````



`onChange`는 setState하는 함수이고, `handleSubmit`은 초기화 하는 함수입니다.





### use Redeucer

타입스크립트 환경에서 `useReducer`를 사용할 때 코드를 어떻게 준비해야할가요?





#### 카운터를 `useReducer`로 다시 나타내기

Counter 컴포넌트를 `useState`가 아닌 `useReducer`로 사용하는 코드로 나타냅니다.



-  **src/Counter.tsx**

````typescript
import React, { useReducer } from 'react';

type Action = { type: 'INCREASE' } | { type: 'DECREASE' };

function reducer(state: number, action: Action): number{
  switch(action.type) {
    case 'INCREASE':
      return state + 1;
    case 'DECREASE':
      return state - 1;
    default:
      throw new Error('Unhandled action');
  }
}

function Counter() {
  const[ count, dispatch ] = useReducer(reducer, 0);
  const onIncrease = () => dispatch({ type: 'INCREASE' });
  const onDecrease = () => dispatch({ type: 'DECREASE' });

  return (
    <div>
      <h1>{count}</h1>
      <div>
        <button onClick={onIncrease}>+1</button>
        <button onClick={onDecrease}>-1</button>
      </div>
    </div>
  );
}


export default Counter;
````



`Action` 부분을 보면 Action 타입은 `{ type: 'INCREASE' }` 또는 `{ type: 'DECREASE' }`임을 명시합니다.

또한, `reducer`함수 맨 윗줄에 있는

```typescript
function reducer(state: number, action: Action): number
```

에서는 `state`타입과 리턴 타입을 동일하게 했습니다. 이것은 매우 중요합니다.



**이유??**

> 이렇게 동일한 타입으로 선언하게 되면, 실수들을 방지할 수 있습니다.(예: 특정 케이스에 결과값을 반환하지 않았거나, 상태의 타입이 바뀌게 되었을 경우 error를 감지할 수 있습니다.)



그리고 액션객체에 다른 값들이 필요할 경우 그 값들의 타입을 정해준다면 자동완성을 통해 확인할 수 있게 됩니다.



### ReducerSample 구현하기

자동완성이 되는것과 타입검사가 되는 것을 직접 확인하기 위해 ReducerSample 이라는 컴포넌트를 만들겠습니다.

- **src/ReducerSample**

````typescript
import React, { useReducer } from 'react';

type Color = 'red' | 'blue' | 'yellow';

type State = {
  count: number;
  text: string;
  color: Color;
  isGood: boolean;
};

type Action = 
  | { type: 'SET_COUNT'; count: number }
  | { type: 'SET_TEXT'; text: string }
  | { type: 'SET_COLOR'; color: Color }
  | { type: 'TOGGLE_GOOD'; };

function reducer ( state: State, action: Action ): State {
  switch(action.type){
    case 'SET_COUNT':
      return {
        ...state,
        count: action.count   // count가 자동완되며, number 타입인걸 확인할 수 있다.
      };
    case 'SET_TEXT':
      return {
        ...state,
        text: action.text
      };
    case 'SET_COLOR':
      return {
        ...state,
        color: action.color
      };
    case 'TOGGLE_GOOD':
      return {
        ...state,
        isGood: !state.isGood
      };
    default:
      throw new Error('Unhandled action');
  }
}

function ReducerSample() {
  const [state, dispatch] = useReducer(reducer, {
    count: 0,
    text: '',
    color: 'red',
    isGood: true
  });

  const setCount = () => dispatch({ type: 'SET_COUNT', count: 5 });     // count를 넣지 않으면 에러 발생
  const setText = () => dispatch({ type: 'SET_TEXT', text: 'bye' });
  const setColor = () => dispatch({ type: 'SET_COLOR', color: 'blue' });    /// 'blue'를 넣지 않으면 에러발생
  const toggleGood = () => dispatch({ type: 'TOGGLE_GOOD' });

  return (
    <div>
      <p>
        <code>count: </code> {state.count}
      </p>
      <p>
        <code>text: </code> {state.text}
      </p>
      <p>
        <code>color: </code> {state.color}
      </p>
      <p>
        <code>isGood: </code> {state.isGood ? 'true' : 'false'}
      </p>
      <div>
        <button onClick={setCount}>SET_COUNT</button>
        <button onClick={setText}>SET_TEXT</button>
        <button onClick={setColor}>SET_COLOR</button>
        <button onClick={toggleGood}>TOGGLE_GOOD</button>
      </div>
    </div>
  );
}

export default ReducerSample;
````



**Point**

1.  Action들은 `type`만 존재하지 않고 추가적인 값들이 있을 때 `Action`이라는 타입을 정의함으로써 Reducer에서 자동 완성이 되어 개발의 편의성을 제공합니다.
2. 액션을 dispatch할 때도 액션에 대한 타입검사가 이루어지므로 사소한 실수를 줄일 수 있습니다.



- **src/App.tsx**

```typescript
import React from 'react';
import ReducerSample from './ReducerSample';

const App: React.FC = () => {
  return <ReducerSample />;
};

export default App;
```





### useRef

`useRef`는 우리가 리액트 컴포넌트에서 외부 라이브러리의 인스턴스 또는 DOM을 특정 값 안에 담을 때 사용합니다. 추가적으로, 이를 통해 컴포넌트 내부에서 관리하고 있는 값을 관리할 때 유용합니다. 하지만, 이 값은 렌더링과는 관계가 없어야 합니다.



#### 변수 값 관리하기

타입스크립트 환경에서 `useRef`를 통해 어떤 변수 값을 관리하고 싶을 땐 다음과 같은 코드를 작성합니다.

````typescript
const id = useRef<number>(0);
  const increaseId = () => {
    id.current += 1;
  }
````



 `useRef` 를 쓸땐 위와 같은 코드처럼 Generic 을 통해 `~.current` 의 값을 추론 할 수 있습니다. 



#### DOM 관리하기

ref 안에 DOM을 담을 때도 마찬가지입니다. 단, 초기값은 `null`로 해야 합니다. 다음의 예제에서 확인해봅니다.

```typescript
import React, { useState, useRef } from 'react';

type MyFormProps = {
  onSubmit: (form: { name: string; description: string }) => void;
};

function MyForm({ onSubmit }: MyFormProps) {
  const inputRef = useRef<HTMLInputElement>(null);		// 초기값 설정 null
  
  const [form, setForm] = useState({
    name: '',
    description: ''
  });

  const { name, description } = form;

  const onChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    const { name, value } = e.target;
    setForm({
      ...form,
      [name]: value
    });
  };

  const handleSubmit = (e: React.FormEvent<HTMLFormElement>) => {
    e.preventDefault();
    onSubmit(form);
    setForm({
      name: '',
      description: ''
    }); // 초기화
    if (!inputRef.current){   // inputRef
      return;
    }
    inputRef.current.focus();
  };

  return (
    <form onSubmit={handleSubmit}>
      <input name="name" value={name} onChange={onChange} ref={inputRef} />   // 변경부분
      <input name="description" value={description} onChange={onChange} />
      <button type="submit">등록</button>
    </form>
  )
}

export default MyForm;
```



`inputRef` 쪽 코드를 보면 다음과 같이 Generic 으로 `HTMLInputElement` 타입을 넣어주었습니다.

```typescript
 const inputRef = useRef<HTMLInputElement>(null);
```

추후 `ref`를 사용 할 때 어떤 타입을 써야 하지? 하고 헷갈릴 수 있을 것입니다. 그럴 땐, 에디터 상에서 커서를 원하는 DOM 위에 올려보세요.



 추가적으로, `inputRef.current` 안의 값을 사용 하려면 `null` 체킹을 해주어야 합니다. 즉, 특정 값이 정말 유효한지 유효하지 않은지 체크해서, 타입스크립트에서 만약 어떤 타입이 `undefined` 이거나 `null` 일 수 있는 상황에는 해당 값이 유효한지 체킹하는 작업을 꼭 해주어야 자동완성도 잘 이루어지고, 오류도 사라집니다. 





### 정리

- `useState`를 사용할 때에는 `useState<string>`과 같이 Generics를 사용합니다.
- `useState`의 Generics는 상황에 따라 생략할 수 있지만, 상태가 `null`일 경우나, 까다로운 배열이나 객체의 경우 Generics를 명시해야 합니다.
- `useReducer`를 사용할 때에는 액션에 대한 타입스크립트를 모두 준비해서 `|`를 이용하여 타입체크와 자동완성을 이용합니다.
- `useRef`를 사용하여 DOM에 대한 정보를 담을 땐, 초기값을 `null`로 설정하여 사용하고 값을 사용하기 위해 `null`체크를 반드시 합니다.



### 이해가 안되는 점

- useRef의 의미
- [name]과 같이 []로 묶는 이유