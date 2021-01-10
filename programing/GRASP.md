#### Law of demeter 최소 지식

getter는 의존성을 만들게 된다.  안좋음

`classA.methodA`의 최대 지식 한계

- `classA`의 필드 객체
- `methodA`가 생성한 객체
- `methodA`의 인자로 넘어온 객체

다 알면 안된다. a.b.c.d X 하면 안됨.

train wreck이 일어남



객체가 제대로 작동하는가를 테스트하려면...

1. 객체통신망에서 테스트할 객체에게 메세지를 보낸 뒤
2. 그 객체가 이웃 객체에게 메세지를 보냈는지 확인
3. 통신한 이웃 객체를 조하면 된다.



>  mock객체를 활용하여 객체망을 검증함.



mockery(모조객체)와 mock(목객체)

테스트관리객체      테스트용 모의객체

mokery = 모조객체 = context



1. 필요한 목객체를 생성한다.

2. 테스트할 객체를 둘러싼 객체망을 구성한 뒤(DI)
3. 트리거가 되는 메세지를 일으켜
4. 각 목객체의 상태를 확인한다.





### GRASP

#### (패턴)

- 정보 담당자 Information Expert
- 소유권한 Creator
- 컨트롤러
- 낮은 연결
- 높은 응집도
- 간접 참조
- 다형성
- 순수 조립
- 변화 보호



#### Information Expert

해당 정보를 갖고 있는 객체에게 책임을 할당하라

객체의 본질과 데이터 은닉을 지킬 수 있는 패턴



#### Creator

객체 시스템의 이질적인 부분인 생성 시에도 정보전문가 패턴을 따르자.

어떤 객체가 대상을 포함하거나, 이용하거나, 부분으로 삼거나, 잘 알고 있다면 그 대상을 생성하게 시키자.



#### Controller

미디에이터 패턴의 설계판 확장으로 서브시스템으로 묶을 수 있다면 컨트롤러를 도입하자.



> 디자인패턴 외우고 => 객체지향 공부하고 => 다시 디자인패턴 이해



#### Low Coupling & High Cohesion

결합도를 낮추고 응집도를 높이는 패턴은 다른 양상으로 나타남. 결합도를 낮추려면 아는 객체 수를 줄여야 함. 하지만 더 중요한 것은 **단방향 의존성**임. 이에 비해 응집도를 높이려면 객체를 도출할 때부터 변화율을 고려해야 함.

> 양방향은 버그

> 양방향 참조를 단방향으로 바꾸려면 더 많은 형(type)이 필요하다.



변화 이유는 '한가지'로 결정됌.

객체의 변화율은 도메인에 의해 결정됨.



변화율에 따른 코드 관리. 형의 경계로 격리. 그리고 이것이 성립하려면, 단반향 의존성



#### Protected Variations

추상적인 수준에서 책임을 정의하여 다양한 구상가능성으로부터 사용할 모듈을 보호하라.



#### Polymorphism

전략패턴처럼 분기가 예상되는 책임이라면 다형성을 이용하라.



#### Pure Fabrication

공통된 기능이나 순수 기능적인 객체는 따로 모아서 작성한다.

디자인패턴 : 깊이 많이 세련되게 템플릿, 스티리지 패턴을 공부해야한다.

스티리지패턴을 템플릿 패턴으로, 템플릿 패턴에서 스티리지 패턴으로 변경 해야한다. 



#### Indirection(포인터의 포인터) OPEN CLOSED원칙

직접 참조관계를 피하고 중계 객체를 이용하면 개별 객체의 충격을 중계 객체에서 흡수할 수 있다. 



```java
public class TicketSeller {
    private TicketOffice ticketOffice;
    public void setTicketOffice(TicketOffice ticketOffcie) {
        this.ticketOffice = ticketOffice;
    }
    
    Reservation reserve(Customer customer, Theater theater, Movie movie, Screening screening, int count) {
        Reservation reservation = Reservation.NONE;
        Money price = movie.calculateFee(movie, screening, count);	// 잘못됨. movie에 대한 지식을 알아버림. 하단 처럼 변경
        // Money price = ticketOffice.calculateFee(movie, screening, count); // tickeOffice와의 중개역할만 하게 됨.
        if(customer.hasAmount(price)) {
            reservation = ticketOffice.reserve(theater, movie, screening, count);
            if(reservation != Reservation.NONE) customer.minusAmount(price);
        }
        return reservation;
    }
}
```