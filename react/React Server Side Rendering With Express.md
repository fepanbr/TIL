## React Server Side Rendering With Express



이 글은 [React Server Side Rendering With Express](https://medium.com/@danlegion/react-server-side-rendering-with-express-b6faf56ce22)을 따라하면 작성하였습니다.



### 들어가며

React Server Side Rendering은  ExpressJs와 같은 서버에서 React App을 랜더링 할 수 있도록 합니다. 이러한 React SSR 방식은 SEO와 초기 페이지 로드와 같은 것에 이점이 있습니다. 



### 미리 준비할 사항

- Vs code
- React
- NodeJs
- ExpressJs
- ES6



우선 디렉토리에 다음과 같은 코드를 실행하자.

```bash
npm init
```



서버를 만들기 위해 **ExpressJs**를 사용한다. 그러므로 ExpressJs 모듈을 설치하자.

```bash
npm install express
```



그리고 ES6를 사용할 것이다. 그래서 코드를 transpile 하기 위해 **Babel**이 필요하다. 그리고 Babel은 production release에 필요한 것이 아니기에 development에 의존성을 추가한다. 

```bash
npm install --save-dev @babel/cli @babel/core @babel/node @babel/plugin-proposal-class-properties @babel/plugin-transform-runtime @babel/polyfill @babel/preset-env
```

간단히 설명하자면

- <u>@babel/cli</u> : command line에서 컴파일이 가능하게 한다.
- <u>@babel/core</u> : 코어 런타임
- <u>@babel/node</u> : node 대신에 babel을 사용할 수 있게 한다.
- <u>@babel/plugin-proposal-class-properties</u> : transpile classes

