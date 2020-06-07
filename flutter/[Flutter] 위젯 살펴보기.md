## [Flutter] 위젯 살펴보기



 Flutter의 widget은 React로부터 영감을 받았다. 그 중심 아이디어는 *out of widgets* 한 UI를 만드는 것이다.

widget에 상태가 변하면, 그 minimal한 변화를 감지하여 widget을 rebuild한다.



### Hello world

```dart
import 'package:flutter/material.dart';

void main() {
    runApp(
    	Center(
        	child: Text(
            	'Hello, world!',
                textDirection: TextDirection.ltr,
            ),
        ),
    );
}
```





