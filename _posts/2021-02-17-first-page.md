---
title:  "GitHub Blog 첫번째 포스팅"
excerpt: "GitHub Blog 서비스인 github.io 블로그 시작."

categories:
  - Blog
tags:
  - test
---  

#처음 시작하면서

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

**잘 만 되네.. ㅋㅋㅋㅋㅋ 일단 쓴다**

YFM에서 정의한 제목을 이중 괄호 구문으로 본문에 추가할 수 있다.  
이 글의 제목은 {{ page.title }}이고  
마지막으로 수정된 시간은 {{ page.last_modified_at }}이다.  