## block/non block



blocking을 억제하는게 목적.

업계 요구사항에 맞춰서 

  

```javascript
for(const i of (function*() {
    let i = 0;
    while(true) yield i++;
})()) console.log(i);
```

플랫폼의 안정성을 위해 블록 되는 시간이 길면 강제 종료 시킴.



### BLOCKING FUNCTION

점유하는 시간만큼 블록을 일으키는 함수

```javascript
const f = v -> {
    let i = 0;
    while(i++ < v);
	return i;
};
f(10);
f(100000000);
```



enterprise급은 enterprise급으로 세세하게 만든다.

그것의 기본은 blocking을 피한다.



예) 

- 배열순회, 정렬 - 배열크기에 따라
- DOM순회 - DOM의 하위구조에 따라
- 이미지프로세싱 - 이미지크기에 따라



### BLOCKING EVASION

독점적인 CPU점유로 인해 모든 동작이 정지됨.

타임아웃체크에 의해 프로그램이 강제 중단됨.

**블록킹의 조합을 예측할 수 없음.**



```javascript
const f = v -> other(some(v), v * 2);
f(10);
```



시분할 운영체제의 동시 실행

1,2,1,2,3,1,2,1



자바스크립트 쓰레드

MAIN UI THREAD 1 

BACKGROUND THREAD N

WEB WORKER THREAD => 별도의 THREAD를 만들 수 있다.



FRAME

프레임 - 명령큐

자바스크립트는 명령 큐에 저장한다.

나머지 쓰레드에서는 결과만 큐에 넣는다. 



MAIN UI THREAD에서는 읽기만 함.



### TIME SLICING

```javascript
const looper = (n, f, slice = 3) => {
    let limit = 0, i = 0;
    const runner = _=> {
        while(i < n) {
            if(limit++ < slice) f(i++);
            else{
                limit = 0;
                requestAnimationFrame(runner);
                break;
            }
        }
    };
    requestAnimationFrame(runner);
}
```

```javascript
const looper = (n, f, ms = 5000, i = 0) => {
    let old = performance.now(), curr;
    const runner = curr => {
        while(i < n) {
			if(curr - old < ms) f(i++);
            else {
                old = performance.now();
                requestAnimationFrame(runner);
                break;
            }
        }
    };
    requestionAnimationFrame(runner);
};
```



