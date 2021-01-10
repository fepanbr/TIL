spread

```javascript
const iter = {
    [Symbol.iterator](){return this},
    arr:[1,2,3,4],
    next(){
        return {
            done: this.arr.length == 0,
            value: this.arr.pop()
        };
    }
};
```



제곱을 요소로 갖는 가상 컬렉션

```javascript
const N2 = class{
    constructor(max) {
        this.max = max;
    }
    [Symbol.iterator]() {
		let cursor = 0, max = this.max;
        return {
            done:false,
            next() {
                if(cursor > max) {
                    this.done = true;
                } else {
                    this.value = cursor * cursor;
                    cursor++;
                }
                return this;
            }
        }
	}
}
```

> 루프걸때 늘 limit에 제한을 둔다.
>
> iterator가  제어권을 갖는다. 무한히 false가 되는것을 막아야한다.



동기명령 : 한번에 적재한 명령이 실행되는 것. 간섭 불가능.

블로킹: 동기적인 명령을 실행하는 동안 간섭 못하는 것.

프레임: 리퀘스트, setTimeout: 슬립걸어주는것.





## Generator



```
const N2 = class{
    constructor(max) {
        this.max = max;
    }
    [Symbol.iterator]() {
		let cursor = 0, max = this.max;
        return {
            done:false,
            next() {
                if(cursor > max) {
                    this.done = true;
                } else {
                    this.value = cursor * cursor;
                    cursor++;
                }
                return this;
            }
        }
	}
}
```

같은 코드



```javasc
const generator = function*(max) {
	let cursor = 0;
	while(cursor < max) {
		yield cursor * cursor;
		cursor++;
	}
}
```



yield는 next가 반환되는 효과와 같다.

while문은 정지 불가능



yield는 suspension

call routine 제너레이터



