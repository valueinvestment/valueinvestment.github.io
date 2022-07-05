---
title:  "BOJ 1182 with js _ 부분수열의 합 (Combination)"
excerpt: "BOJ 1182"
toc: true
toc_sticky: true

categories:
  - 백준 알고리즘
tags:
  - [Algorithm, Coding Test, JS, Java Script, Baekjoon]
---  

## 1182 with Node.js _ 부분수열의 합 (Combination) ##

## 문제 ## 
N개의 정수로 이루어진 수열이 있을 때, 크기가 양수인 부분수열 중에서 그 수열의 원소를 다 더한 값이 S가 되는 경우의 수를 구하는 프로그램을 작성하시오.

## 입력 ## 
> 첫째 줄에 정수의 개수를 나타내는 N과 정수 S가 주어진다. (1 ≤ N ≤ 20, |S| ≤ 1,000,000) 둘째 줄에 N개의 정수가 빈 칸을 사이에 두고 주어진다. 주어지는 정수의 절댓값은 100,000을 넘지 않는다.

## 출력 ##
> 첫째 줄에 합이 S가 되는 부분수열의 개수를 출력한다.

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

const [N, S] = input().split(' ').map(value => Number(value));
const list = input().split(' ').map(value => Number(value));
let result = 0;

function combination(array, lastIndex){
    const sum = array.reduce((a,b) => a+b, null);
    if(sum == S){
        result++;
    }
    
    for (let i = lastIndex; i < N; i ++){
        array.push(list[i]);
        combination(array, i + 1); // lastIndex 값을 이용하여 조합식 구현
        array.pop();
    }    
}

combination([],0);
console.log(result);
```
## 살펴보아야 할 점 ##
순열과는 다르게 중복을 포함하지 않으므로 방문을 체크해주지 않고 lastIndex를 이용해 순차적으로 방문하여 조합식처럼 경우의 수를 구할 수 있다.

## 순열과 조합 ##
<a href="https://aerocode.net/376" target="_blank">https://aerocode.net/376</a>


### 문제 링크 ### 
<a href="https://www.acmicpc.net/problem/1182" target="_blank">https://www.acmicpc.net/problem/1182 </a>