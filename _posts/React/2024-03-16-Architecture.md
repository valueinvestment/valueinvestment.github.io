---
title: "React Fiber 아키텍처 - React 톺아보기 스터디 0주차"
excerpt: "React Deep Dive"

categories:
  - React, React톺아보기
tags:
  - study, javascript, react
---

**React Fiber의 깊이 있는 탐구**

React Fiber는 React의 핵심 알고리즘을 재구성한 것으로, 더 나은 애플리케이션의 성능과 개발자 경험을 제공하기 위해 도입되었습니다. 이 아티클에서는 React Fiber의 구조, 작동 원리, 그리고 그것이 어떻게 React 애플리케이션의 성능을 향상시키는지에 대해 자세히 살펴보겠습니다. 🚀

---

## React Fiber의 기본 개념

React Fiber는 React 16에서 소개된 새로운 렌더링 엔진입니다. 기존의 "스택 렌더러"를 대체하는 이 새로운 엔진은 애플리케이션의 UI를 더 효율적으로 렌더링하고, 사용자와의 상호작용을 개선하는 목적을 가지고 있습니다. React Fiber는 비동기 렌더링과 성능 향상을 가능하게 하는 React의 핵심 알고리즘의 재구현입니다. 이것은 React의 핵심 알고리즘을 대대적으로 다시 작성한 것입니다.

- **주요 목표**:
  - **증분 렌더링(Incremental Rendering)**: 렌더링 작업을 작은 단위로 나누어 처리합니다.
  - **작업의 중단 및 재개**: 렌더링 작업을 중단하고 필요에 따라 재개할 수 있습니다.
  - **우선순위 기반 작업**: 더 중요한 작업을 먼저 처리합니다.

## 주요 개념

### 1. Fiber

Fiber는 React의 렌더링 파이프라인에서의 작업 단위입니다.

### 2. 조정 (Reconciliation)

조정은 현재 UI 상태와 새로운 상태를 비교하고 어떤 변경 사항이 적용되어야 하는지 결정하는 과정입니다. React Fiber는 "조정"이라는 프로세스를 사용하여 UI를 효율적으로 업데이트합니다.

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

가상 DOM은 실제 DOM의 가벼운 복사본입니다. React Fiber는 가상 DOM을 사용하여 실제 DOM을 직접 조작하지 않고도 UI를 효율적으로 업데이트합니다.

### React Fiber의 작동 원리

React Fiber의 핵심은 "Fiber"라는 작업 단위입니다. 각 Fiber는 React 컴포넌트에 대한 작업을 나타내며, React는 이러한 Fiber들을 사용하여 렌더링 작업을 관리합니다. 이것은 가상 스택 프레임을 나타냅니다. React는 Fiber를 사용하여 렌더링 작업의 우선 순위를 관리하고 예약합니다.

- **Fiber 노드**: 각 컴포넌트에 대한 정보와 수행해야 할 작업을 포함합니다.
- **Fiber 트리**: 애플리케이션의 컴포넌트 구조를 나타내는 트리입니다.
- **작업 우선순위**: React는 다양한 작업에 우선순위를 부여하여 중요한 작업을 먼저 수행합니다.

---

#### Fiber 작동 방식

1. **렌더링 단계**: 이 단계에서 React는 UI를 나타내는 Fiber 노드 트리를 구성합니다.
2. **커밋 단계**: 이 단계에서 React는 렌더링 단계에서 결정된 변경 사항을 실제 DOM에 적용합니다.

### React Fiber의 장점

React Fiber는 애플리케이션의 성능을 크게 향상시키며, 개발자가 더 나은 사용자 경험을 제공할 수 있도록 돕습니다.

- **유연한 작업 관리**: 작업의 중단 및 재개 기능을 통해 메인 스레드의 부하를 줄일 수 있습니다.
- **더 나은 사용자 경험**: 우선순위 기반 작업 처리를 통해 중요한 업데이트를 빠르게 반영할 수 있습니다.
- **향상된 성능**: React Fiber는 더 효율적인 렌더링 작업 스케줄링을 가능하게하여 복잡한 애플리케이션에서 향상된 성능을 제공합니다 (증분 렌더링).
- **비동기 렌더링**: Fiber를 사용하면 React가 렌더링 작업을 더 작은 조각으로 나누고 중요한 업데이트를 우선적으로 처리하여 사용자 경험을 더 부드럽게 만들 수 있습니다.

---

### 예시: Fiber의 작동 이해하기

React Fiber의 작동 원리를 이해하기 위해, 간단한 예시를 살펴보겠습니다. 아래는 React Fiber가 작업을 어떻게 처리하는지를 시각적으로 보여주는 예시 이미지입니다.

![React Fiber 작동 예시](https://files.codingninjas.in/article_images/react-fiber-architecture-1-1636956334.webp)

이 이미지는 React Fiber가 컴포넌트 트리를 어떻게 순회하며, 작업을 어떻게 나누고 처리하는지를 보여줍니다. 각 단계에서 React는 현재 처리 중인 컴포넌트의 작업을 평가하고, 필요에 따라 다른 작업으로 전환할 수 있습니다.

---

React Fiber는 React 애플리케이션의 성능과 개발자 경험을 혁신적으로 개선하는 중요한 발전입니다. 이를 통해 개발자들은 사용자에게 더 나은 인터랙티브 경험을 제공하며, 애플리케이션의 성능을 극대화할 수 있습니다. React Fiber의 깊이 있는 이해를 통해, 여러분의 애플리케이션 개발에 새로운 가능성을 탐색해 보세요! 🌈

더 많은 정보는 [공식 React 문서](https://reactjs.org/docs/faq-react.html)를 참조하십시오.

---

### References

- [React 파이버 아키텍처 분석](https://d2.naver.com/helloworld/2690975)
- [React Fiber Architecture](https://immigration9.github.io/react/2021/05/29/react-fiber-architecture.html)
