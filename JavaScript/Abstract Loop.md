javascript는 함수를 값으로 사용.

선언하지 말기.



class도 변수에 할당하기.



JSON.parse(JSON.stringfy)가 제일 빠르다.

내가 생각한걸 "정확"하게 표현해줘야한다.



주석 버리자.



문으로 확정되면, 방법 없음. 복사해서 써야함.



결국 제어문을 직접 사용할 수 없고 구조 객체를 이용해 루프 실행기를 별도로 구현.

프로그램의 원리: if문 제거가 중요.

if제거방법: 외부에서 값을 설정해놓고, 그 값을 가져옴.



주어진 라이브러리를 잘 사용하는게 스크립트언어에서는 좋다.

구조적인 문제를 해결하는데 집중.(if를 줄이는데 사용.)



## Abstract Loop





```javascript
const Operator = class {
	static factory(v) {
        if(v instanceof Object) {
            if(!Array.isArray(v)) v = Object.values(v);
            return new ArrayOp(v.map(v => Operator.factory(v)));
        }else return new PrimaOp(v);
    }
    constructor(v){this.v = v;}
    operation(f){throw 'override';}
};
const PrimaOp = class extends Operator {
    constructor(v){super(v);}
    operator(v){f(this.v)}
}
```



# Yield



```javascript
const odd = function*(data) {
    for(const v of data) {
        console.log("odd", odd.cnt++);
        if(v % 2) yield v;
    }
};

odd.cnt = 0;
for(const v of odd([1,2,3,4])) console.log(v);
```

```javascript
const take = function*(data, n) {
    for(const v of data) {
		if(n--) yield v; else break;
    }
};
take.cnt = 0;
for(const v of take([1,2,3,4], 2)) console.log(v);
```





```javascript
const Stream = class {
    static get(v) {return new Stream(v);}
    constructor(v) {
        this.v = v;
        this.filters = [];
    }
    
    add(gene, ...arg) {
        this.filters.push(v => gene(v, ...arg));
        return this;
    }
    
    *gene() {
        let v = this.v;
        for(const f of this.filters) v = f(v);
        yield* v;
    }
}
```

```javascript
const odd = function*(data) {
    for(const v of data) if(v % 2) yield v;
};
const take = function*(data, n) {
    for(const v of data) if(n--) yield v; else break;
}

for(const v of Stream.get([1,2,3,4])).add(odd).add(take, 2).gene());
console.log(v);
```

