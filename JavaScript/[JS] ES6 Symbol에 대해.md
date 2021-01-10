# [JS] ES6 Symbol에 대해



### Symbol은 뭘까?

Symbol은 ES6에 새롭게 추가 된 primitive data type이다. 



> primitive data type: String, Boolean, null, undefined, Number 등의 원시 타입이다.



### Symbol의 특징은 뭘까?

1. Symbol()은 new 키워드로 선언하지 않는다

```javascript
const sym = Symbol('hi');	// Symbol('hi')
const sym2 = new Symbol('ho')	//  error
```



2. Symbol()의 return 값은 모두 **unique**하다

```javascript
const sym1 = Symbol('Hee');
const sym2 = Symbol('Hee');

console.log(sym1 === sym2);		// false
```





### Symbol을 어디에 사용할까?

#### 객체 프로퍼티에 대한 식별자로 사용한다.

Symbol의 return 값은 고유(unique)하기 객체의 고유한 프로퍼티로 사용할 수 있다. **즉, 객체에 어떠한 프로퍼티와도 충돌하지 않는다.**

```javascript
var person = {
    name: 'ch.park',
    age: 12,
}

var nameSymbol = Symbol('name');
person[nameSymbol] = 'know';

console.log(person['name'])		//  'ch.park'
console.log(person[nameSymbol]) // 'know'
```



#### Symbol.for를 사용하여 전역 심볼로 사용할 수 있다.

Symbol.for()를 이용하면, global symbol registry에 등록 된 symbol을 찾아, 있으면 그 값을 return하고, 없으면 새롭게 전역 심볼로 등록합니다.



```javascript
const sym1 = Symbol.for('Hee');
const sym2 = Symbol.for('Hee');

console.log(sym1 === sym2);		// true
```

