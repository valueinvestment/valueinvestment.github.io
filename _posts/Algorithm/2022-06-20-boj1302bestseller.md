---
title:  "BOJ 1302 with js _ 미로 탐색 (Map)"
excerpt: "BOJ 1302"
toc: true
toc_sticky: true

categories:
  - 백준 알고리즘
tags:
  - [Algorithm, Coding Test, JS, Java Script, Baekjoon]
---  

## 1302 with Node.js _ 베스트샐러 ##

## 문제 ## 
> 김형택은 탑문고의 직원이다. 김형택은 계산대에서 계산을 하는 직원이다. 김형택은 그날 근무가 끝난 후에, 오늘 판매한 책의 제목을 보면서 가장 많이 팔린 책의 제목을 칠판에 써놓는 일도 같이 하고 있다.

>오늘 하루 동안 팔린 책의 제목이 입력으로 들어왔을 때, 가장 많이 팔린 책의 제목을 출력하는 프로그램을 작성하시오.

## 입력 ## 
> 첫째 줄에 오늘 하루 동안 팔린 책의 개수 N이 주어진다. 이 값은 1,000보다 작거나 같은 자연수이다. 둘째부터 N개의 줄에 책의 제목이 입력으로 들어온다. 책의 제목의 길이는 50보다 작거나 같고, 알파벳 소문자로만 이루어져 있다.

## 출력 ##
> 첫째 줄에 가장 많이 팔린 책의 제목을 출력한다. 만약 가장 많이 팔린 책이 여러 개일 경우에는 사전 순으로 가장 앞서는 제목을 출력한다.

## 정답 코드 ##
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

let count = +input();
let map = new Map();

for(let i = 0; i < count; i++ ){
  const inputName = input();
  const beforeCount = map.get(inputName) ?? 0;
  map.set(inputName, beforeCount + 1); // map (key,value) 형식으로 이름 별 출현한 숫자 저장 
}

let result = '';
let max = 0;
map.forEach((value, key) =>  { //한 번 순회하면서 최대 값 찾아줌
  if(value > max){
    max = value;
    result = key;
  } 

  if(value == max && result > key) {
    result = key;
  }
})

console.log(result); // 결과 값 출력
```
## 살펴보아야 할 점 ##
### Map함수 이용 ### 
> <a href="https://valueinvestment.github.io/%EB%B0%B1%EC%A4%80%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98/boj1620pocketmon/" target="_blank">이전 문제풀이 참조 </a>

> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map" target="_blank">Map 문서</a>
