````javascript
const dataLoader = async function*(...aIters){
    let prev; // 격변
    for(const iter of aIters) {
        iter.update(prev);
        prev = (await iter.load().next()).value;	// 격변
        yield prev;
    }
};
const render = async function(...aIters){
    for await(const json of dataLoader(PrevPass, ...aIters)) {
        console.log(json);
    }
}
````

> 추상화라는 것. 덜 변화하는 것 === '추상화'. 변화가 일어나는 부분만 고치기 위해 추상화를 한다.

prev update와 iter.load()는 트랜잭션이다. 즉, 같이 가야하는 메소드다.

=> load로 묶음



```javascript
const dataLoader = async function*(pass, ...aIters) {
    const dataPass = new pass;
    for(const item of aIters) {
        const v = await item.load(dataPass.data).next();
        yield dataPass.data = v.value;
    }
}
const render = async function(...aIters) {
    for await(const json of dataLoader(...aIters)){
        console.log(json)
    }
}

const DataPass = class {
   get data(){throw "override";};
   set data(v){throw "override";};
}
const PrevPass = class extends DataPass{
    #data;
    get data(){return this.#data;}
    set data(v){return this.#data = v;}
const IncPass = class extends DataPass{
    #data = [];
        get data(){return this.#data;}
    set data(v){return this.#data.push(v);}
}
```

> 변화하는 부분은 따로 역할을 분리 후 런타임 바인딩!
>
> 런타임 바인딩: 내가 실행하는 시점에 바인딩 되는것. 마음대로 수정 가능하다.



### Async Item

```javascript
const AsyncItem = class{
    static private dataPass; static private items;
    static iterable(dataPass, ...items){
        AsyncItem.dataPass = dataPass;
        AsyncItem.items = items;
        return AsyncItem;
    }
    static async *[Symbol.asyncIterator]() {
        const dataPass = new AsyncItem.dataPass;
        for(const item of AsyncItem.items){
            const v = await item.load(dataPass.data).next();
            yield dataPass.data = v.value;
        }
    }
    async *load(v){throw "override";}
}
const render = async function(...aIters){
    for await(const json of AsyncItem.iterable(PrevPass, ...aIters)) {
        console.log(json);
    }
}
```



```javascript
const Renderer = class{
    dataPass;
    constructor(dataPass) {
        this.dataPass = dataPass;
    }
    set dataPass(v){this.dataPass = v;}
    async render(...items) {
        const iter = AsyncItem.iterable(this.dataPass, ...items);
        for await(const v of iter) cosnole.log("**", v);
    }
};
const renderer = new Renderer(PrevPass);
renderer.render(...)
```



```javascript
const AsyncItem = class {
	static ...
    async *load(v){throw "override";}
};

const Url = class extends AsyncItem{
    #url, #opt, #dataF;
    constructor(u, opt, dataF = JSON.stringfy) {
        super();
        this.#url = u;
        this.#opt = opt;
        this.#dataF = dataF;
    }
	async *load(v) {
        if(v) this.#opt.body = this.dataF(v);
        return await(await fetch(this.#url, this.#opt)).json();
    }
};
```

urls

```javascript
const Parallel = class extends AsyncItem{
    #items;
    constructor(...items){
        super();
        this.#items = items;
    }
	async *load(data) {
        const arr = [...this.#items].map(item=>item.load(data).next());
        return (await Promise.all(arr)).map(v=>v.value);n  
    }
} 
```

> 인스턴스의 필드면 트랜잭션으로서 작동할 수 없다. 개입 가능성이 있다.
>
> 트랜잭션이면 트랜잭션으로 이용하자.

