Ternary Operator



```dart
void main() {
    bool jackBauerIsAwesome = true;
    
    if (jackBauerIsAwesome == true) {
        print("That's great!")
    } else {
        print("OH! no");
    }
    
    
    jackBauerIsAwesome == true ? print("That's great!") : print("Oh no");
    
    jackBauerIsAwesome ? print("That's great!") : print("Oh no");
    
}
```



위의 모든 문법이 같다.



```dart
void main() {
    int myAge = 12;
    
    bool canBuyAlcohl = myAge > 21 ? true : false;
}
```





