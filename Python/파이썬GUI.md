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


btn2 = Button(root, padx = 20, pady = 20, text = "아무튼")
btn2.pack()

root.mainloop() 
```

### 출력결과
- padding 설정(버튼, 버튼 사이)

![image](https://user-images.githubusercontent.com/82345970/166202485-6d035edf-57a9-4b71-bcb0-4bda102f912b.png)











