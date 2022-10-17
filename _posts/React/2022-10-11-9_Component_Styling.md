---
title: "[React를 다루는 기술] 9장 - 컴포넌트 스타이링"
excerpt: ""
toc: true
toc_sticky: true

categories:
  - React
tags:
  - [React, JS, Java Script, Study]
---

# 🎉 Component Styling

## 😉 CSS

### 🐱‍🐉 이름 짓는 규칙

- 컴포넌트를 스타일링하는 가장 기본적인 방식
- class name은 "컴포넌트 이름-클래스" 형태로 지어야 충돌이 나지 않는다

### 🐱‍🐉 CSS selector 활용

- 특정 클래스 내부에 있는 경우에만 스타일 적용하기
  - .App .logo 처럼 .App 클래스 내부에 .logo만 적용하게 만들기

## 😉 Sass 사용하기

- Syntactically Awesome Style Sheets
- 자주 사용되는 CSS 전처리기 중 하나로 확장된 CSS 문법을 사용하여 CSS 코드를 더욱 쉽게 작성할 수 있도록 해준다.
- .scss와 .sass의 두 가지 확장자 지원

```scss
// .sass
$font-stack: Helvetica, sans-serif
$primary-color: #333

body
  font: 100% $font-stack
  color: $primary-folor // 변수 사용

//.scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-folor;
}
```

- CSS selector 편리하게 사용

  - 클래스{} 안에 클래스 적용하면 동일한 기능.
  - SassComponet 클래스 안에 있는 .box 클래스 사용

```scss
.SassComponent{
    .box{
        ...
    }
}
// box 이면서 red 일때 ex)
.SassComponent{
    .box{
        &.red
    }
}
```

- mixin : 재사용되는 스타일 블록을 함수처럼 사용가능

  - @mixin 함수이름($파라미터){
    css 속성
    }

```scss
@mixin square($size) {
  $calculation: 32px * $size;
  width: $calculation;
  height: $calculation;
}
// 적용하기
&.red {
  @include square(1);
}
```

- 스타일 적용하는 JS에 import './SassComponent.scss'

## 😉 CSS Module

- 스타일을 작성할 때 CSS 클래스가 다른 CSS 클래스의 이름과 절대 충돌하지 않도록 파일마다 고유한 이름을 자동으로 생성해 주는 옵션
  - [파일 이름]\_[클래스 이름]\_\_[해시값] 형태
- .module.css 확장자로 파일을 저장하면 자동으로 CSS Module이 적용됨

```jsx
import React from "react";
import styles from "./CSSModule.module.css"; // scss 도 가능

// 1. css파일로 module 만들기
/* CSSModule.module.css -> CSSModule_wrapper__1dasg 이런 식으로 고유하게 생성됨
.wrapper{
    ...
}
:global .something{ 
    ...
}*/

/*
CSS Module이 아닌데 쓰는 방법

일반 파일 확장자 ( Module.css, Module.scss를 안쓴)
클래스 앞에 :local 붙이기 
*/

// 2. classnames로 css 클래스 조건부 설정하기
// import classNames from "classnames";

// 3. CSS 모듈과 같이 사용 : bind 함수를 사용하여 CSS Module의 styles.[클래스 이름]에서 styles.를 제거
// const cx = classNames.bind(styles)

export default function CSSModule() {
  // export default function CSSModule({highligted, theme) {
  return (
    <div className={`${styles.wrapper} ${styles.inverted}`}>
      {/*classnemes('one', {two: false})*/} // 결과값 one
      {/* <div className={classNames("MyComponent", { highlighted }, theme)}> */}
      {/* 이 경우 highlight가 props라면 true, false에 의해 보여짐 theme은 문자열이라 하면 내용 그대로 쓰면 적용됨 */}
      {/* <div className={`MyComponent ${theme} ${highlighted ? 'highlighted' : ''}`}> */}{" "}
      // class name을 안 쓸 경우
      {/* <div className={[styles.wrapper, styles.inverted].join(' ')}> */} //
      클래스 2개 이상 넣어야 할 떄
      {/* <div className={`${styles.wrapper} ${styles.inverted}`}> */} // 클래스
      2개 이상 넣어야 할 떄 Hi <span className="something">CSS Module</span> //
      global로 선언된 전역 스타일 그냥 문자열로 넣는다
      {/* bind 함수 이용 */}
      {/* <div className={cx("wrapper", "inverted")}></div> */}
    </div>
  );
}
```

