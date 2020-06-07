# 임시상태(ephemeral state)와 앱상태(app state)사이에 변이



> *이 문서는 앱의 상태, 임시 상태 그리고 각각을 Flutter앱에서 어떻게 관리할지를 소개한다.*



넓은 의미에서, 앱의 상태(state)는 앱이 실행중일 때, 메모리에 존재하는 모든 것이다. 즉, 앱의 assets, flutter 프레임워크에서 UI를 유지하기 위한 모든 변수, 애니메이션 상태, 텍스쳐, 폰트, 등등을 의미한다. 이 넓은 의미에서, 상태의 정의는 괜찮은 반면에, 앱을 구조화하는데는 유용하지 않다.



첫번째로,  너는 텍스처같은 일부 상태도 관리하지 않습니다. framework가 그것들을 관리한다. 그래서 좀더 상태에 대한 유용한 정의는 너가 UI를 리빌드(rebuild)하기 위한 어떤 data든지 state가 된다. 두번째로, 너가 직접 관리하고자 하는 상태는 두가지 타입으로 나눠질 수 있다. ephemeral state와 app state가 그것이다.





### Ephemeral state



임시 상태(Ephemeral state)는 주로 UI state, local state)라고 불리는데, 이것은 단일 위젯에 깔끔하게 포함되어있는 상태이다.