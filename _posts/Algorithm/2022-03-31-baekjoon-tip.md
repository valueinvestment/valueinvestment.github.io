---
title:  "Baek joon JS 코딩 테스트 꿀팁 java script"
excerpt: "js로 처음 코딩테스트 시작할 때 꿀팁"
toc: true
toc_sticky: true

categories:
  - 백준 알고리즘
tags:
  - [Algorithm, Coding Test, JS, Java Script, Baekjoon]
---  

## Java Script로 백준 알고리즘 테스트 시험보기 ##

## 입력과 출력 ##
- 백준 코딩 테스트는 입력과 출력으로 테스트를 하므로 stdin을 사용하여 입력받고 console.log 를 이용해 출력해야한다.
- 언어는 <strong>node.js </strong>를 고르도록하자. 제출 페이지에 언어 설정을 눌러 들어가 Drag & Drop 으로 설정이 가능하다
![언어설정](https://user-images.githubusercontent.com/78516146/161020862-f2dafff1-a45c-4002-a926-4df344dc29f1.png){: #magnific title=""}

## Parameter 입력받아 사용 ##

![예제](https://user-images.githubusercontent.com/78516146/161021824-32ca9de4-99dd-48d7-8ab3-1a3942d0c7c3.png){: #magnific title=""}
- 여기서 보이는 예제 입력 1의 10줄을 할당하여 계산해보겠다

```js
const fs = require("fs");
const stdin = (
  process.platform === "linux"
    ? fs.readFileSync("/dev/stdin").toString()
    : `` // 기본 입력값 설정 (백준 코딩테스트에서 비워놔도 무방하다.)
).split("\n");

const input = (() => {  //input()을 호출할 때마다 한줄씩 읽어온다.
  let line = 0;
  return () => stdin[line++];
})(); 

let result = 0;

for(let i = 0; i < 10; i++ ){
    result += solution(input()); // 10번 반복하여 input()을 불러왔으므로 예제 입력 10줄이 모두 입력되었다
}
console.log(result); // 결과 값 출력
```

### 온라인 테스트 사이트 ### 
<a href="https://www.jdoodle.com/execute-nodejs-online/" target="_blank">https://www.jdoodle.com/execute-nodejs-online/</a>
- 백준과 똑같은 코드로 테스트가 가능하다! 우측 하단 stdin Inputs로 parameter 입력이 가능 🤸‍
![jdoodle](https://user-images.githubusercontent.com/78516146/161024031-5dfd7107-362a-400a-9bd5-b49b4d370eda.png){: #magnific title=""}


