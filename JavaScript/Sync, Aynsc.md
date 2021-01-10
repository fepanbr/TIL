## Sync, Aynsc



### Sync

서브루틴이 즉시 값을 반환함. 함수가 즉시 리턴하면 sync

```javascript
const double = v => v*2;
console.log(double(2));
```



#### BLOCK 즉시 플로우제어권을 반환하지 않음.

#### NONBLOCK이 가능





### Async

서브루틴이 콜백을 통해 값을 반환함. 인자로 콜백함수 넘겼나의 유무

```javascript
const double = (v, f) => f(v*2);
double(2, console.log); // 4
```

block

```javascript
  const sum = (n, f) => {
    let sum = 0;
    for(let i = 1; i <= n; i++) sum += i;
    return f(sum);
};
sum(10, console.log);
console.log(123);
```

non Block

```javascript
const sum = (n, f) => {
    requestAnimationFrame(_ => {
        let sum = 0;
        for(let i = 1; i <= n; i++) sum +=i;
        f(sum);
    });
};
```

 