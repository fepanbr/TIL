## React-Redux 

- **Providing the Store**

우선 Redux의 `store`를 앱에 적용해야 한다. 이 때, `<Provider />` API를 이용한다.



```javascript
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import TodoApp from './TodoApp';

import { Provider } from 'react-redux';
import store from './redux/store';

const rootElement = document.getElementById('root')
ReactDOM.render(
	<Provider store={store}>
    	<TodoApp />
    </Provider>,
	rootElement
)
```

* Connecting the Component

react-redux에서 `connect` 를 함수를 제공한다. `connect`는 Redux의 `store`에 접근하여, 값을 읽을 수 있게 해준다. 

`connect` 함수에는 두가지 argument가 있다.

* `mapStateToProps` : `store`에 값이 변경될 때마다, 호출된다. 전체 `store` 에 state값들을 받아서, component가 필요로 하는 data객체를 return 한다.
* `mapDispatchToProps` : parameter는 함수 혹은 객체일 수 있다. 

만약, parameter가 함수일 경우, component를 한번 호출한다. 그리고 `dispatch` 를 

