---
title:  "React Hook"
excerpt: "React Hook 소개"

categories:
  - React
tags:
  - React
---  

#React Hook

## Hook 소개
### Hook의 등장배경
> Component 간 상태 로직 재사용이 쉽도록 (계층의 변화 없이 상태관련 로직을 재사용)
>
> Class의 최적화와 최소화가 어렵다 판단 함수형 구조에서 Class의 장점인 state와 life cycle 기능을 쓰자!
>> Class의 최적화가 어려운 이유 : Ahead-of-time compilation( 미리 컴파일 해놓는 방식 ex_Svelte, Angular ) 방식의 Componemt folding에서 최적화에 문제가 되는 것을 발견 (오히려 느려짐) 
>
> 
### Hook의 개념
> 함수 컴포넌트에서 React state와 lifecycle features(생명 주기 기능)을 연동(hook into)할 수 있게 해주는 함수.

### 1. useState
 Class 구조의 this.state와 같은 역활
 
 ```jsx
// Hook 구조
import React, {useState} from 'react';

function Example() {
    const [count, setCount] = useState(0);
    const [author, setAuthor] = useState('valueInvestment'); //state 선언
    return (
        <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>
                Click me!!!
            </button>
            <p> Author : {author} </p>
        </div>    
    );
}

// Class 구조
class Example extends React.Component {
    constructor(props) {
        super(props);    
        this.state = {
            count: 0,
            author: 'valueInvestment'
        } // state 선언
    }
    
    render() {
        return (
         <div>
            <p>You clicked {this.state.count} times</p>
            <button onClick={() => this.setState({ count: this.state.count + 1 })}>
              Click me
            </button>
            <p> Author : {this.state.author} </p>
          </div>
        );   
    }
}   
``` 

### 2.useEffect
 함수 컴포넌트 내에서 side effects를 수행하는 기능을 연동 (Hook)
 React는 DOM을 바꾼 이후에 (매 rendering 이후에) effect 함수를 실행함.
 Effects는 컴포넌트 안에 선언되어있기 때문에 props와 state에 접근 가능 
 > side effects : React 컴포넌트 안에서 데이터를 가져오거나 구독하고, DOM을 직접 조작하는 동작.>

```jsx
// Hook 구조
import React, {useState, useEffect } from 'react';

function Example () {
    const [count, setCount] = useState(0);
    const [author, setAuthor] = useState('valueInvestment');
    // componentDidMount, componentDidUpdate와 비슷
    useEffect(() => {
    //브라우저 API를 이용해 문서의 타이틀을 업데이트합니다.
     document.title = `Count Example~ (count: ${count} times) by ${author}`;    
    });
    
    return (
    <div>
        <p>You clicked {count} times</p>
        <button onClick={() => setCount(count + 1)}>
            Click me!!!
        </button>
        <p> Author : {author} </p>
    </div>    
    );
}
// Class 구조
class Export extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            count: 0,
            author: "valueInvestment"
        }   
    }
    
    componentDidMount() {
        document.title = `Count Example~ (count: ${this.state.count} times) by ${this.state.author} `;
    }
    componentDidUpdate(prevProps, prevState, snapshot) {
        document.title = `Count Example~ (count: ${this.state.count} times) by ${this.state.author} `;
    }
    // 2개의 life cycle (생명주기) method에 같은 코드가 중복되어 들어감.

    render() {
        return (
         <div>
            <p>You clicked {this.state.count} times</p>
            <button onClick={() => this.setState({ count: this.state.count + 1 })}>
              Click me
            </button>
            <p> Author : {this.state.author} </p>
          </div>
        );   
    }
}
```