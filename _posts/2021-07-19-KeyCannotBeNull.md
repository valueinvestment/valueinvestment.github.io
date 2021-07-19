---
title:  "Key cannot be null. Parameter name: key"
excerpt: "C# Winform Design Time Error"
image: "../assets/images/cat.jpg"

header:  
  overlay_image: https://i.pinimg.com/originals/79/85/58/798558dfd2f90b4ca98635358b3d2fa7.png
  overlay_filter: 0.5 # 투명도

categories:
  - Coding
  
tags:
  - [C#, Winform, Bug]
---  

# Key cannot be null. Parameter name: key

### Design Time 오류

Component(UserControl)를 만들고 나서 다른 Component에 올려놓으니 딱 하고 뜨는 에러.. 

![얘는 또 뭐야](/assets/images/KeyCannotBeNull/ValueCannotBeNull.png)

이 에러는 Visual Studio에서 Design_Time 에 Component를 그릴 때 나는 에러입니다. 

![코드를 살펴보자](/assets/images/KeyCannotBeNull/CodeSample.png)

코드에서 보면 Property들과 Initialize, Load 이벤트 까지가 DesignTime에도 사용됩니다. 
 
![코드를 살펴보자](/assets/images/KeyCannotBeNull/Answer.png)

이런식으로<span style="color:red"> DesignTime에 Load를 하지 않도록 설정</span>하면 간단하게 해결이 됩니다.

컴포넌트에서 Key cannot be null. 이런 식의 에러가 나면 자동 실행부분을 잘 봐주세요.