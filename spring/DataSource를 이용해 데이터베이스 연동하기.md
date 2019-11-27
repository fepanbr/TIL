# DataSource를 이용해 데이터베이스 연동하기



이전에 예제의 방식은 웹 애플리케이션이 필요할 때마다 데이터베이스를 연결하여야 하며, 이 과정은 오래걸립니다. 또한, 수십명 많게는 수백명이 동시에 접속하는 경우 앞의 방법을 이용하면 비효율적입니다.

그래서 **컨넥션 풀(connection pool)**를 이용합니다.



#### 컨넥션 풀(Connection pool) 

> 컨넥션 풀(Connection pool)은 미리 사전에 데이터베이스를 연결하여 유지하는 기술입니다.





#### 컨넥션 풀 동작 과정

1. 톰켓 컨테이너를 실행한 후 응용 프로그램을 실행합니다.
2. 톰캔 컨테이너 실행 시 ConnectionPool 객체를 생성합니다.
3. 생성된 컨넥션 객체는 DBMS와 연결합니다.
4. 데이터베이스와의 연동 작업이 필요할 경우 응용 프로그램은 ConnectionPool에서 제공하는 메서드를 호출하여 연동합니다.



#### JNDI

- 정의

> JNDI(Java Naming Directory Interface)란 필요한 자원을 키/값 쌍으로 저장한 후 필요할 때 키를 이용해 값을 얻는 방법입니다. 즉, 미리 접그할 자원에 키를 지정한 후 애플리케이션이 실행 중일 때 이 키를 이용해 자원에 접근해서 작업을 하게 됩니다.

- 사용 예

1. 웹 브라우저에서 name/value 쌍으로 전송한 후 getParameter(name)로 값을 가져올 때
2. 해쉬맵이나 해쉬 테이블
3. 도메인 네임으로 DNS서버에 요청할 경우 도메인 네임에 대한 IP주소를 가져올 때



#### DataSource 설정

- tomcat-dbcp.jar 다운로드 ( http://www.java2s.com/Code/Jar/t/Downloadtomcatdbcp7029jar.htm )
- WEB-INF -> lib에 jar파일 추가
- tomcat context.xml에 Resource 추가

```xml
<Resource
    	name="jdbc/oracle"
    	auth="Container"
    	type="javax.sql.DataSource"
    	dirverClassName="oracle.jdbc.OracleDriver"
    	url="jdbc:oracle:thin:@localhost:1521:XE"
    	username="fepanbr"
    	password="s5781037"
    	maxActive="50"
    	maxWait="-1" />
```









