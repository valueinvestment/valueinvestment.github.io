---
title:  "[React를 다루는 기술] 4장 - 이벤트 핸들링 "
excerpt: ""
toc: true
toc_sticky: true

categories:
  - React
tags:
  - [React, JS, Java Script, Study]
---  

## 😉 이벤트 핸들링 ##
- 이벤트 : 사용자가 웹 브라우저에서 DOM 요소들과 상호 작용 하는 것
  - 마우스 커서 올리기, 클릭하기, Form 요소에서 값 바뀌면 onChange 이벤트..

- 리액트의 이벤트 시스템
  1. 주의 사항
  - 이벤트 이름은 카멜 표기법 ex) onclick => onClick, onkeyup => onKeyUp
  - 이벤트에 코드가 아닌 함수 형태의 값(객체)을 전달한다.
  - 함수 전달에 좋은 화살표 함수 사용
  - 렌더링 부분 외부에 미리 만들어서 전달 가능
  - DOM 요소에만 이벤트를 설정할 수 있다. (html 태그 같은 DOM요소에만 설정 가능)
  - 컴포넌트에는 설정이 안된다.

  2. 자주 사용하는 이벤트
  - 참고(https://reactjs.org/docs/events.html)


## 😉 함수형 컴포넌트에서 이벤트 예제 ##

- e 객체 : SyntheticEvent. 웹 브라우저의 네이티브 이벤트랄 감싸는 개체. 이벤트가 끝나면 초기화

```jsx
const EventPractice = () => {
  const [message, setMessage] = useState(''); //  기본 형태
  const [form, setForm] = useState({
    userMessage: '',
    username: '',
  }) //  useState()의 두번 째 인자 상태 설정 함수를 2개 써도 상관없음.
  const onClick = () => {
    alert(message);
    setMessage('');
  }; // 임의 메서드로 return 밖에 선언함으로 가독성 확보(성능은 비슷)

const onChage = (e) =>{
    const nextForm = {
        ...form,        // 불변성 유지 위해
        [e.target.name] : e.target.value
    }
    setForm(nextForm)
} // 두개의 input을 하나의 onChange로 관리

  return (
    <div>
      <h1>이벤트 연습</h1>
      <input
        type="text"
        name="message"
        value={message}
        placeholder="아무거나 입력해보세요."
        onChange={(e) => {
          setMessage(e.target.value);
        }}
      />

      <input
          type="text"
          name="userMessage"
          onChange = {onChange}
      />
      <input
          type="text"
          name="username"
          onChange = {onChange}
      />

      <button onClick={onClick}> 확인 </button>
    </div>
  );
};
```
