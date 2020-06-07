



# Spring 2일차



### DI(Dependency injection)

의존성 주입: 의존관계를 만드는 것을 의미.



applicationContext.xml은 스프링 설정 파일이다. 

이 안에 객체들을 선언하고, 각 객체들 간에 DI(의존주입)이 가능하다.



즉,

```java
Name name = new Name();
Age age = new Age();

Person person = new Person(name, age);	// Person은 Age와 name에 의존적이다.
```



위의 내용을 스프링설정파일인, applicationContext.xml로 표현하자면,



```xml
<beans>
	<bean id="person" class="package.ClassName">
    	<constructor-arg ref="name"></constructor-arg>
        <constructor-arg ref="age"></constructor-arg>
    </bean>
</bean>
```



