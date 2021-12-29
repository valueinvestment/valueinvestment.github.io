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
 
 ```jsx harmony
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
 > side effects : React 컴포넌트 안에서 데이터를 가져오거나 구독하고, DOM을 직접 조작하는 동작.
```jsx harmony
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
### '>' 을 사용

> MarkDown 문서에 익숙해지고 예쁘게 꾸미는 법을 알아가 보자
>>일단은 여러번 작성해본다.

### '*' 을 사용

* jekyll을 왜 추천하는 걸까? 사실 MarkDown 만으로 원하는 기능을 구현하기 힘들지 않나?
  * 물론 편리하지만 그것이 전부는 아닌것 같다  
 
### '-' 을 사용
- 정말 내가 원하는 Custom한 블로그를 한다면 HTML을 구현해야 하는 걸까?
  - 일단은 가보자 간단한 것부터 차근차근
  
### '+' 을 사용
+ 마크다운 언어를 사용하다보니 느낀것이
    + 이 정도로 사용할 용도면 굳이... GitHub Page를 쓰지 않고 일반 블로그 포스팅 하는 것이 좋을 것 같다.
        + 처음에 세팅하기 힘들기만하고....
        
         
### '``` ``' 을 사용 - **코드 인용**
```
mark down을 쓰면 뭐 확실히 편하긴 하네
코드도 넣기 편할 것 같고  
Editor 에서 보는 것처럼 보여주는 PlugIn등을 사용하면
이대로도 만족스럽게 사용할 것 같다.  
```

```javascript
var test = 'Test Java Script Format'
console.log(test)
```

**예쁘게 잘 나온다 쓰자!**

YFM에서 정의한 제목을 이중 괄호 구문으로 본문에 추가할 수 있다.  
이 글의 제목은 {{ page.title }}이고  
마지막으로 수정된 시간은 {{ page.last_modified_at }}이다.  