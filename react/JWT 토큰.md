## JWT 토큰



### 1. 준비사항

- *babel*

- *jsonwebtoken*



### 2. Babel 설정

- npm init

```bash
npm init -y
```



- babel 모듈 설정

```bash
npm install @babel/node @babel/preset-env @babel/core
```



- babelrc파일 생성, index.js 생성 및 package.json 수정

```json
// .babelrc
{
	"presets": ["@babel/preset-env"]
}
```

````json
// package.json

"scripts": {
    "start": "babel-node index.js"
  }
````

```javascript
// index.js

//const express = require('express');   // ES5
import express from 'express';
```

