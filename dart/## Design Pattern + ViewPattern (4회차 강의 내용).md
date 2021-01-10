## Design Pattern + ViewPattern (4회차 강의 내용)



남이 의존하게 되는 메소드는 캡슐화한다. (제한된 권한만, 잘 모르게)

인자는 한개나 0개가 좋은 메소드



인자가 많이 노출될수록 외부 의존성 증가



```` javascript
const taskSort = {
    title: (a,b) => a.sortTitle(b),
    date:  (a,b) => a.sortDate(b),
}

// 잘못된 오브젝트
// task를 모두 알고있기 때문에 권한이 너무 높다 => 클래스로 변경
````



```javascript
const Sort = class {
	static title = (a, b) => a.sortTitle(b);
	static date = (a, b) => a.sortDate(b);
	sortTitle(task){throw 'override';}
	sortDate(task){throw 'override';}
}

const Task = class extends Sort{
    static get(title, date = null) {return new Task(title, date);}	// 팩토리함수
    // 생성자도 퍼블릭이다
    // 생성자에 대한 지식을 외부의 노출하지 않는 방법은 팩토리 함수를 이용.
    
    constructor(title, date) {
        if(!title) throw 'invalid title';
        this._title = title;
        this._date = date;
        this._isComplete = false;
    }
    
    isComplete(){return this._isComplete;}
    toggle(){this._isComplete = !this._isComplete;}
    sortTitle(task){return this._title > task._title;}
    sortDate(task){return this._date > task._date;}
}
```



미래에 변경 상황을 생각해보고, 밸런스를 유지하는게 중요.



```javascript
const TaskList = class{
    constructor(title) {
        if(!title) throw 'invalid title';
        this._title = title;
        this._list = [];
    }
    add(title, date){this._list.push(Task.get(title, date));} 
    // 엔트리 입구는 값으로 받고 나머지는 받으면 안된다.
    remove(task) {	// title, date로 받으면 안됌. 그래서 task 객체로 받음.
        // 만약에 값컨텍스트를 사용한다면, removeForTitle 이런식으로 구체화 필요.
        const list = this._list;
        if(list.includes(task)) list.splice(list.indexOf(task), 1);
    }
    byTitle(stateGroup = true){return this._getList(Sort.title, stateGroup);}
    byDate(stateGroup = true){return this._getList(Sort.date, stateGroup);}
}
```

> 값 컨텍스트와 객체 컨텍스트를 구분.

인자는 하나만, 그리고 메소드를 늘리는게 낫다.



```javascript
const Task = class{
    constructor(title, date) {
        this._title = title, this._date = date, this._isComplete = false;
        this._list = [];
    }
    isComplete(){...} toggle(){...}
    add(title, date = null){this._list.push(new Task(title, date));}
    remove(task) {
        const list = this._list;
        if(list.includes(task)) list.splice(list.indexOf(task), 1);
    }
  	
}
```





