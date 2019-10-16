## redux(생활코딩) ##

**state** : 상태값을 가지고 있다. 

```javascript
function reducer(oldState, action) {
    //....
}
var store = Redux.createStore(reducer);
```

Redux를 만드는 reducer



**render ** : 우리가 짤 코드, 

Store에 직접 접근할 수 없다. 

그래서 접근할 수 있는 함수들이 있다.



``` javascript
function render() {
    var state = store.getState(); // state상태 가져오기
    //...
    document.querySelector('#app').innerHTML = `
	<h1>...</h1>
`
}
```

state 값이 바뀔 때마다 render를 하는 함수 subscribe()



```javascript
<form onsubmit="
	//...
	store.dispatch({type:'create', payload:{title:title, desc:desc}});
">
```



dispatch()를 통해 Action 객체를 전달   

dispatch()는 2가지를 일을합니다.

reducer를 호출하여 state 값을 바꿉니다.

그작업후 subscribe을 통해 render를 호출

dipatch가 reducer를 호출할 때 두가지값을 전달합니다.

현재 state값과 action객체를 전달합니다.

그리고 return하는 객체는  새로운 state입니다.

state값이 변경, dispatch가 subscribe을 호출하고, subscribe은 render를 호출하고 state를 가져와 화면이 변경됩니다.



**getState** : state에 접근

**subscribe** : state변경됬을 때 구동될 함수를 등록한다.

**dispatch** : 값을 변경한다.



# redux가 좋은 이유

* 중앙 집중적인 데이터 스토어를 통해 애플리케이션을 쉽게 개발가능.(**복잡성 감소**)

* 형상관리 하듯이 모든 변화를 확인 할 수 있다. 즉 시간관리를 할 수 있다.