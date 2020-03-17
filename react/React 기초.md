## React 기초





### JSX 소개

````javascript
const element = <h1>Hello, world! </h1>
````

위의 문법은 *문자열, HTML* 이 아닙니다!

바로 *JSX*라고 불리우는 JavaScript를 확장한 문법입니다. 



#### JSX란?

> React에서는 이벤트가 처리되는 방식, 시간에 따라 state가 변하는 방식, 화면에 표시하는 방식 등 렌더링 로직이 본질적으로 다른 UI 로직과 연결된다는 사실을 받아드립니다.
>
> React는 별도의 파일에 마크업과 로직을 넣어 기술을 인위적으로 분리하는 대신, 둘 다 포함하는 "컴포넌트"라고 부르는 느슨하게 하게 연결된 유닛으로 **관심사를 분리**합니다.  -출처 : [React 공식 홈페이지 자습서](https://ko.reactjs.org/docs/introducing-jsx.html)

위에서 핵심은 **UI를 구성하는 로직과 마크업을 한 파일에 모은다**는 것입니다. 그리고 그 파일이 *컴포넌트(component)*라는 것입니다. 