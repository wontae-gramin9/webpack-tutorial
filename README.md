# Webpack tutorial

### Modularity achieving의 역사

1. 파일을 여러개로 나눔. modularity는 가지고 있지만 네트워크 요청 수가 많아지고 import 순서가 망가지면 동작하지 않음
2. 하나의 엄청난 js, css, html파일을 만들어서 네트워크 요청 횟수를 줄였지만, 디버깅이 엄청나게 어려워짐
3. commonJs의 도입으로 require(path)로 modularity를 달성함. 그러나 browser는 commonJs(require)를 이해하지 못하므로 Browserify, RequireJs같은 별도 라이브러리가 필요했음
4. 웹팩 등장

   - commonJs, ES6 호환
   - Js뿐만 아니라 css, images, fonts import 가능
   - dependency graph로 파일간의 dependency를 파악
   - removing unused code in a library, 그리고 필요한 코드만 가져옴
   - removing the duplication of code
   - Fetching modules at runtime

### Dependency Graph

많은 js, css, images, fonts파일이 있다고 해보자.

- Entry file

  - Normally index.js, bootstraping all application
    - 만약 server를 만든다면, index.js에 db connection도 있을거고 서버 시작도 있을 것
    - 만약 클라이언트를 만든다면, 홈페이지겠고 다른 모든 dependency들을 로드하겠지.
  - index.js의 import, require구문에 따라 필요한 파일들을 모두 fetch함
    - 재귀식으로 internal 디펜던시가 있으면 전부 가져와서 index.js에 pulling함

- 만약 아무런 디펜던시가 없는 파일들이 있다면, 그 파일을 번들링하지 않는다
- 번들링하면 아웃풋을 받게될것
  - js, css를 하나만 빌드해도 되고, 여러개 나눠서 빌드해도 된다.
  - 빌드가 끝나면, index.html에서 웹팩 아웃풋만 import하게 된다.
