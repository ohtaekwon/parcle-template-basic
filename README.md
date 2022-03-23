## RESET.CSS

#### [더 알아보기](https://www.jsdelivr.com/package/npm/reset-css)

- main.scss 가 실행되기 전에 동작해야 하기 때문에 위에 작성한다.

https://heropy.blog/css/images/logo.png


## ICO CONVERTER

[](https://www.icoconverter.com/)


## parcel plugin
https://www.npmjs.com/package/parcel-plugin-static-files-copy

- 개발의존성 모듈로 설치 
    - `npm i -D parcel-plugin-static-files-copy`

- `package.json` 파일에 아래 내용 추가
```json
  "statciFiles":{
    "staticPath":"static"
  }
```
- `static` 폴더를 생성 후, 안에다 파일을 이동


## 공급 업체 접두사(Vender Prefix)

- 터미널에서 `npm i -D postcss autoprefixer` 입력하면, `postcss` 와 `autoprefixer` 패키지가 설치된다.
    - 실행이 되지 않는다면, 하나씩 해도 된다.
    - `npm i -D postcss`
    - `npm i -D autoprefixer`
- 실행이 끝나면 `package.json` 파일에 아래의 코드 추가한다.
    ```json
    "browerslist" : [
      "> !%",
      "last 2 versions"
    ]
    ```
- `"> !%"` : 전세계의 점유율이 1%이상인 모든 브라우저
- `"last 2 versions"` : 해당하는브라우저의 마지막 2개 버전까지는 지원하겠다는 의미이다.
- 루트 경로에 `.postcssrc.js` 파일을 생성한다.
    - 뒤에 `rc`는 **Runtime configuration**의 약어로 붙은 파일은 구성 파일을 의미한다.
    - 파일이름 앞에 `.`가 붙는 것은 구성옵션이거나 숨김 파일을 의미한다.

#### `.postcssrc.js`

- 1) ESM - Javascript의 모듈개념이다.
    - `nodeJS` 에서는 ESM을 지원하지 않고 기본적으로 `commonJS`를 지원한다.
```js
// ESM
import

export
```

- 2) commonJS
```js
// ESM
// CommonJS

// import autoprefixer from 'autoprefixer'
const autoprefixer = require('autoprefixer') // 가져오기 

// export {
//   plugins:[
//     autoprefixer
//   ]
// }
module.exports = {
  plugins:[
    autoprefixer
  ]
}  // 내보내기
```
#### 주의 : 충돌 오류가 발생
- `autoprefixer`와 `postcss`의 버전으로 인한 충돌이 발생할 경우
- 둘 중 하나의 버전을 다운그레이드 하면 된다.
    - ex) `npm i -D autoprefixer@9` : `autoprefixer`를 9버전으로 설치



## babel

#### [더 알아보기](https://babeljs.io/)

- Babel은 ECMAScript 2015+ 코드를 이전 JavaScript 엔진에서 실행할 수 있는 이전 버전과 호환되는 JavaScript 버전으로 변환하는 데 주로 사용되는 무료 오픈 소스 JavaScript 트랜스컴파일러입니다.
- 즉, 자바스크립트 코드를 바벨을 통해서 구형 버전으로 변환시킬 수 있는 컴파일러이다.

#### 사용법

- 터미널에 `npm i -D @babel/core @babel/preset-env` 를 입력
    - `@babel/core` 패키지 설치
    - `@babel/preset-env` 패키지 설치
- 루트 경로에 `.babelrc.js` 파일 생성후 아래와 같이 코드 추가
    ```js
    module.exports = {
      presets:['@babel/preset-env']
    }
    ```
- `ES5` 의 문법으로 변경되어 브라우저에서 시작한다.
- 필요에 따라서, `package.json` 파일에 아래 내용 추가
    ```js
    "browerslist": [
      "> !%",
      "last 2 versions"
    ]
    ```
- 바벨에서는 `async` , `await` 문법은 기본설정만으로는 제공하고 있지 않다. 
- 따라서, 터미널에서 `npm i -D @babel/plugin-transform-runtime` 입력한다.
- `.babelrc.js` 파일에서 아래 내용을 추가한다.
    ```js
    pligins: [
      ['@babel/plugin-transform-runtime']
    ]
    ```
- 이제 `async` , `await` 문법이 사용가능해진다.
- 비동기 문법이 실행이 된다.