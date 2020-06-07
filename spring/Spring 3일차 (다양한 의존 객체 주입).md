# Spring 3일차 (다양한 의존 객체 주입)



## 1. setter 의존 주입

```java
public class DataBaseConnectionInfo {
    private String jdbcUrl;
    private String userId;
    private String userPw;
    
    public setJdbcUrl(String jdbcUrl) {
        this.jdbcUrl = jdbcUrl;
    }
    public setUserId(String userId) {
        this.userId = userId;
    }
    public setUserPw(String userPw) {
        this.userId = userPw;
    }

}
```



위와 같은 표현

```xml
<bean id="dataBaseConnectionInfoDev" class="packageName.ClassName">
	<property name="jdbcUrl" value="jdbc:~~~~"></property>
    <property name="userId" value="fepanbr"></property>
    <property name="userPw" value="dkfldnfl"></property>
</bean>
```



## 2. List 타입 의존 객체 주입

```java
public void setDevelopers(List<String> developers) {
    this.developers = developers;
}
```



위와 같은 표현

```xml
<property name="developers">
	<list>
    	<value>fepanbr</value>
        <value>fepanb2r</value>
        <value>fepanbr5</value>
    </list>
</property>
```



## 3. Map타입 객체 주입



```java
public void setAdministrators(Map<String, String> administrators) {
    this.administrators = administrators;
}
```



위와 같은 표현

```xml
<property name="administrators">
	<map>
    	<entry>
            <key>
                <value>fepanbr</value>
            </key>
            	<value>fepanbr@deerdwq.com</value>
        </entry>
        <entry>
        	...
        </entry>
    </map>
</property>
```

