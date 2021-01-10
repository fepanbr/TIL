### Enum



```dart
void main() {
    Car myCar = Car(carStyle: 2);		// 애매 모호 2가 뜻하는게 뭔지 모름.
    Car myCar = Car(carStyle: CarType.convertible);		// convertible이란걸 알 수 있음.
}


class Car {
    
    CarType carStyle;
    
    Car({this.carStyle});
}

enum CarType {
    hatch, SUV, convertible, coupe
}
```

