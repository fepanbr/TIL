### Subject와 Observable의 차이



>  *Subject는 Observable이면서 동시에 Observer이다. 즉, Observable역할을 하면서 동시에 Observer의 역할을 합니다. 그렇기 때문에 Observable이나 Subject 모두 subscribe가 가능합니다. 그리고 Subject는 **Multicast** 방식이고 Observable은 **Unicast**방식입니다. 즉, Multicast방식인 Subject는 **여러개**의 Observer가 Subscribe를 할 수 있고, Observable의 경우 **한 개**의 Observer만이 Subscribe가 가능합니다.*



또한, 둘의 중요한 차이는 Observable은 함수이기 때문에 어떠한 상태를 가지지 않기 때문에, 모든 새로운 Observe에 대해서 create 코드를 발생시킵니다. 이는 어떠한 Observer든 처음부터 시작하는 값을 받는다는 것입니다. 이에 달리, Subject는 Observer의 세부정보를 저장하고 코드를 한 번만 실행하고 몯느 관찰자에게 그 결과를 제공한다.