## 😉 Styled-components

- 자바스크립트 파일 안에 스타일 선언하기 ( CSS-in-JS 방식 )
  - 컴포넌트 기반 개발 방법이 주류 각 컴포넌트에 HTML, CSS, JavaScript를 몽땅 때려 박는 패턴이 많이 사용
- Tagged Template Literals(ES6)을 사용해서 스타일 정의
  - 백틱(`)  을 사용하여 문자열과 변수를 함께 사용할 수 있어 문자열 처리에 유용한 기능, 함수 형태로도 사용 가능

```jsx
import styled from "styled-components";
import Button from "./Button";

styled.button`
  // <button> HTML 엘리먼트에 대한 스타일 정의
`;

styled(Button)`
  // <Button> React 컴포넌트에 스타일 정의
`;

const StyledButton = styled.button`
  // 고정 스타일링
  padding: 6px 12px;
  border-radius: 8px;
  font-size: 1rem;
  line-height: 1.5;
  border: 1px solid lightgray;
  color: gray;
  background: white;
`;

function Button({ children }) {
  return <StyledButton>{children}</StyledButton>;
}

const media = Object.keys(sizes).reduce((acc, label) => {
  acc[label] = (...args) => css`
    @media (max-width: ${sizes[label] / 16}em) {
      ${css(...args)};
    }
  `;
  return acc;
}, {});

const StyledButton = styled.button`
  // 가변 스타일링
  padding: 6px 12px;
  border-radius: 8px;
  font-size: 1rem;
  line-height: 1.5;
  border: 1px solid lightgray;

  color: ${(props) => props.color || "gray"};
  background: ${(props) => props.background || "white"};

  ${media.desktop`width: 768px`}
  ${media.tablet`width:100%`}
`;
/* @media (max-width: 1024px) {
  width: 768px;
}
@media (max-width: 768px) {
  width: 100%;
} */

function Button({ children, color, background }) {
  return (
    <StyledButton color={color} background={background} Î>
      {children}
    </StyledButton>
  );
}

import React from "react";
import styled, { css } from "styled-components";

const StyledButton = styled.button`
  // 가변 스타일링 2 바꾸고 싶은 속성이 여러개 일 경우
  padding: 6px 12px;
  border-radius: 8px;
  font-size: 1rem;
  line-height: 1.5;
  border: 1px solid lightgray;
  /* & 문자를 사용하여 Sass처럼 자기 자신 선택 가능 */
  &:hover {
    background: rgba(255, 255, 255, 0.9);
  }

  /* 다음 코드는 primary 값이 존재하는 경우 특정 스타일을 부여해 줍니다 */

  ${(props) =>
    props.primary &&
    css`
      color: white;
      background: navy;
      border-color: navy;
    `}
`;

function Button({ children, ...props }) {
  return <StyledButton {...props}>{children}</StyledButton>;
}
```

- 마운트 될때, 업데이트 될때 - 값이 없을 경우

  - useEffect(()⇒{})
  - 화면이 렌더링 된 이후 수행이 되며, 리 렌더링이 발생하는 경우 다시 수행이 된다

- 마운트 될 때만 쓰임 - 빈 배열 인경우

  - useEffect(()⇒{}, [])
  - 화면이 렌더링 된 이후에만 수행이 된다.

- 특정값이 업데이트 될 때만 실행 - 배열 값이 존재하는 경우

  - useEffect(()⇒{}, [값])
  - 화면이 렌더링 된 이후에 수행이 되고, ‘값’이 변경되었을 경우 해당 메서드가 수행이 된다.

- deps에 특정 값을 넣게 된다면 컴포넌트가 처음 마운트 될 때, 지정한 값이 바뀔 때, 언마운트 될 때, 값이 바뀌기 직전에 모두호출이 된다.

> 💡clean-up 함수

- Component의 unmount이전 / update직전에 어떠한 작업을 수행하고 싶다면 Clean-up함수를 반환해 주어야 한다.

  - unmount 될 때 : useEffect(func, [])
  - 특정값 update 직전 : useEffect(func, [특정값])

- clean-up함수를 사용하게되면, 작동 순서는
  - re-render -> 이전 effect clean-up -> effect

```jsx
useEffect(() => {
  console.log("일반 상황1 -> 마운트되어서 Info 컴포넌트가 보일 때");
  console.log("일반 상황2 -> 정보가 업데이트 될 때");
  return () => {
    console.log("뒷정리 함수 상황1 : 언마운트 되어서 숨기려할 때");
    console.log(
      "뒷정리 함수 상황2 -> 업데이트 되기 직전에. 즉 input에 값 입력해도 업데이트 직전인 상황나옴. 리액트 -> 리액ㅌ"
    );
    console.log("상황 2는 2번째 배열에 값에 따라 달라짐");
  };
}, [name]);
```

## 😉 useReducer

- 다양한 컴포넌트 상황에 따라 다양한 상태를 다른 값으로 업데이트 해주고 싶을 때
- 지금까지는 onClick 이벤트 같은 누르는 상황에만 값을 업데이트 했음.
- reducer(state, action). (현재 상태, 업데이트를 위해 필요한 정보를 담은 액션)
- action 값을 받아 새로운 상태로 변환 -> 불변성 유지
- 어떤 action인지 알려주는 type 필드 필요
- 컴포넌트 외부에 함수로 설정
- useReducer의 가장 큰 장점 : 컴포넌트 업데이트 로직을 컴포넌트 바깥으로 빼낸다.

```jsx
function reducer(state, action) {
  switch (action.type) {
    case "INCREASE":
      return { value: state.value + 1 };
    case "DECREASE":
      return { value: state.value - 1 };
    default:
      return state;
  }
}

const Counter = () => {
  const [state, dispatch] = useReducer(reducer, { value: 0 });

  return (
    <div>
      <p>현재 카운터 값 : {state.value}</p>
      <button onClick={() => dispatch({ type: "INCREASE" })}>+1</button>
      <button onClick={() => dispatch({ type: "DECREASE" })}>-1</button>
    </div>
  );
};
```

## 😉 useMemo

- 컴포넌트 내부에서 발생하는 연산 최소화
- 실습 코드는 insert외에 input 내용 수정되어도 getAverage함수가 호출됨
- useMemo 사용하면 특정 값이 바뀌었을 때만 연산을 실행, 원하는 값이 바뀌지 않았다면 이전 연산 결과를 다시 사용

## 😉 useCallback

- 만들어 놨던 함수 재사용
- 렌더링 성능 최적화
- 그냥 함수 선언하면 렌더링 할 때마다 함수 다시 렌더링
- useCallback 사용하면 처음 렌더링 했을 때 만들어 놓은 함수 리렌더링 시 다시 안만들고 재사용
- 두 번째 인자로 업데이트 된 상태 적용하면, 그때만 리렌더링할 때 함수 다시 생성

```jsx
import React, { useState, useMemo, useCallback } from "react";

const getAverage = (numbers) => {
  console.log("calculating now");
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((a, b) => a + b);
  return sum / numbers.length;
};

export default function Average() {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState("");

  const onChange = useCallback((e) => {
    setNumber(e.target.value);
  }, []);

  const onInsert = useCallback(
    (e) => {
      const nextList = list.concat(parseInt(number, 10));
      setList(nextList);
      setNumber("");
    },
    [number, list]
  );

  const avg = useMemo(() => getAverage(list), [list]);

  return (
    <div>
      <h1>Average</h1>
      <input value={number} onChange={onChange} />
      <button onClick={onInsert}>Enroll</button>
      <ul>
        {list.map((value, index) => (
          <li key={index}>{value}</li>
        ))}
      </ul>
      <div>
        <b>평균값:</b> {avg}
      </div>
    </div>
  );
}
```

## 😉 useRef

- ref 기능을 사용하고자 할 때 쓸 수 있다.
- 컴포넌트의 로컬 변수를 사용해야 할 때도 사용할 수 있다.
- useRef의 객체는 렌더링에 영향을 미치지 않는다.

```jsx
const inputEl = useRef(null);

const onInsert = useCallback(e => {
  ...
  inputEl.current.focus();
})

<input value={number} onChange={onChange} ref={inputEl} />
<button onClick={onInsert}>등록</button> //dom에 접근

const id = useRef(1);
const setId = (n) => {
  id.current = n;
}
const printId = () => {
  console.log(id.current) // 로컬 변수 (렌더링과 상관없이 바뀔 수 있는 값) 사용하기
}
```

## 😉 custom hooks

```jsx
import { useContext } from "react";
import RouterContext from "../components/RouterContext";

const useRouter = () => {
  const { setPath } = useContext(RouterContext);
  const push = (path) => {
    history.pushState({}, "", path);
    dispatchEvent(new Event("popstate"));
    setPath(path);
  };
  return { push };
};
export default useRouter;
```
