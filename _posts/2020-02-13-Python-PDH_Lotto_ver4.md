---
title: "[Python] 내 전용 로또 번호 생성기 #3"
excerpt: "기능 구현 - 1"

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
드디어 기능을 구현한다.  
기능이 한 가지 밖에 없어서 김이 새긴 하지만 천리길도 한 걸음부터이다.  
내 프로그램의 기능은 번호 생성 버튼을 클릭했을 때 중복되지 않은 6개의 숫자가 출력되는 것이다.  
그 점만 유의해서 구현해보도록 하자!  

### 마우스 클릭 - bind
- - -
우선 마우스로 번호 생성 버튼을 클릭했을 때 기능을 실행해주는 함수로 넘어가야한다.  
마침 적당한 녀석이 있다.  
bind라는 녀석인데 bind()는 이벤트 바인딩을 위한 메서드이다.  
이 녀석은 이벤트와 핸들러를 연결해주는 역할을 한다.  
이벤트 명에는 여러 가지가 있다.  
```
- <Button-1> : 마우스 왼쪽 버튼 클릭
- <Button-2> : 마우스 중간 버튼 클릭
- <Button-3> : 마우스 오른쪽 버튼 클릭
- <Double-Button-1> : 마우스 왼쪽 버튼 더블 클릭
- <Return> : Enter 키 눌려짐
- <Key> : 키가 눌려짐
```  
이 녀석들 중 나는 마우스로 한번 클릭이므로 Button-1을 사용할 것이다.  

``` python
from tkinter import *
from tkinter import ttk
def num_Create(click):
    print('hi')

root=Tk()
root.title("PDH_Lotto")
root.geometry('305x150')

entry=[]
entry=[0]*6
for i in range(6):
    entry[i]=ttk.Entry(root, width=5)
    entry[i].place(x=20+(45*i), y=60)

btn=ttk.Button(root, text="번호 생성", width=10)
btn.bind("<Button-1>", num_Create)
btn.place(x=115, y=90)
root.mainloop()
```  
btn에 마우스 왼쪽 버튼 클릭과 로또 번호를 생성해주는 num_Create 핸들러를 연결해주었다.  
잘 연결되었는지 확인하기 위해 hi를 출력하게 해보았다.  
![bind 테스트](https://user-images.githubusercontent.com/37354733/74406961-450eeb80-4e74-11ea-9f04-424947f60a1b.png)  
기모찌.  
아주 잘 연결되었다.  
이제 로또 번호를 생성해보자.  

### 로또 번호 생성 구현
- - -
우선 로또 번호를 생성해서 출력하고 제대로 나오는 지 확인해보자.  

``` python
import random
num_list=[]
while len(num_list)<6:
    num_list.append(random.randrange(1,46))
    num_list=set(num_list)
    num_list=list(num_list)
num_list.sort()
print(num_list)
```

로또 번호는 랜덤이기 때문에 random 모듈을 import했다.  
그리고 random으로 추출되는 번호를 저장하기 위한 list를 선언하고, 1부터 45까지의 숫자를 위해 randrange 함수를 사용했다.  
중복 처리에 대한 부분때문에 set 자료형으로 처리할까도 생각했지만, 나는 list가 편하므로 list로 처리했다.  
하지만 set도 잠시나마 사용했다.  
set로 중복을 제거하고 다시 list로 변환해주었다.
그리고 sort하고 출력해보았다.  
![로또 번호 테스트](https://user-images.githubusercontent.com/37354733/74407307-18a79f00-4e75-11ea-81d1-9ff5e64b5e49.png)  
잘 나온다.  
이제 함수에 넣어서 나의 목표를 향해 한걸음 더 나아가보자.  

### Entry에 값 출력
- - -
이제 생성된 로또 번호를 각 Entry에 출력해주어야 한다.  
각 Entry에 출력해주기 위해서는 insert라는 친구가 필요하다.  
Entry의 메서드 중 하나인 insert는 ``` insert(index, "문자열") ```로 사용할 수 있는데, 이 친구는 index 위치에 문자열을 추가해준다.  
그럼 사용해보자잇!  

``` python
from tkinter import *
from tkinter import ttk
import random
def num_Create(click):
    label=Label(root, text="당첨되시길^ㅇ^", fg='red')
    label.place(x=115,y=20)
    num_list=[]
    while len(num_list)<6:
        num_list.append(random.randrange(1,46))
        num_list=set(num_list)
        num_list=list(num_list)
    num_list.sort()
    entry1.insert(0,num_list[0])
    entry2.insert(0, num_list[1])
    entry3.insert(0, num_list[2])
    entry4.insert(0, num_list[3])
    entry5.insert(0, num_list[4])
    entry6.insert(0, num_list[5])



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
btn.bind("<Button-1>", num_Create)
btn.place(x=115, y=90)
root.mainloop()
```
각 Entry에 추가해줘야 하므로 하나하나 다 넣어주었다.  
좀 보기 껄끄럽다.  
우선 구현하고 나중에 최적화해봐야겠다.  
이렇게 코드를 작성하고 한 번 돌려 보았다.  

![Entry 출력](https://user-images.githubusercontent.com/37354733/74407841-30335780-4e76-11ea-92cf-ddca1d185ea0.png)  
짜릿.  
기분 좋아서 한번 더 눌렀다가 찌릿했다.  
![클릭 두번](https://user-images.githubusercontent.com/37354733/74407857-388b9280-4e76-11ea-95c7-f18b92f3b781.png)  
이게 뭐람.  
한 번 더 눌렀을 때 전의 값이 지워지지 않았다.  
이 부분을 해결해야 한다.  
아 물론 다음 포스팅에서.  
