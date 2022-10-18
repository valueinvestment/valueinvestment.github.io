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

  /* 반응형 디자인 설정 */
  @media (max-width: 1024px) {
    width: 768px;
  }
`;

function Button({ children, ...props }) {
  return <StyledButton {...props}>{children}</StyledButton>;
}
```
