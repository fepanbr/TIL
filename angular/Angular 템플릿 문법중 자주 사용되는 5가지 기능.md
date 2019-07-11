## Angular 템플릿 문법중 자주 사용되는 5가지 기능

- `*ngFor`

- `*ngIf`

- 문자열 바인딩(Interpolation) `{{ }}`

- 프로퍼티 바인딩 `[ ]`

- 이벤트 바인딩 `( )`

  ***

여기서 나오는 바인딩(binding)의 의미는 뭘까?

#### 1. 데이터 바인딩이란?

구조화된 웹 애플리케이션을 구축하기 위해서는 View와 model을 분리가 필수적이다. 하지만 분리된 View와 model은 유기적으로 동작하여야 한다. 그래서 data binding이 이것을 가능하게 한다.

데이터 바인딩(data binding)은 View와 Model을 하나로 연결하는 것을 의미한다. Angular의 데이터 바인딩은 템플릿(View)과 컴포넌트 클래스의 데이터(Model)을 하나로 묶어 유기적으로 동작하도록 하게 하는 것을 말한다. 

***

#### 2. 변화 감지

뷰와 모델의 동기화를 유지하기 위해 상태의 변화를 감지하고 이를 반영하는 것을 말한다. AngularJS는 양방향 바인딩과 단방향 바인딩을 지원한다. (양방향 템플릿 문법: ''[()]'' )

모델의 변화감지는 HTML요소가 아니므로 변화를 감지하지 못한다. 모델이 변경된다는 것은 컴포넌트 클래스의 **프로퍼티 값**이 변경되는 것이다.

```typescript
import { component } from '@angular/core'

@Component({
    selector: 'app-hello',
    template: `
		<h2> 안녕하세요 {{ name }}</h2>
		<input type="text" placeholer="이름을 입력하세요." 				#inputYourName>
		<button (click)="setName(inputYourName.value)">등록			</button>`,
    style: [`...`]
})
export class HelloComponent { 
	name: string;
    
    setName(name: string){
        this.name = name;
    }
}
```

