## JDK 설정하기

> 원하는 버전의 JDK를 다운받아야 합니다. 그러기 위해서는 Oracle에 회원 가입이 되어있어야 하기에 회원가입을 먼저 하시고 진행하시길 바랍니다.

원하는 버전의 JDK를 받은 후 설치합니다. 설치시 따로 누르실건 없습니다. '**다음***'만 누르시길 바랍니다. 
보통 설치 후, 아래와 같은 경로에 설치 됩니다.

```
C:\Program Files\Java
```

`jdk-11.0.5` 저는  JDK 11을 받았습니다. 그래서 이와 같은 폴더가 생성되어있었습니다. 그리고 `jdk-11.0.5` 이 폴더의 경로를 복사해 둡니다.

그리고 나서 내PC -> 마우스 오른쪽 클릭 -> 속성 -> 고급 시스템 설정 -> 고급탭 -> 환경 변수 를 클릭합니다.
![환경변수1.png](https://images.velog.io/post-images/fepanbr/8aad08c0-fef1-11e9-84b5-d176537669aa/환경변수1.png)
- 위의 화면에서 '새로만들기' 클릭 후 

![환경변수2.png](https://images.velog.io/post-images/fepanbr/b7ec4940-fef1-11e9-abd7-69b6e89bd111/환경변수2.png)

- 위와 같이 변수 이름 = **"JAVA_HOME"**, 변수 값 = **"경로"** 로 저장합니다.


![환경변수3.png](https://images.velog.io/post-images/fepanbr/e56a1960-fef1-11e9-9d10-c3f6d9f9dfb8/환경변수3.png)

- 그 이후 시스템 변수에서 'Path'를 찾아 편집버튼을 누르고


![환경변수4.png](https://images.velog.io/post-images/fepanbr/f29d9da0-fef1-11e9-9d10-c3f6d9f9dfb8/환경변수4.png)

- 새로만들기를 눌러 **%JAVA_HOME%\bin** 을 입력하고 저장합니다.


- 마지막으로 환경 변수가 잘 설정 되었는지 확인하기 위해 명령프롬프트 창(cmd)을 열고 **'javac -version'**을 입력하여 JAVA 버전을 확인합니다.