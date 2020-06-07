## Spring 5일차



자동 주입할 때 이름이 같으면 어떤 bean을 이용해야하는지 모를 때가 있음.

이 때 쓰는게, Qualifier



@AutoWired()에 required=false 속성을 주게 되면 자동 주입시, 그 객체가 없더라도 Exception이 발생하지 않는다.



@Inject도 자동 주입가능하다.

자동 주입시 구체적으로 명시 되지않았을 때, 그 객체를 직접 명시해주는 방법이 @Inject에도 있다.

@Inject에 @Named(value="wordDao1") 과 같은 이름을 직접 명시해주는 방법이 있다.