# 파이썬 GUI

## Tkinter
- Tkinter는 최신 Python 프로그램에 포함된 내장된 모듈
- Tcl/Tk에 대한 파이썬 Wrapper
- Tcl : Tool Command Language 일종의 프로그래밍 언어
- Tk : Took kit 일종의 GUI 툴킷
- 지원되는 위젯들이 부족하고 UI도 예쁘지는 않지만, 간단히 GUI 만들 떄 쉽게 사용
- **파이참 Pyqt5 사용하면 GUI 이쁘게 가능**

## Tkinter의 기본 문장
### Tkinter 모듈 import
```py
from tkinter import *

root = Tk() # root = new Tk(), root 객체 생성,  Tk() -> 윈도우 만들어주는 역할
root.mainloop() # root는 윈도우, mainloop 돌게끔 설정

```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/166200466-11d95e03-b6ce-4725-b35a-5fffdf423fa6.png)

### 타이틀 생성
```py
from tkinter import *

root = Tk() 
root.title("Python GUI")

root.mainloop() 
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/166200718-194fd414-6c13-4a56-97a9-d967f677dcbf.png)


### 윈도우 창 일정크기로 설정
```py
from tkinter import *

root = Tk() 
root.title("Python GUI")
root.geometry('800x600+200+100') #크기 800x600,  200 x축, 100 y축 -> 실행시 특정위치에 고정되서 나오게 해줌
root.resizable(False,False) # 윈도우 x,y 사이즈 조절 못하게 false로 막음 True로 하면 변경 가능
root.mainloop() 

```

### 출력결과
- 사이즈 800 x 600으로 고정되어 출력

![image](https://user-images.githubusercontent.com/82345970/166200947-8230439e-de6b-466c-9e27-994083f46b9a.png)

### 위젯이란
- 버튼,체크박스,리스트박스,라디오버튼,슬라이드바, 텍스트, 메뉴바, 프로그레스바 등 의 컨트롤들을 통틀어 **위젯** 이라고 함

### 버튼 만들기
- Button() 위젯을 사용

```py
from tkinter import *

root = Tk() 
root.title("Python Button")
root.geometry('800x600+200+100')

btn1 = Button(root,text = "버튼인가?") # btn1 = new Button()
btn1.pack() # pack() 없으면 안된다.

root.mainloop() 
```

### 출력결과
- pack()을 해야만 실제 루트에 버튼이 포함된다.
 
![image](https://user-images.githubusercontent.com/82345970/166202113-0a924c8b-e74a-4de8-8d24-d3b562f681bd.png)

### 버튼 출력
```py
from tkinter import *

root = Tk() 
root.title("Python Button")
root.geometry('800x600+200+100')

btn1 = Button(root, text = "나버튼인가?") # btn1 = new Button()
btn1.pack()


btn2 = Button(root, padx = 20, pady = 50, text = "아무튼")
btn2.pack()

btn3 = Button(root,width = 10, height = 5, text = "튼튼", fg = "white", bg = "red")
btn3.pack()

root.mainloop() 




```

### 출력결과
- 빨간색배경, 흰색 글씨

![image](https://user-images.githubusercontent.com/82345970/166205283-e3627744-91b3-4e46-9f3c-efacd436bcaa.png)


### 버튼 이미지 넣기, 버튼 눌렀을때 이벤트
```py
from tkinter import *


root = Tk() 
root.title("Python Button")
root.geometry('800x600+200+100')

def btncmd():
    print("좋아요를 꾸~욱 눌러주세요")

photo = PhotoImage(file = "jamsuham.png")
btn = Button(root, image = photo, command= btncmd)
btn.pack()

root.mainloop() 

```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/166206699-1202d3fe-0318-4f7c-8db2-25f997a778fe.png)

### 레이블 예제
```py
from tkinter import *


root = Tk() 
root.title("Python Button")
root.geometry('800x600+200+100')

label = Label(root, text = "누구인가?")
label.pack()

root.mainloop() 
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/166207516-2d742c3b-81dd-4001-adba-3c8c4c603a9b.png)

