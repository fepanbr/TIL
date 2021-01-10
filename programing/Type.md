### Type

#### Type

- Role : 형을 통해 역할을 묘사함.
- Responseibility : 형을 통해 로직을 표현함.
- Message : 형을 통해 메세지를 공유함
- Protocol : 객체 간 계약을 형을 통해 공유함.



#### value = responsibility



Value Object

- 모든 필드가 불변 (`final Double amount`)
- 새로운 값을 리턴 (`new Money()`)



```java
public class Money {
    public static Money of(Double amount){return new Money(amount);}
    private final Double amount;
    Money(Double amount){this.amount = amount;}
    public Money minus(Money amount) {
        return new Money(this.amount > amount.amount ? this.amount - amount.amount : 0.0);
    }
    public Money multi(Double times) {
        return new Money(this.amount * time);
    }
    public Money plus(Money amount) {
        return new Money(this.amount + amount.amount);
    }
    public boolean greaterThen(Money amount) {
        return this.amount >= amount.amount;
    }
}
```



```java
public class Reservation {
    static final REservation NONE = new Reservation(null, null, null, 0);
    
   final Theater theater;
   final Movie movie;
	final Screening screening;
    final int count;
    
}
```



> trigger와 action 외부에서 제어하게 된다.
>
> 값 객체는 외부에 노출 되면 안된다.

