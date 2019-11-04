# 리액트 프로젝트에서 타입스크립트 사용하기 #4 #TIL

### TypeScript 환경에서 리액트 Context API 제대로 활용하기



이 글은 [리액트 프로젝트에서 타입스크립트 사용하기 - velopert]( https://velog.io/@velopert/create-typescript-react-component ) 를 참고하여 작성하였습니다.



---



### 프로젝트 준비

````bash
$ npx create-react-app ts-context-api-tutorial --typescript
````



3 가지의 파일 생성

- TodoForm.tsx: 새 할 일을 등록할 때 보여줍니다.
- TodoItem.tsx: 할 일에 대한 정보를 보여줍니다.
- TodoList.tsx: 여러 TodoItem들을 렌더링 해줍니다.



- **src/components/TodoForm.tsx**

```typescript
import React, { useState } from 'react';

function TodoForm() {
  const [ value, setValue ] = useState('');			// useState 초기화

  const onSubmit = (e: React.FormEvent) => {		// onSubmit 실행시 값 초기화
    e.preventDefault();
    setValue('');
  }

  return (
    <form onSubmit={onSubmit}>
      <input
        value={value}
        placeholder="무엇을 하실 건가요?"
        onChange={e => setValue(e.target.value)}
      />
      <button>등록</button>
    </form>
  );
}

export default TodoForm;
```

- **src/components/TodoItem.tsx**

````typescript
import React from 'react';
import './TodoItem.css';

export type TodoItemProps = {
  todo: {
    id: number;
    text: string;
    done: boolean;
  };
}

function TodoItem({ todo }: TodoItemProps) {			// TodoItemProps 형태의 todo
  return (
    <li className={`TodoItem ${todo.done ? 'done' : ''}`}>
      <span className="text">{todo.text}</span>
      <span className="remove">(X)</span>
    </li>
  );
}

export default TodoItem;
````

- **src/components/TodoList.tsx**

````typescript
import React from 'react';
import TodoItem from './TodoItem';

function TodoList() {
  const todos = [
    {
      id: 1,
      text: 'Context API 배우기',
      done: true
    },
    {
      id: 2,
      text: 'TypeScript 배우기',
      done: true
    },
    {
      id: 3,
      text: 'TypeScript 와 Context API 함께 사용하기',
      done: false
    }
  ];

  return (
    <ul>
      {todos.map(todo => (
        <TodoItem todo={todo} key={todo.id} />			// todo
      ))}
    </ul>
  );
}

export default TodoList;

````



