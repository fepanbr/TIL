# Symbol



MDN - Symbol 



Symbol은 primitive data type. Symbol 함수는 sysmbol 타입의 value를 리턴하고, 심볼은 static property와 static method를 가지고 있음. 하지만, new Symbol() 키워드를 지원하지 않아, constructor 측면으로는 불완전하다. 



Symbol()에서 return 하는 값들은 모두 uniq하다. **Symbol 값은 객체 프로퍼티에 대한 식별자로 사용될 수 있다. 이것이 Symbol의 목적이다. **



심볼을 사용하는 목적은 Symbol의 값은 객체 프로퍼티에 대한 식별자로 사용하여, 기존의 프로퍼티들과 충돌하지 않는 고유의 uniq한 값을 프로퍼티를 만드는것이다.



```javascript
var includes = Symbol('즐거운 자바스크립트');
Array.prototype[includes] = function () {
  return console.log('its Symbol');
}
var arr = [1, 2, 3];
arr.includes(1); // true
arr['includes'](1); // true
arr[includes](); // its Symbol
```





```javascript
let sym1 = Symbol();
let sym2 = Symbol('foo');
let sym3 = Symbol('foo');
```



```javascript
Symbol('foo') === Symbol('foo')		// false
```

각 Symbol은 ('foo')를 사용한다고 해서 같지 않습니다. 이유는 Symbol이 리턴하는 값은 모두 uniq하기 때문입니다.



sysmbol은 객체의 프로퍼티가 될 수 있습니다.

```javascript
var symbol = Symbol("hey");
var obj = { name: "jane" };

obj[symbol] = { age: 8};
console.log(obj);
console.log(obj[symbol]);
console.log()
console.log(obj.symbol);	// type error
```





### Shared symbols in the global symbol registry

Symbol()을 이용하는 문법은 글로벌 심볼을 만들 수 없습니다. 그래서 Symbol.for()나 Symbole.keyFor()를 이용하여 symbol을 global symbol registry에서 검색할 수 있습니다.

위의 예제를 기준으로 생각해보면,

ex)

```javascript
var sym1 = Symbol('foo');

var sym2 = Symbol('foo');

sym1 === sym2		// false

var sym1 = Symbol.for('foo');

var sym2 = Symbol.for('foo');

sym1 === sym2		// true 
```



> global symbol registry
>
> string 키로 접근할 수 있는 registry이다. 









> 출처: 
>
> MDN - [Symbol](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Symbol)
>
> [[javascript] Symbol에 대하여](https://medium.com/@hyunwoojo/javascript-symbol-%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-6aa5903fb6f1)
>
> https://ko.javascript.info/symbol