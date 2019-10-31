## JavaScript code 컨벤션 자동화

#### 코딩 컨벤션이란? 

**코딩 컨벤션**은 **읽고, 관리하기 쉬운 코드를 작성하기 위한 코딩 스타일 규약**이다. 



#### 코딩 컨벤션은 왜 필요한가?

여러 개발자가 협업해야하는 상황에서 일종의 규약이 있다면, **유지보수 및 가독성**이 좋아져, 협업이 쉬워진다. 특히, 자바스크립트의 경우 다른 언어의 비해 문법구조가 유연하기 때문에, 통일된 규약이 없다면 **오류를 찾기** 어렵게 된다.



## 자바스크립트에서 코드 컨벤션 자동화하기

Javascript에서는 *Husky, Lint-staged, Prettier*를 이용하여 코드 컨벤션을 자동화 할 수 있다.



#### Husky

````
npm install husky --save-dev
````

**깃 훗을 편하게 작성할 수 있게 도와주는 도구**이다. 



````javascript
{
    "script": {
        "precommit": "npm test",
        "prepush": "npm test",
    }
}
````

위와 같이 **package.json**에 작성하여 커밋 푸쉬 전에 할 작업을 설정할 수 있다.



#### Lint-staged

**staged도니 파일을 lint 해주는 도구**이다. Husky와 같이 쓰면 staged된 파일들에 대해서 특정 작업을 수행할 수 있다.

```javascript
{
    "scripts": {
    "precommit": "lint-staged"
  },
  "lint-staged": {
    "*.js": ["eslint --fix", "git add"]
  }
}
```

▲ 커밋하기 전에 모든 js파일에 대하여 lint를 수행하도록 설정



#### Prettier

**코드 컨벤션을 고쳐주는 도구**이다. es2017을 포함하여 JSX, typescript, flow를 지원하고, 심지어 *CSS, LESSS, SCSS* 까지 지원한다.





출처: http://guswnsxodlf.github.io/auto-js-code-convention 