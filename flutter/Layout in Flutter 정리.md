## Layout in Flutter



> 이 글은 [Layout in Flutter](https://flutter.dev/docs/development/ui/layout) 을 공부하며 정리한 글입니다.



### 이 글의 Point

Flutter의 레이아웃의 포인트는 3가지입니다.

1. 플러터의 위젯(Widget)은 UI를 빌드하는 **Class**입니다.
2. 위젯은 레이아웃(Layout)이나 UI요소로 사용됩니다.
3. 복잡한 레이아웃(Layout)은 **간단한 위젯**으로 구성합니다.



플러터는 거의 모든것이 위젯으로 되어있습니다. 레이아웃 모델 또한 위젯입니다.

(Row, Column, grid...) 



### 위젯 배치하기



#### 1. 우선 위젯을 선택하자

여러가지 위젯들(Text, Image, Icon...)을 선택하자.



#### 2. 위젯들을 만든다.

Text 위젯

````dart
Text("Hello World"),
````

Image 위젯

````dart
Image.asset('images/lake.jpg', fit: Boxfit.cover),
````

Icon 위젯

````dart
Icon(Icons.stars, color: Colors.red[500]),
````



#### 3. 레이아웃 위젯에 위젯들을 추가하기

레이아웃 위젯들은 `child`나 `children` 와 같은 property가 있습니다.

이 property들에 위젯들을 추가합니다.

ex) `Center` 위젯 예제

```dart
Center(
	child: Text("Hello World"),
)
```



### 4. 레이아웃 위젯을 페이지에 추가하기

플러터 앱의 대부분에 위젯은 build()메소드를 가지고 있습니다. 이 메소드를 이용하여 return이나 instantiating하여 해당 위젯을 보여줍니다.



#### Material Apps

Material app은 기본적인 배너, 배경색,  drawer, snack bars, button과 같은 API를 가지고 있는 위젯입니다. 이를 이용하여 Material 디자인에 기반한 위젯을 만들 수 있습니다.