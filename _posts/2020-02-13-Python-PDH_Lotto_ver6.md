---
title: "[Python] 내 전용 로또 번호 생성기 #5"
excerpt: "코드 최적화 및 완성"

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
### 코드 최적화
- - -
프로그램의 동작은 완성이지만 코드가 최적화되지 않았기 때문에 완성이라고 할 수 없다.  
이번 포스팅에서 코드를 최적화하고 완성을 시켜볼것이다.  
최적화를 위해 내 코드에서 겹치는 부분을 확인해보니 각 Entry에 대해 객체를 생성하고 배치하는 부분과 값을 넣어주는 부분, 값이 있을 때 삭제하는 부분이 껄끄러웠다.  
이 부분을 반복문을 써서 줄여보자는 생각이 들었다.  
근데 반복문을 써서 될까 의문이긴 했지만 한 번 해보았다.  
우선 각 Entry에 대해 객체를 생성하고 배치하는 부분을 바꿔보자.  

``` python
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
```  
이 부분을 반복문을 통해 바꿔보아야겠다.  
``` python
entry=[]
for i in range(6):
    entry[i]=ttk.Entry(root, width=5)
    entry[i].place(x=20+(45*i), y=60)
```  
이렇게 바꿔 보았다.  
하지만 에러가 발생했다.  
![에러 발생](https://user-images.githubusercontent.com/37354733/74410094-9a9ac680-4e7b-11ea-8945-91052953b725.png)  
범위를 벗어났다고 한다.  
난 안 벗어났는디.  
자세히 살펴보니 귀여운 실수가 하나 있었다.  
entry라는 list는 현재 비어 있는 list라 값을 할당할 수 가 없는 것이다.  
append를 많이 쓰다보니 감이 죽었나 보다.  

``` python
entry=[]
entry=[0]*6
for i in range(6):
    entry[i]=ttk.Entry(root, width=5)
    entry[i].place(x=20+(45*i), y=60)
```  
꼼수 느낌으로 ``` entry=[0]*6 ``` 코드를 추가하여 임의적으로 공간을 할당해주었다.  
그랬더니 제대로 출력되는 모습을 확인할 수 있었다.  
여기서도 통했으므로 값을 넣어주는 부분과 값이 있을 때 삭제하는 부분도 반복문으로 처리할 수 있겠다는 생각이 들었다.  

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
    if not entry[0].get()=='':
        for i in range(6):
            entry[i].delete(0, 'end')

    for i in range(6):
        entry[i].insert(0, num_list[i])

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
바로 코드를 바꿔보았다.  
예상대로 아주 잘 되었다.  
코드도 아까보다 많이 줄어들어서 예쁨이 뿜뿜해졌다.  
더 최적화할 부분이 있나 살펴보았지만 만족을 해서 그런가 보이지도 않는다.  
내 마음대로 완성이다.  
**이제 로또 사러간다잇!**  
