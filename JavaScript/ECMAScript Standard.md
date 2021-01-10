JavaScript Pipeline

Code: TypeScript, Dart, Kotlin

Transpiler 각 언어를 자바스크립트로 변경시켜줌. 

Packaging: webpack



ES11을 이용 (2020)



### ECMAScript Standard

매년 상반기 새로운 버전을 출시함

ES6이후 급격한 언어의 변화를 지양하고 점진적인 버전업을 진행

새롭게 반영될 내용은 Stage0~3까지 단계별 승격을 통해 정식 반영시 Stage4가 됨.



TC39위원회에서 회의를 통해 결정되며 위원회는 다양한 업계와 관계자로 구성됨

실제 각 제안의 담당자가 구글 관련 개발자인 경우가 많음.

Stage4기준 보다 구글이 원하는 순서대로 크롬에 빨리 반영되는 경우가 많음.

크롬위주임.



#### ES6

- **Class**, Object Literal

- Arrow
- **Iterator, Generator, For of**
- const, let
- destructuring, rest, spread
- Template string
- Symbol, Promise, Map, Set, WeakMap, WeakSet, Proxy, Reflect



#### ES7~10, Stage3

- 7 - 중첩된 rest해제 const [a, ...[b, ...c]] = [1,2,3,4] (a=1, b=2, c = [3,4])
- 8 - **async/await, shared memory, atomics**

>javascript 워커 쓰레드
>
>멀티쓰레드 패턴중 워커 쓰레드 패턴: 컨텍스트 한개만 가질 수 있다. 동기화 문제가 일어나지 않는다.
>
>메인 쓰레드 값을 쉐어함. (shared memory) arrayBuffer
>
>atomics: lock기능 shared할 때, 문제 안생기게.

- 9 - object 해체, **asynchronous iterators**

>  asynchronous iterators: 비동기 로직을 제너레이터스럽게 사용함.

- 10 - optional catch 

- BigInt, globalThis, **top level await**, class field, private feild=> 이미 크롬에서 반영중임/method
- optional chaining, nullish coalescing, WeakReference



javascript 어렵다!!!!!



## Program

Language code === Lint & IDE

Machine language === Compile

Run === Runtime



ES2020, TypeScript...		Lint & IDE

Transpiler							Compile

File & deploy



Browser load				Browser Compile

Browser parsing

Run								Runtime

Browser close



## Runtime

Runtime Execution



loading

instruction fetch & decoding			=> CPU가 해석할 수 있는 instruction을 메모리에 적재 & decoding





### Runtime Details

essential definition loading: 언어에서 지정한 것

vtable mapping: 가상메모리 vtable



