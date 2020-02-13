---
title: "[Python] 내 전용 로또 번호 생성기 #4"
excerpt: "기능 구현 - 2"

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
### Entry 출력 - 수정
- - -
지난 포스팅에서 아래와 같은 찌릿한 오류를 맛 보았다.  
![클릭 두번](https://user-images.githubusercontent.com/37354733/74407857-388b9280-4e76-11ea-95c7-f18b92f3b781.png)  
이 녀석을 수정하기 위해서는 먼저 있던 출력을 지워주는 과정이 필요했다.  
어떻게 해야할 지 생각을 해보다가 새로운 번호를 출력해주기 전에 확인을 해서 먼저 있던 출력이 있다면 지워주는 과정을 진행하기로 했다.  
그러기 위해서는 현재 출력되어 있는 값을 가져와야 했다.  
가져올 친구로 누가 있나 찾아보다 get()이라는 메서드를 발견했다.  
get() 메서드는 현재 Entry의 텍스트를 문자열로 **반환** 해주는 녀석이다.  
바로 테스트 해보았다.  

``` python
print(entry1.get())
```
이 코드를 추가하여 entry1의 값을 반환해보았다.  
![get() 테스트](https://user-images.githubusercontent.com/37354733/74408439-c0be6780-4e77-11ea-8ab2-6051a7dd2f9b.png)  
잘 반환해준다.  
이제 이 반환되는 값으로 값이 있는지 없는지 판단하면 된다.  
판단만 하고 그치는 것이 아니라 값이 있다면 지워주어야 한다.  
그 부분은 delete() 메서드가 담당한다.  
delete() 메서드는 ``` delete(start, end) ```로 사용할 수 있는데 start부터 end까지의 문자열을 삭제해준다.  
그럼 사용해보자잇!  

``` python
from tkinter import *
from tkinter import ttk
import random
def num_Create(click):
    num_list=[]
    while len(num_list)<6:
        num_list.append(random.randrange(1,46))
        num_list=set(num_list)
        num_list=list(num_list)
    num_list.sort()
    if not entry1.get()=='':
        entry1.delete(0,'end')
        entry2.delete(0, 'end')
        entry3.delete(0, 'end')
        entry4.delete(0, 'end')
        entry5.delete(0, 'end')
        entry6.delete(0, 'end')

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
어우 코드가 더 길어졌다.  
각 Entry마다 삭제를 해주어야 하기 때문에 또 6줄 추가해버렸다.  
최적화 무조건 해야겠다.  
설레는 마음으로 실행해보았다.  

![한번 클릭](https://user-images.githubusercontent.com/37354733/74408678-6d004e00-4e78-11ea-838a-67dd93e60e3c.png)  
![두번 클릭](https://user-images.githubusercontent.com/37354733/74408707-7c7f9700-4e78-11ea-842c-c110ccaa4ca0.png)  
오우.  
전의 값도 잘 사라진다.  
근데 뭔가 좀 심심하다.  
대박을 기원하는 문구를 하나 넣으면 좋을 것 같다.  

### Label - 대박 기원  
- - -
Entry로 문구를 넣어도 좋지만 뭔가 고정된 느낌을 주고 싶어서 Label을 택하게 되었다.  
Label을 안 써보기도 했으므로 당첨이다.  
Label은 약간 주석 느낌이다.  
우선 예시로 한 번 사용해보자잇!  

``` python
from tkinter import *

root=Tk()
root.title("PDH_Lotto")
root.geometry('305x150')

label=Label(root,text="라벨 테스트")
label.pack()

root.mainloop()
```
테스트이므로 간단한 코드를 작성해보았다.  
Label도 Entry와 비슷한 느낌으로 사용해주자.  

![Label 테스트](https://user-images.githubusercontent.com/37354733/74409105-5efefd00-4e79-11ea-8ae2-7df46cfea20f.png)  
오호. 이런 느낌.  
밋밋하긴 하다.  
글자 색을 빨간색으로 바꿔서 내 프로그램에 적용시켜보자.  

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
    if not entry1.get()=='':
        entry1.delete(0,'end')
        entry2.delete(0, 'end')
        entry3.delete(0, 'end')
        entry4.delete(0, 'end')
        entry5.delete(0, 'end')
        entry6.delete(0, 'end')

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
글자색을 빨간색으로 하기 위해 ``` fg='red' ```를 추가했다.  
fg는 글자색을 의미한다.  
(참고로 bg는 배경 색이다.)  
실행해보자잇!  

![Label 적용 - 클릭 전](https://user-images.githubusercontent.com/37354733/74409364-e77d9d80-4e79-11ea-9aa5-39ea8586964d.png)  
아직 클릭 안 해서 대박 기원 메세지가 나오지 않는다.  
눌러보자잇!  
![Label 적용 - 클릭 후](https://user-images.githubusercontent.com/37354733/74409425-04b26c00-4e7a-11ea-893d-9954b361115f.png)  
예쁘다.  
기분이 그냥 좋아진다.  
이로써 프로그램은 완성이다.  
하지만 코드가 너무 길다.  
간단한 프로그램인만큼 코드도 길지 않았으면 했는데 생각보다 많이 길어졌다.  
다음 포스팅에서 한 번 줄여보자잇!  
