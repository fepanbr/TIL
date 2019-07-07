## web-Application의 이해

#### web container에서 web-application등록하기

1. webApp directory에 application을 등록하는 방법

   **webapps**에 저장해두면. **tomcat**컨테이너에서 자동 실행하게 된다.

   기본적으로 서비스를 하기위해서 사용하기에 좋지만, 테스트하기 위해 사용하기에는 매번 갱신이 필요하여 불편하다.

   ***

2. **sever.xml**에 등록하기

   **sever.xml**에 **<Context>**태그를 등록하여 사용한다.

   **<Context>**태그 구성요소

   1. path : web application의 컨텍스트이름
   2. docBase : 컨텍스트에 대한 웹 애플리케이션의 실제 위치한 경로, 실제 웹 애플리케이션의 WEB-INF가 위치한 경로
   3. reloadable : 실행 중 소스 코드가 수정될 경우 바로 갱신할 지를 설정. **(true/false)**

