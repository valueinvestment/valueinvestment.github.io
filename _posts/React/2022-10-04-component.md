---
title:  "[React를 다루는 기술] 3장 - Component "
excerpt: ""
toc: true
toc_sticky: true

categories:
  - React
tags:
  - [React, JS, Java Script, Study]
---  

## 컴포넌트
- 단순한 템플릿 이상
- 데이터가 주어졌을 때 이에 맞추어 UI개발
- 라이프사이클 API 적용 가능

1. 클래스형 컴포넌트
- state 기능, 라이프사이클 기능, 임의 메서드 정의 가능
- render() 함수 호출을 통해 렌더링 (JSX 반환)

2. 함수형 컴포넌트
- state, 라이플사이클 API 사용 불가능 -> Hooks 기능으로 해결
- 선언하기 용이, 메모리 자원 효율성, 결과물의 파일 크기 감소

## 컴포넌트 생성
```jsx
import React from 'react';

const NewComponent = () => {
    return <div>Hello React Component!</div>;
};

export default NewComponent;
```

1. ES6의 화살표 함수
- 함수를 표현하는 새로운 방식
- 주로 함수를 파라미터로 전달할 때 유용
- this 비교
  - function : 자신이 종속된 객체의 this를 가리킴
  - 화살표 함수 : 자신이 종속된 인스턴스의 this를 가리킴

2. 모듈 내보내기, 불러오기
- 내보내기 ( exprot )
  - 다른 파일에서 import 할 때 불러오도록 설정 (default로 하나만 선언도 가능)
- 불러오기 ( import )
  - import App from './App';

## props
- props는 불러오는 상위 컴포넌트에서 넣어 줄 수 있다.
- 받아오는 컴포넌트는 인자에 props를 넣고 {props.name}을 활용하여 쓸 수 있다.

```jsx
//선언
import MyComponent from './MyComponent'
const App = () =>{
    return <MyComponent name="React">
}

// 사용
const MyComponent = (props) =>{
    return <div>안녕하세요 제 이름은 {props.name}입니다.</div>
}
```

- 받아오는 쪽에 "Component 이름".defaultProps = {name:"초기값"}으로 설정을 줄 수 있다.
```jsx
const MyComponent = (props) => {
    ...
}

MyComponent.defaultProps = {
    name : '기본 이름'
}
```

- innerText는 props.children으로 접근할 수 있다.
```jsx
<부모 컴포넌트>
const App = () =>{
    // 태그 사이의 값 '리액트'
    return <MyComponent>리액트</MyComponent>
}

<자식 컴포넌트>
const MyComponent = (props) =>{
    return <div>children 값은 {props.children}</div>
}
```

- proptypes를 사용하면 props의 타입을 강제할 수 있다. (다른 타입이면 경고)

```jsx
MyComponent.propTypes ={
    favoritNumber : PropTypes.number.isRequired
}
```

## state
### props와 state의 차이점
- props는 부모 컴포넌트가 설정하는 값으로 읽기 전용이다.
- state는 컴포넌트 내부에서도 바뀔 수 있는 값이다. 상태 관리에 용이함

### 클래스형 컴포넌트의 state

```jsx
import React, {Component} from 'react';

class Counter extends Component {
    constructor(props) {
        super(props);
        this.state = {
            number: 0,
        };
    }

    //  state = {
    //     number: 0,
    // }; 이런식으로 간단히 사용하기도 한다.

    render() {
        const {number} = this.state;
        return (
            <div>
                <h1>{number}</h1>
                <button
                    onClick={() => {
                        this.setState({number: number + 1});
                    }}
                >
                    +1
                </button>
            </div>
        );
    }
}

export default Counter;
```

- 컴포넌트에 state 를 설정할 때는, constructor 메소드를 작성하여 설정한다. 이는 컴포넌트의 생성자 메소드로, 반드시 super(props) 를 호출하여, 리액트 Component 클래스가 지닌 생성자 함수를 호출해 주어야한다.

- this.state 값에 초기값을 설정해주는데, 컴포넌트의 state 는 객체 형식이어야 한다.

- render 함수에서 현재 state 를 조회할 때는 this.state 를 조회하면 된다. 그리고 button 의 onClick 이라는 값을 props 로 넣어주는데, 이는 버튼을 클릭할때 호출 시킬 함수를 설정한다. (이벤트)

- 이벤트로 설정할 함수를 화살표 함수 문법을 사용해서 넣어주었다.

### 함수형 컴포넌트의 state
```jsx
import React, {useState} from 'react';

const Say = () => {
    const [message, setMessage] = useState(''); // hook을 이용하여 state 세팅
    const onClickEnter = () => setMessage('Hi!');
    const onClickLeave = () => setMessage('Bye!');

    return (
        <div>
            <button onClick={onClickEnter}>Enter</button>
            <button onClick={onClickLeave}>Exit</button>
            <h1>{message}</h1>
        </div>
    );
};

export default Say;
```

### state를 사용할 때 주의사항
- state 값을 바꿀 때 세터 함수를 사용해야 한다. 직접적으로 바꾸면 안됨.
- 배열이나 객체를 업데이트 하는 과정
  - 배열, 객체 사본을 만든다. ( spread 연산자 )
  - 사본에 값을 업데이트 한 후 사본의 상태를 setState, 세터 함수를 이용해 업데이트 ( 배열의 내장함수들. map, filter ..)

```jsx
  const array = [
      {id : 1, value : true},
      {id : 2, value : false},
      {id : 3, value : true},
  ]
  let nextArray = array.concat({id:4})          // id가 4인 객체 추가
    nextArray.filter(item => item.id !== 2)     // id가 2인 객체 제거
    nextArray.map(item => item.id === 1 ? {...item, value:false})
    // id가 1인 객체 값을 false로 변경
```
