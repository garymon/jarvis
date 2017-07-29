## Scope
* 함수 단위의 렉시컬 스코프
* 블록단위 스코프 지원 X (util ES5) only use var
* let, const는 블록단위 스코프를 지원.

### use strict
* 함수나, 스크립트 최상단에 스트링으로 입력.

### eslint
* npm i eslint -D
* node_modules/.bin/eslint --init
** 이후에 .eslintrc.파일이 생성됨.
* package.json에 lint 명령어추가.
** "lint": "eslint src"
** src디렉토리

### webpack
* 디버깅을 위해서 source-map사용
** devtool: 'source-map'
