---
title: "리액트 Fiber 아키텍처 - 리액트 톺아보기 스터디 0주차"
excerpt: "React Deep Dive"

categories:
  - React, 리액트톺아보기
tags:
  - study, javascript, react
---

# 리액트 Fiber 아키텍처

## 소개

리액트 Fiber는 비동기 렌더링과 성능 향상을 가능하게 하는 리액트의 핵심 알고리즘의 재구현입니다. 이것은 리액트의 핵심 알고리즘을 대대적으로 다시 작성한 것입니다.

## 주요 개념

### 1. 피버 (Fiber)

피버는 리액트의 렌더링 파이프라인에서의 작업 단위입니다. 이것은 가상 스택 프레임을 나타냅니다. 리액트는 피버를 사용하여 렌더링 작업의 우선 순위를 관리하고 예약합니다.

### 2. 조정 (Reconciliation)

조정은 현재 UI 상태와 새로운 상태를 비교하고 어떤 변경 사항이 적용되어야 하는지 결정하는 과정입니다. 리액트 피버는 "조정"이라는 프로세스를 사용하여 UI를 효율적으로 업데이트합니다.

### 예시:

```jsx
// 이전 상태
const oldState = { count: 2 };

// 새로운 상태
const newState = { count: 3 };

// 조정 과정
if (oldState.count !== newState.count) {
  // 새로운 카운트로 UI 업데이트
}
```

### 3. 가상 DOM (Virtual DOM)

가상 DOM은 실제 DOM의 가벼운 복사본입니다. 리액트 피버는 가상 DOM을 사용하여 실제 DOM을 직접 조작하지 않고도 UI를 효율적으로 업데이트합니다.

## 피버 작동 방식

1. **렌더링 단계**: 이 단계에서 리액트는 UI를 나타내는 피버 노드 트리를 구성합니다.
2. **커밋 단계**: 이 단계에서 리액트는 렌더링 단계에서 결정된 변경 사항을 실제 DOM에 적용합니다.

## 리액트 피버의 장점

- **향상된 성능**: 리액트 피버는 더 효율적인 렌더링 작업 스케줄링을 가능하게하여 복잡한 애플리케이션에서 향상된 성능을 제공합니다.
- **비동기 렌더링**: 피버를 사용하면 리액트가 렌더링 작업을 더 작은 조각으로 나누고 중요한 업데이트를 우선적으로 처리하여 사용자 경험을 더 부드럽게 만들 수 있습니다.

## 예제 코드:

```jsx
import React from "react";

class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  handleClick = () => {
    this.setState((prevState) => ({
      count: prevState.count + 1,
    }));
  };

  render() {
    return (
      <div>
        <p>카운트: {this.state.count}</p>
        <button onClick={this.handleClick}>증가</button>
      </div>
    );
  }
}

export default Counter;
```

위의 예제에서 버튼이 클릭될 때마다 컴포넌트의 상태가 업데이트되어 UI가 다시 렌더링됩니다.

더 많은 정보는 [공식 리액트 문서](https://reactjs.org/docs/faq-react.html)를 참조하십시오.

전부 이해하지 못했습니다 계속 문서를 읽어보는 과정이 있어야 이해가 될 것 같습니다.

---

### References

- [React 파이버 아키텍처 분석](https://d2.naver.com/helloworld/2690975)
- [React Fiber Architecture](https://immigration9.github.io/react/2021/05/29/react-fiber-architecture.html)