### 레이블 이미지 넣기
```py
from tkinter import *


root = Tk() 
root.title("Python Button")
root.geometry('800x600+200+100')

photo = PhotoImage(file = "jamsuham.png")
label = Label(root, image=photo)
label.pack()

root.mainloop() 
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/166207653-904b9656-f2cd-4d7a-af01-fc9b5b6ab395.png)


### 버튼,레이블 조합 예제
```py
from tkinter import *


root = Tk() 
root.title("Python Button")
root.geometry('800x600+200+100')


label = Label(root, text = "최선을 다하자")
label.pack()

def change():
    label.config(text = "아자아자 화이팅") # config -> label text 변경해준다
btn = Button(root, text = "클릭", command = change)
btn.pack()
root.mainloop() 
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/166208317-48d06562-7dec-44e9-ba74-b9ece16c83ce.png)


### 버튼 클릭시, 이미지 변경
```py
from tkinter import *


root = Tk() 
root.title("Python Button")
root.geometry('800x600+200+100')


label = Label(root, text = "최선을 다하자")
label.pack()

def change():
    global photo #photo 전역변수로 만들어줌, 지역변수로 하면, 클릭시 지역변수라서 유지가 안됨
    photo = PhotoImage(file = "jamsuham.png")
    label.config(image=photo)
btn = Button(root, text = "클릭", command = change)
btn.pack()
root.mainloop() 
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/166208793-9eaa3fe0-1765-40e5-96bd-af7ff44d71dd.png)

### TEXT 입력창 만들기
```py
from tkinter import *


root = Tk() 
root.title("Python Button")
root.geometry('800x600+200+100')

txt = Text(root, width = 40, height = 20)
txt.pack()

root.mainloop()
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/166637991-93cb297a-680a-4e71-aabb-603757f9647c.png)

### TEXT 입력창 만들기
- **입력창에 미리 글자 입력하는 방법**

```py
from tkinter import *


root = Tk() 
root.title("Python Button")
root.geometry('800x600+200+100')

txt = Text(root, width = 40, height = 20)
txt.insert(END, "글자를 입력하세요")
txt.pack()

root.mainloop()
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/166638197-824b88b5-3a15-4858-9a32-35274e9260e9.png)

### Entry를 이용한 로그인창 만들기
```py
from tkinter import *


root = Tk() 
root.title("Python Button")
root.geometry('800x600+200+100')

ent1 = Entry(root, width = 30)
ent1.insert(END, "ID를 입력하세요")
ent1.pack()

ent2 = Entry(root, width = 30)
ent2.insert(END, "비밀번호를 입력하세요")
ent2.pack()

def btncmd():
    print(ent1.get())
    print(ent2.get())

def btndelete():
    ent1.delete(0,END)
    ent2.delete(0,END)
btn = Button(root, text = "로그인", command = btncmd)
btn.pack()

btn2 = Button(root, text = "삭제", command = btndelete)
btn2.pack()

root.mainloop()

```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/166639990-aa5567d5-70ee-4035-a809-a39e2bd6e9ad.png)

### Listbox 예제
```py
from tkinter import *


root = Tk() 
root.title("Python listbox")
root.geometry('800x600+200+100')

listbox = Listbox(root,selectmode = "extended", height = 5)

listbox.insert(0, "파이썬")
listbox.insert(1, "C#")
listbox.insert(2, "HTML5")

listbox.insert(END, "자바")
listbox.insert(END, "Node")
listbox.pack()

root.mainloop()
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/166640731-b453787d-2269-487e-8bbb-209afecc6f1a.png)

### Listbox 예제
- **selectmode = single로 바꾸면 리스트에 있는 항목들 shift(키보드)눌렀을때 여러항목 선택 안 됨**
- **height =10 리스트항목 10개 생김**
```py
from tkinter import *


root = Tk() 
root.title("Python listbox")
root.geometry('800x600+200+100')

listbox = Listbox(root,selectmode = "single", height = 10) 

listbox.insert(0, "파이썬")
listbox.insert(1, "C#")
listbox.insert(2, "HTML5")

listbox.insert(END, "자바")
listbox.insert(END, "Node")
listbox.pack()

root.mainloop()
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/166641386-76cded3e-89eb-4e11-93ab-a80fc27cbba7.png)






















