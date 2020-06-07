# spring 4일차(스프링 설정 파일 분리)



### 스프링 설정 파일 분리



```java
String[] appCtxs = {"classpath:appCtx1.xml", "classpath:appCtx2.xml", "classpath:appCtx3.xml"};
GenericXmlApplicationContext(appCtxs);
```



```xml
<!-- 하나의 xml 파일을 이용하여 appCtx2, appCtx3을 추가하기 -->

<import resource="classpath:appCtx2.xml"></import>
<import resource="classpath:appCtx3.xml"></import>
```



> 주로 스프링 설정 파일은 **기능**별로 설정파일을 나눈다.



### Bean의 범위



#### 싱글톤(Singleton)

스프링 컨테이너에서 생성된 빈(Bean) 객체의 경우 동일한 타입에 대해서는 기본적으로 한 개만 생성이 되며, getBean() 메소드로 호출될 때 동일한 객체가 반환 된다.



#### 프로토타입( Prototype )

싱글톤 범위와 반대의 개념도 있는데 이를 프로토타입(Prototype) 범위라고 한다. 프로토타입의 경우 개발자는 별도로 설정을 해줘야 하는데, 스프링 설정 파일에서 빈(Bean)객체를 정의할 때, scope속성을 명시해 주면 된다.