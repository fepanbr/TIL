## Sequential Async



````javascript
const render = function(...urls) {
	Promise.all(url=>fetch(url, {method: "GET"}).then(res => res.json())).then(arr=>{
        arr.forEach(console.log);
    });
};

render("1.json", "2.json", "3.json");
````



```javascript
const render = function(...urls) {
    const loop =_=> {
        if (urls.length) {
            fetch(urls.shift(), {method: "GET"}).then(res=>res.json()).then(json=> {
				console.log(json);
                loop();
            });
        }
    };
}
```

### Generator & Executor

```javascript
const dataLoader = function*(f, ...urls) {
    for(const url of urls) {
        const json = yield fetch(url, {method: "GET"}l).then(res => res.json());
    }
};

const render = function(...urls) {
    const iter = dataLoader(console.log, ...urls);
    const next = ({value, done})=> {
        if(!done) value.then(v=>next(iter.next(v)));
    };
    next(iter.next())
}
```



> 외부에서 그 이후를 진행하기 위해서. 프로미스를 쓴다. 반제어를 할 때 의미를 갖는다. 즉, then을 따로 쓸 때. 유용



```javascript
const dataLoader = function*(f, ...urls) {
    for(const url of urls) {
        const json = yield fetch(url, {method: "GET"}).then(res => res.json());
        yield json;
    }
};

const render = function(...urls) {
    const iter = dataLoader(...urls);
    const next = ({value, done})=>{
        if(!done){
            if(value instanceof Promise) value.then(v=>next(iter.next(v)));
            else{
                console.log(value);
                next(iter.next());
            }
        }
    };
    next(iter.next());
};
render("1.json", "2.json", "3.json");
```



## Async Iterator

async  await 는 외부에 제어권을 줄 방법이 없다.



```javascript
const render = async function(...urls) {
    for(const url of urls) {
        console.log(await (await fetch(url, {method: "GET"})).json());
        // 제어와 렌더링 두 부분이 같이 들어갈 수 밖에 없다.
    }
};
render("1.json", "2.json", "3.json");
```



```javascript
const dataLoader = async function*(...urls) {
    for(const url of urls) {
        yield await(await fetch(url, {method: "GET"}).json());
    }
};

const render = async function(...urls) {
    for await(const json of dataLoader(...urls)) {
        console.log(json)
    }
};
render("1.json", "2.json", "3.json");
```

### Async yield*

```javascript
const urlLoader = async function*(url) {
	yield await(await fetch(url, method: "GET")).json();
};
const dataLoader = async function*(...urls){
    for(const url of urls) yield* urlLoader(url);
};
const render = async function(...urls) {
    for await(const json of dataLoader(...urls)) {
        console.log(json)
    }
};
```

> yield*은 sub Iterator를 상위 iterator로 이동시킬 수 있다.



### Aysnc Group

```javascript
const urls = async function*(...urls) {
    const r = [];
    for(const u of urls.map(url)) r.push((await u.next()).value);
    yield r;
}
const render = async function(...aIters) {
    for await(const json of dataLoader(...aIters) console.log)
}
render(urls("1.json", "2.json"), url("3.json"));
```



```javascript
const start = function*(url){yield "load start";};
const end = function*(url){yield "load end";};
const urls = async function*(...urls) {
    const r = [];
    for(const u of urls.map(url)) r.push((await u.next()).value);
    yield r;
}
const render = async function(...aIters) {
    for await(const json of dataLoader(...aIters) console.log)
}
render(start(), urls("1.json", "2.json"), url("3.json"), end());
```

> async iterator가 아니더라도 yield*를 통해 꺼낼 수 있다.



### Pass Param

1,2 데이터를 취합해 3을 로딩함.

어떻게 하면 그다음 애한테 데이터를 넘겨올것인가. 일반화.



```typescript
const url = (url, opt = {method:"POST"})=>new Url(url, opt);
const Url = class {
    private url;
    private opt;
    consturctor(url, opt)  {
		this.#url = url;
        this.#opt = opt;
    }

	async *load(){
        yield await(await fetch(this.url, this.opt)).json();
    }
}
```

>함수형 async Generator는 생성 시점의 인자와 지역변수만 사용할 수 있었지만,  메소드형 async Generator는 인자와 지역변수뿐만 아니라, 변경되는 속성을 this라는 키워드를 사용하여 이용할 수 있게 된다. 

전기 바인딩: 생성 당시의 바인딩.(인자와 지역변수)가 생성 시점에 고정됨

후기 바인딩: 호출 되는 시점에 따라서 다른 value를 생성시킬 수 있게 됨



````javascript
const start = function*(url){yield "load start";};
const end = function*(url){yield "load end";};
const urls = async function*(...urls) {
    const r = [];
    for(const u of urls.map(url)) r.push((await u.next()).value);
    yield r;
}
const render = async function(...aIters) {
    for await(const json of dataLoader(...aIters) console.log)
}
render(start(), urls(url("1.json"), url("2.json")), url("3.json"), end()); 
````



### Async Iterator Class

```javascript
const AIter = class {
	update(v){}
    async *load(){throw "override";}
}

const Url = class extends AIter {
    private url, opt;
constructor(u, opt) {
    super();
    this.url = u;
    this.opt = opt;

	}
	update(json){if(json) this.opt.body = JSON.stringfy(json);}
	async *load() {
        console.log("body", this.opt.body);
        yield await(await fetch(this.url, this.opt)).json();
    }
}

const Start = class extends AIter {
    async* load(){yield "load start";}
}
const End = class extends AIter {
    async* load(){yield "load end";}
}
const START = new Start();
const END = new End();

const dataLoader = async function*(...aIters) {
    let prev;
    for(const iter of aIters) {
        iter.update(prev);
        prev = (await iter.load().next()).value;
        yield prev;
    }
};

const render = async function(...aIters) {
    for await(const json of dataLoader(...aIters)) {
        console.log(json);
    }
}
```