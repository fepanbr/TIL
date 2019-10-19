dispatch를 호출하면 reducer를 호출하도록 되어있다.

state값을 직접변경하지말고, 복사본을 만들어 변경하여 return해야 시간여행 가능.

```javascript
Object.assign({}, {name:'egoing'}, {city:'seoul'}); // 복사
```

위의 예제를 참고하여 복제한다.

```javascript
if(action.type === 'CHANGE_COLOR'){
    newState = Object.assign({}, state, {color:'red'});
}
return newState;
```



reducer는 action과 이전의 state값을 통해 새로운 state 값을 리턴한다.

이때 새로운 state값은 복제하여 return 한다.

