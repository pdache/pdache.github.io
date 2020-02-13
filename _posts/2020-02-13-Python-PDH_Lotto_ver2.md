---
title: "[Python] 내 전용 로또 번호 생성기 #1"
excerpt: "기본 문법 이해 및 세팅"

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

Tkinter는 파이썬 기본 내장 모듈이다.  
그저 import만 하면 되기 때문에 아주 좋다.  
Tkinter의 기본적인 느낌을 맛보고 가자.
### Tkinter 기본 문장
- - -
``` python
from tkinter import *
root=Tk()
root.title("PDH_Lotto")
root.mainloop()
```
우선 tkinter 모듈을 import하는 것에서 시작한다.  
import를 하고 나서는 Tk 클래스 객체를 root에 설정한다.  
그리고 이 객체의 title 즉, 프로그램의 상단 바에 나타나는 제목을 설정한다.  
바로 내 signature인 PDH를 설정해주었다.  
그 후, mainloop() 메서드를 호출한다. mainloop() 메서드는 이벤트 메시지 루프로서 키보드나 마우스 등 다양한 이벤트로부터 오는 메시지를 받고 전달하는 역할을 한다.  
위의 코드를 실행하면 기본적인 틀을 만들게 된다.
![PDH_Lotto 틀](https://user-images.githubusercontent.com/37354733/74389436-7c17d980-4e41-11ea-99ea-32bdeed27099.png)
예쁘다.  
하지만 크기가 작아서 PDH_Lotto로 설정한 나의 title이 잘려서 나오는 것을 확인할 수 있다.  
이 때 사용할 수 있는 geometry 메서드를 사용해서 title을 정상적으로 출력해야 한다.  
- - -
``` python
from tkinter import *
root=Tk()
root.title("PDH_Lotto")
root.geometry("400x300")
root.mainloop()
```
geometry 메서드는 객체.geometry("너비x높이+x좌표+y좌표")로 나타내어 창의 너비와 높이, 초기 화면 위치의 x, y 좌표를 설정할 수 있다.
나는 굳이 x,y 좌표는 필요성을 못 느껴서 너비와 높이만 설정했다.  
![크기 재설정](https://user-images.githubusercontent.com/37354733/74393350-2cd7a600-4e4d-11ea-8b36-0411ec22e303.png)
예쁘다.  
빨리 안에 채워 넣고 싶은 욕구가 생겼다.  

### PDH_Lotto Entry
- - -
번호가 생성되면 생성된 번호를 표시해줄 칸이 필요하다.  
이런 칸은 Entry로 해결할 수 있다.  
Entry(기입창)는 텍스트를 입력받거나 출력하기 위한 것이다.  
나는 출력만 하기 때문에 입력은 사용하지 않는다.  
나는 ttk 모듈을 사용할 것인데 tkinker의 확장 모듈로서 좀 더 디자인이 이쁘다.
Entry는 번호가 6개이므로 6개를 사용한다.

``` python
from tkinter import *
from tkinter import ttk

root=Tk()
root.title("PDH_Lotto")
root.geometry('400x300')

entry1=ttk.Entry(root)
entry1.grid(row=1, column=0)
```
우선은 잘 나오나 하나만 테스트 해보았다.  
grid가 궁금할 수 있는 사람들을 위해 짧게 설명하자면 tkinter의 위젯 배치를 위한 것이다.  
place(절대 위치 배치)와 pack(상대 위치 배치)도 있지만 나는 grid가 편하고 끌려서 grid를 택했다.  

![Entry 사용 예시](https://user-images.githubusercontent.com/37354733/74396050-46302080-4e54-11ea-8bb6-1d9e9619d7d1.png)
실행 화면이다.  
좀 맘에 안든다. 번호를 출력하는 것이기 때문에 큰 공간이 필요하지는 않다.  
조금 수정해보자.

``` python
from tkinter import *
from tkinter import ttk

root=Tk()
root.title("PDH_Lotto")
root.geometry('400x300')

entry1=ttk.Entry(root, width=5)
entry1.grid(row=3, column=0)
```
Entry의 default width는 20으로 설정되어 있기 때문에 5로 바꿔보았다.  
![Entry 수정](https://user-images.githubusercontent.com/37354733/74396277-ce162a80-4e54-11ea-99da-547c5dcbbd3c.png)
예뻐졌다.  
이제 6개 만들어보자.  

``` python
from tkinter import *
from tkinter import ttk

root=Tk()
root.title("PDH_Lotto")
root.geometry('400x300')

entry1=ttk.Entry(root, width=5)
entry1.grid(row=1, column=0)
entry2=ttk.Entry(root, width=5)
entry2.grid(row=1, column=1)
entry3=ttk.Entry(root, width=5)
entry3.grid(row=1, column=2)
entry4=ttk.Entry(root, width=5)
entry4.grid(row=1, column=3)
entry5=ttk.Entry(root, width=5)
entry5.grid(row=1, column=4)
entry6=ttk.Entry(root, width=5)
entry6.grid(row=1, column=5)

root.mainloop()
```
말 그대로 6개 추가했다.  
column은 1씩 증가했다. 행렬 개념을 적용해서 생각해야 한다.
![Entry 6개](https://user-images.githubusercontent.com/37354733/74396452-5e546f80-4e55-11ea-8604-d43cb91abf25.png)
예쁘다.  
이제 버튼을 만들어야 한다.  
버튼은 다음 포스팅에서 만들 것이다.  
