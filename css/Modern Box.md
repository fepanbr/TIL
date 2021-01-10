## Modern Box



Fragment 영역은 border-box까지 이다.



box-shadow: border-box바깥에 그려지고, geometry를 차지하지 않는다.



relative는 normal-flow를 그리고 relative를 계산한다.

geometry를 설정하고 fragment를 그린다.



### OUTLINE

````html
<div style="background: brown; border-radius: 15px; outline: 10px solid brown; border: 1px dashed #fff; color: #fff; box-shadow: 0 0 0 10px brown"</div>
````



### POSITION 

offset은 조회전용.

offset을 가지고 다시 layout을 그려아하는 로직은 조심해야 한다.



#### OFFSET PARENT (기준점)

1. NULL

-  ROOT, HTML, BODY
- POSITION: FIXED
- OUT OF DOM TREE (FRAGMENT, REMOVE)



2. RECURSIVE SEARCH

- PARENT POSITION: FIXED = NULL
- PARENT.POSITION: !STATIC = OK;
- BODY = OK
- TD, TH, TABLE = OK
- PARENT.PARENT CONTINUE

> 결론: OFFSET PARENT는 오직 **absolute**와 **relative**밖에 되지 않는다.

> 즉, static안에 absolute를 넣기 위한 컨테이너로 relative를 사용한다.



#### OFFSET VALUE

offsetLeft

offsetTop

offsetWidth

offsetHeight



offsetScrollTop

offsetScrollLeft

offsetScrollWidth

offsetScrollHeight

> 실제 컨텐츠의 크기는 **offsetScroll**



#### Absolute

```html
<div style="width:200px; height: 200px; background:yellow;margin:100px">
    <div style="width:100px;height:100px;position:absolute;background:red"></div>
    <div style="width:100px;height:100px;position:absolute;background:blue;left:0"></div>
</div>
```



> 위 예제는 position absolute의 기본값은 static의 위치와 똑같은 기본값을 갖는다. (0,0)이 아니다. 

offsetParent를 기준으로 값을 계산한다.

> relative일 때, normal-flow로 그려졌을 때의 거리
>
> absolute일 때, offsetParent를 기준으로 거리를 계산
>
> static일 때, 무시한다.



