### const, let 



### null, undefined

null : 없다.

undefined: 아직 정의되지 않았다.



### !(not), &&(and), ||(or)

이 순서대로



truethy와 falsy

falsy : undefined, null, 0, '', NaN



### 단축 평가 논리 계산법

#### && 사용법

```javascript
console.log(true && 'hello');   // hello
console.log(false && 'hello');  // false
console.log('hello' && 'bye');  // bye

// 왼쪽이 'true'면 오른쪽 값이 출력
// 왼쪽이 'false'면 무조건 false
```

사용처 : **어떤값이 유효할 때만 그 값을 사용할 경우 사용**



#### || 사용법

사용처 : 어떤 값이 false일 때 값을 할당할 때 사용



```javascript
console.log(false || 'hello'); // 'hello'
console.log('' || '이름없다.'); // '이름없다'
```

즉, 앞쪽이 false일 경우 오른쪽 값이 할당.

앞쪽이 true면 뒤는 보지도 않는다.

