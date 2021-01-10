### Functions as First Order Objects



```dart
void main() {
    Car myCar = Car(drive: slowDrive);
}

class Car {
    Car({this.drive});
    
    Function drive;
}

void slowDrive() {
    print('driving slowly');
}

void fastDrive() {
    print('driving super fast');
}
```





