## CSSOM & VENDOR PREFIX

### CSS OBJECT MODEL

````html
<style i="s">
    .test{background:#ff0}
</style>
````

```javascript
const el = document.querySelector("#s");
const sheet = el.sheet;
const rules = sheet.cssRules;
const rule = rules[0];		// test{background:#ff0}
console.log(rule.selectorText);		// .test
console.log(rule.style.background);		//	#ff0
```



#### INSERT RULE

````javascript
const sheet = el.sheet;
const rules = sheet.cssRules;

sheet.insertRule('.red{background:red}', rules.length);
sheet.insertRule('.blue{background:blue}', rules.length); 
````



```javascript
document.styleSheets[0] // 기본적으로 내장되어 있는 객체 
// styleSheets의 순서에서 가장 마지막에 있는게 우선순위가 높다.
```



#### DELETE RULE

````javascript
const sheet = el.sheet;
const rules = sheet.cssRules;

sheet.insertRule('.red{background:red}', rules.length);
sheet.insertRule('.blue{background:blue}', rules.length); 

document.querySelector('.red').onclick=_=>{
    sheet.insertRule('.red{background:red}', rules.length);
    sheet.insertRule('.blue{background:blue}', rules.length);
}
document.querySelector('.blue').onclick=_=>{
    sheet.deleteRule(rule.length - 1);
}
````



> css를 통해서 이용해서 건드리면 dom을 조작하지 않기에 성능상에 이슈가 생기지 않는다.  또한, 빠르다.



### COMPATIBITY LIBRARY

#### - VENDOR PREFIX

- 실행도중에 확인하는 수 밖에 없다.

#### UNSUPPORTED PROPERTY

GRACEFUL FAIL

#### HIERARCHY OPTIMIZE

stylesheet가 여러개 있으면, 

SHEET.DISABLED = TRUE



#### CLASSES

- STYLE
- RULE
- CSS



STYLE

````javascript
const Style =(_=> {
    const prop = new Map, prefix = 'webkit,moz,ms,chrome,o,khtml'.split(',');
    const NONE = Symbol();
    const BASE = document.body.style;
    const getKey =key=> {
        if(prop.has(key)) return prop.get(key);
        if(key in BASE) prop.set(key, key);
        else if(!prefix.some(v=>{
            const newKey = v + key[0].toUpperCase() + k.substr(1);	// webkitBackground
            if(newKey in BASE){
                prop.set(key, newKey);
                key = newKey;
                return true;
            }else return false;
        })){
            prop.set(key, NONE);
            key = NONE; // 프리픽스로도 안되면 없는 키!
        }
    }
    return class {
        constructor(style){this._style = style;}
        get(key) {
            key = getKey(key);
            if(key === NONE) return null;
            return this._style[key];
        }
        set(key, val) {
            key = getKey(key);
            if(key !== NONE) this._style[key] = val;
            return this;
        }
    };
})();

const el = document.querySelector("#s");
const sheet = el.sheet;
const rules = sheet.cssRules;
const rule = rules[0];
const style = new Style(rule.style);

const style = new Style(rule.style);

style.set('borderRadius', '20px').set('boxShadow', '0 0 0 10px red');
````

`document.body.style`이 그 속성을 가지고 있다면, 그 속성은 가지고 있는거야. 라고 판단.



```javascript
const Rule = class {
    constructor(rule) {
        this._rule = rule;
        this._style = new Style(rule.style);
    }
    get(key) {
        return this._style.get(key);
    }
    set(key, val) {
        this._style.set(key, val);
        return this;
    }
}


const el = document.querySelector("#s");
const sheet = el.sheet;
const rules = sheet.cssRules;
const rule = new Rule(rules[0]);
rule.set('borderRadius', '20px').set('boxShadow', '0 0  0 10px red');

```



````javascript
cosnt Sheet = class {
    constructor(sheet) {
        this._sheet = sheet;
        this._rules = new Map;
    }
}
````



해결하고자 하는것

- VENDOR PREFIX: RUNTIME FETCH => body.style이용
- UNSUPPORTED : GRACEFUL FAIL



