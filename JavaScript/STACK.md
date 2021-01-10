## STACK



### HTML PARSER

```html
A = <TAG>BODY</TAG>
B = <TAG/>
C = TEXT
BODY = (A | B | C)N
```



```html
<div>
    a
    <a>b</a>
    c
    <img/>
    d
</div>
```



```javascript
const parser = input => {
    input = input.trim();
    const result = {name: 'ROOT', type: 'node', children:[]};
    const stack = [{tag:result}];
    let curr, i = 0, j = input.length;
    while(curr = stack.pop()) {
        while(i < j) {
            
        }
    };
    return result;
}
```



```javascript
const parser = input => {
    input = input.trim();
    const result = {name:'ROOT', type: 'node', children: []};
    const stack = [{tag: result}];
    let curr, i = 0, j = result.length;
    while(curr = stack.pop()) {
        while(i < j) {
            const cursor = i;
            if(input[cursor] === '<') {
                // A, B의 경우
            } else {
                // C의 경우
            }
        }
    };
    return result;
}
```



```javascript
const parser = input => {
    input = input.trim();
    const result = {name:'ROOT', type: 'node', children: []};
    const stack = [{tag: result}];
    let curr, i = 0, j = result.length;
    while(curr = stack.pop()) {
        while(i < j) {
            const cursor = i;
            if(input[cursor] === '<') {
                // A, B의 경우
            } else {
                const idx = input.indexof('<', cursor);
                curr.tag.children.push({
                    type: 'text', text: input.substring(cursor, idx)
                });
                i = idx; 
            }
        }
    };
    return result;
}
```



```javascript
const textNode = (input, cursor, curr) => {
    const idx = input.indexof('<', cursor);
    curr.tag.children.push({
        type: 'text', text: input.substring(cursor, idx)
    });
    return idx;
};
```



```javascript
const textNode = (input, cursor, curr) => { ... };
const parser = input => {
    input = input.trim();
    const result = {name:'ROOT', type: 'node', children: []};
    const stack = [{tag: result}];
    let curr, i = 0, j = result.length;
    while(curr = stack.pop()) {
        while(i < j) {
            const cursor = i;
            if(input[cursor] === '<') {
                // A, B의 경우
            } else i = textNode(input, cursor, curr);
        }
    };
    return result;
}
```



```javascript
const textNode = (input, cursor, curr) => { ... };
const parser = input => {
    input = input.trim();
    const result = {name:'ROOT', type: 'node', children: []};
    const stack = [{tag: result}];
    let curr, i = 0, j = result.length;
    while(curr = stack.pop()) {
        while(i < j) {
            const cursor = i;
            if(input[cursor] === '<') {
                const idx = input.indexOf('>', cursor);
                i = idx + 1;
            } else i = textNode(input, cursor, curr);
        }
    };
    return result;
}
```



```javascript
const textNode = (input, cursor, curr) => { ... };
const parser = input => {
    input = input.trim();
    const result = {name:'ROOT', type: 'node', children: []};
    const stack = [{tag: result}];
    let curr, i = 0, j = result.length;
    while(curr = stack.pop()) {
        while(i < j) {
            const cursor = i;
            if(input[cursor] === '<') {
                const idx = input.indexOf('>', cursor);
                i = idx + 1;
                if(input[cursor + 1] === '/') {
                    
                }else {
                    let name, isClose;
                    if(input[idx - 1] === '/'){
                        name = input.substring(cursor + 1, idx - 1), isClose = true;
                    }else {
                        name = input.substring(cursor + 1, idx), isClose = true;
                    }
                }
            } else i = textNode(input, cursor, curr);
        }
    };
    return result;
}
```

