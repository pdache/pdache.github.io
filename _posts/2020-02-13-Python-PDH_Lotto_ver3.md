---
title: "[Python] 내 전용 로또 번호 생성기 #2"
excerpt: "로또 번호 생성 버튼 만들기"

categories:
- python
- project
tags:
- python
- tkinter
- 파이썬
- 로또
- toy project

---
이제 버튼을 만들어야 한다.  
버튼은 클릭 시 로또 번호를 생성해주는 기능을 가진다.  
이 버튼까지 만들고 Entry와 버튼, 창을 좀 더 크기를 다듬어서 디자인적인 부분은 끝낼 것이다.  
기능이 중요하기 때문에 더 이상은 시간을 지체할 수 없다.  
우선 바로 들어가보자잇!
### Tkinter Button
- - -
버튼에는 여러 가지 종류가 있다.  
```
- Button
- RadioButton
- CheckButton
- MenuButton
```
- 그냥 Button은 말 그대로 그냥 Button이다.
- RadioButton은 여러 옵션들이 있을 때 하나를 선택할 때 사용한다.  
- CheckButton은 여러 옵션들이 있을 때 여러 개를 선택할 때 사용한다.  
- MenuButton은 메뉴 기능을 가진 버튼을 생성할 수 있다.  

다 필요 없고 Button이 필요하다.  
우선 하나 만들어보자.

``` python
from tkinter import *
from tkinter import ttk

root=Tk()
root.title("PDH_Lotto")
root.geometry('400x300')

btn=ttk.Button()
btn.pack()

root.mainloop()
```
Button은 grid를 사용하지 않고 pack()을 사용했다.  
grid는 행렬 개념이긴 하지만 앞에서부터 채워지기 때문에 상대적인 위치를 잡아주는 pack()을 사용했다.  

![버튼](https://user-images.githubusercontent.com/37354733/74397969-572f6080-4e59-11ea-9f7f-e090c101cfac.png)  
버튼이 생겼지만 꽤나 심심하다.  
버튼 안에 text를 채워 넣어야겠다.  
이것 저것 설정하고 추가하기 위해 Button의 메서드와 파라미터에 대해 간단히 알아보자.    

### Button Method
- - -

|이름|기능|
|:---:|:---:|
|invoke()|버튼을 클릭했을 때와 같은 기능|
|flash()|버튼이 깜빡임|

### Button Parameter
- - -

|이름|기능|default|속성|
|:---:|:---:|:---:|:---:|
|text|버튼에 표시할 문자열|-|-|
|textvariable|버튼에 표시할 문자열을 가져올 변수|-|-|
|anchor|버튼안의 문자열 또는 이미지의 위치|center|n,ne,e,se,s,sw,w,nw,center|
|justify|버튼의 문자열이 여러 줄일 경우 정렬 방법|center|center,left,right|
|wraplength|자동 줄내림 설정 너비|0|상수|

메서드는 사용하지 않을 것 같고, text 파라미터만 사용하면 될 것 같다.  

``` python
btn=ttk.Button(root, text="번호 생성")
btn.pack()
```
이 부분만 수정하면 된다.  

![버튼](https://user-images.githubusercontent.com/37354733/74400529-81851c00-4e61-11ea-90b4-257aa426d5f0.png)    
드디어 버튼이 생성되었다.  
이제 번호 출력 Entry와 Button을 같이 출력해보자.  
오우 큰일났다.  
grid랑 pack이랑 같이 못 쓴다ㅋ  
이걸 이제 알아버려서 어떻게 할 까 하다가 place로 깔끔하게 좌표를 맞춰서 하기로 했다.  
코드가 좀 수정되긴 하지만 괜찮다.  

```python
from tkinter import *
from tkinter import ttk

root=Tk()
root.title("PDH_Lotto")
root.geometry('305x150')

entry1=ttk.Entry(root, width=5)
entry1.place(x=20, y=60)
entry2=ttk.Entry(root, width=5)
entry2.place(x=65, y=60)
entry3=ttk.Entry(root, width=5)
entry3.place(x=110, y=60)
entry4=ttk.Entry(root, width=5)
entry4.place(x=155, y=60)
entry5=ttk.Entry(root, width=5)
entry5.place(x=200, y=60)
entry6=ttk.Entry(root, width=5)
entry6.place(x=245, y=60)

btn=ttk.Button(root, text="번호 생성", width=10)
btn.place(x=115, y=90)

root.mainloop()
```  
place로 다 바꾸고 좌표 또한 내가 봤을 때 이쁘게 수정했다.  
Entry와 Button의 위치를 다 설정하니 창이 너무 커서 보기 싫어졌다.  
그래서 창도 줄였다.
![최종 프로그램 디자인](https://user-images.githubusercontent.com/37354733/74401187-dc1f7780-4e63-11ea-8c37-73d8f9010795.png)  
  기쁘다.  
[내가 원하는 디자인](https://user-images.githubusercontent.com/37354733/74393970-d8352a80-4e4e-11ea-9799-6016c4c77fdd.png){: target="_blank"}처럼 완성되었다.  
다음 포스팅부터는 기능적인 부분을 구현해보자!
