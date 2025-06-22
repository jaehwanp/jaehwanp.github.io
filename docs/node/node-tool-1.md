---
layout: default
title: '[Node.js] 개발시 필요한 사항'
parent: node
---

# npm


## node-module 폴더 없어졌을 떄
 - git에서 불러온 후
```sh
node install
```


## 서버 자동 시작
```s
# package.json

# 서버 자동 재시작
npm install nodemon --save-dev

# 전역 설치
npm i nodemon --global

# 서버 시작
nodemon index.js
```



```json
// ^ 모든 패치와 모든 릴리스를 수용
  "dependencies": {
    "slugify": "^1.6.6"
  },
// 패치된 버전만 수용
"dependencies": {
    "slugify": "~1.6.6"
  },
```