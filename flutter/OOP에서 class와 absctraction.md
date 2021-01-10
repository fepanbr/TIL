클래스



클래스는 객체이다

클래스는 blueprint 역할을 한다.



클래스 구성조건

1. 프로퍼티 (= chareteristic)
2. 메소드



```dart
class Car {
    int numberOfDoors = 5;
    
    void drive() {
		print('wheels start turning');
    }
}
```

위의 경우는 `numberOfDoors`는 프로퍼티이고, `drive()`는 메소드이다.

class안에 있는 함수는 메소드라고 부른다.



클래스 생성

```dart
Car myCar = Car();
```



Constructor

다트에서 Constructor 선언 방법: 동일한 이름으로 선언

```dart
class Human {
	double height;
    int age = 0;
    
    Human({double startingHeight}) {		// class Name과 동일하게
        height = startHeight;
    }
}
```



인스턴스 생성시, 생성자에 값을 전달해야한다.

```dart
void main() {
    
    Human jenny = Human(startingHeight: 15);		// height = 15;
    Human james = Human();			// error

}
```



메소드 선언



```dart
class Human {
	double height;
    int age = 0;
    
    Human({double startingHeight}) {		// class Name과 동일하게
        height = startHeight;
    }
    
    void talk(String whatToSay) {
        print(whatToSay);
    }
}
```



클래스는 왜 필요한가?



컴퓨터는 오직 스위치로 작동한다. on/off		=> 머신언어이다.

OOP가 나왔다.

모든것을 object관전에서 해석한다.



4가지의 개념이 필요하다



Abstraction

복잡한걸. 작은 조각으로 쪼개서 표현한다. 작업을 여러가지로 분리한다. 그러므로써 복잡도를 관리할 수 있다.



capsulate