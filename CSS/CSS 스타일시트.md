## CSS란
- CSS란 Casading Style Sheet 약자로 스타일 시트이다
- HTML로 만들어 놓은 페이지의 레이아웃과 모양을 훨씬 더 좋게 만드는 기술
- 반복적으로 사용되는 서식을 미리 설정하거나, 글자,색상,프레임등을 꾸밀 수 있다

## CSS기본->스타일적용 전(폰트색,폰트크기)
```html
<html>
    <head>
        <meta content = "text/html"; charset = "utf-8"/>
    </head>
    <body>
        

        <p><font color = "red" size = "2">별 하나에 추억과</font></p>
        <p><font color = "red" size = "2">별 하나에 사랑과</font></p>
        <p><font color = "red" size = "2">별 하나에 쓸쓸함</font></p>
        <p><font color = "red" size = "2">별 하나에 동경과</font></p>
        <p><font color = "red" size = "2">별 하나에 시와</font></p>
        <p><font color = "red" size = "2">별 하나에 어머니</font></p>



    </body>
</html>
```



## CSS기본->스타일적용 후(폰트색,폰트크기)
- <style type = "text/css"> </style> 선언
 
```html
<html>
    <head>
        <meta content = "text/html"; charset = "utf-8"/>
        <style type = "text/css">
            body{font:20pt;color:red;}
        </style>
    </head>
    <body>
        

        <p>별 하나에 추억과</p>
        <p>별 하나에 사랑과</p>
        <p>별 하나에 쓸쓸함</p>
        <p>별 하나에 동경과</p>
        <p>별 하나에 시와</p>
        <p>별 하나에 어머니</p>



    </body>
</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163747724-c574e50a-d7a9-4f38-aded-a5f1fb4ae616.png)

### CSS사용방법1
- **문장 안에서의 스타일 시트(Internal style sheet)**
- HTML태그내에 스타일 지정
- 한번만 정의해서 전체에 적용되는 개념이 아니라, 케이스별로 스타일을 정의하여 사용하는 형태
   
```html
<html>
    <head>
        <meta content = "text/html"; charset = "utf-8"/>
        
    </head>
    <body>
        

        <p style = "font-family: 궁서; color:red">별 하나에 추억과</p>
        <p style = "font-family: 굴림; color:blue">별 하나에 사랑과</p>
        <p style = "font-family: 바탕; color:green">별 하나에 쓸쓸함</p>
        <p style = "font-family: 명조; color:yellow">별 하나에 동경과</p>
        <p style = "font-family: 고딕; color:black">별 하나에 시와</p>
        <p style = "font-family: 궁서; color:gray">별 하나에 어머니</p>



    </body>
</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163749073-8f31dffb-5c29-4861-b5f9-c9bd5cfb2a3d.png)

### CSS사용방법2
- **내부 스타일시트(Internal style sheet)**
- HTML문서내에서 <head>와 </head>사이에 스타일을 정의하는 방법
- s1(필자가 직접만듬)이라는 스타일시트로 인해서 내부가 적용이 됨 -> 특정스타일에 대한 이름을 정해줌(s1)

```html
<html>
    <head>
        <meta content = "text/html"; charset = "utf-8"/>
        <style type = "text/css">
            s1{
                font-size:16pt;
                font-family:궁서;
                color:blueviolet
            }
        </style>
    </head>
    <body>
        
        <s1>
            <p>별 하나에 추억과</p>
            <p>별 하나에 사랑과</p>
            <p>별 하나에 쓸쓸함</p>
            <p>별 하나에 동경과</p>
            <p>별 하나에 시와</p>
            <p>별 하나에 어머니</p>
        </s1>    


    </body>
</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163749481-7416218e-175f-4483-80bc-e7188601df47.png)

### CSS사용방법3
- **외부 스타일시트(External style sheet)**
- css라는 확장자를 가진 스타일 시트 파일을 만들고 이 파일을 HTML 문서에 연결하여 사용하는 방법

### 외부 스타일 시트 만들기
1. style.css 라는 파일 생성
```css
s1{
    font-size: 20pt;
    font-family: 궁서;
    color : royalblue;
}
```
2. exfont.html에 적용하기
- exont.html
```html
<html>
    <head>
        <meta content = "text/html"; charset = "utf-8"/>
        <link rel = "stylesheet" type ="text/css" href="style.css">
    </head>
    <body>
        
        <s1>
            <p>별 하나에 추억과</p>
            <p>별 하나에 사랑과</p>
            <p>별 하나에 쓸쓸함</p>
            <p>별 하나에 동경과</p>
            <p>별 하나에 시와</p>
            <p>별 하나에 어머니</p>
        </s1>    

                                                                
    </body>
</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163757379-df68d048-2701-4c82-b868-d9dfd4613142.png)

## CSS 구성요소
### 선택자(selector),속성(property),속성값(property value)
### 요소선택자
- HTML의 태그 요소들을 선택자로 사용한다 -> h1,p,img 등의 태그 요소를 사용한 선택자이다
```html
p{
    colored:red;
}
```
- p라는 요소의 선택자에 스타일을 지정하되, 색상을 red로 설정하라는 것
- color 가 속성이고, red가 속성값 의미

### 요소선택자 예제
```html
<html>
    <head>
        <meta content = "text/html"; charset = "utf-8"/>
        <style type = "text/css">
            p{
                font-size:16pt;
                font-family:궁서;
                color:blueviolet
            }
        </style>
    </head>
    <body>
        
        별 헤는 밤<br<>
            윤동주
            <p>별 하나에 추억과</p>
            <p>별 하나에 사랑과</p>
            <p>별 하나에 쓸쓸함</p>
            <p>별 하나에 동경과</p>
            <p>별 하나에 시와</p>
            <p>별 하나에 어머니</p>
            

                                                                
    </body>
</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163758419-ad7bcd9a-f172-4777-93c6-b08f7acabff7.png)

### 클래스 선택자
- 특정 문단에만 스타일이 적용되도록 하고 싶을때 사용
- 클래스 선택자는 클래스 이름 앞에 .을 붙여셔 표현
```html
jamsuham
    color:rest;
    width:300;
    fornt-sizeL:14pt;
```

### 클래스 선택자 예제
- 필요한 영역에 클래스 선택자 이용함
```html
<html>
    <head>
        <meta content = "text/html"; charset = "utf-8"/>
        <style type = "text/css">
            .star{
                
                font-family:궁서;
                color:blueviolet;
                width:300;
            }
        </style>
    </head>
    <body>
        
        
            <h1 clss = "star"> 별 헤는 밥</h1>
            <h2 class = "star">윤동주</h2>
            <p class = "star">별 하나에 사랑과</p>
            <p>별 하나에 쓸쓸함</p>
            <p>별 하나에 동경과</p>
            <p >별 하나에 어머니</p>
            <p class = "star">별 하나에 시와</p>
            

                                                                
    </body>
</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163759293-59f5550b-ba17-4a7b-8580-ee94ab550566.png)


## 배경 색상 및 이미지 처리 관련 속성
### 배경 색상

- 배경에 색상을 설정하는 속성
```html
div{
    background-color:속성값;
}
```

### 배경 색상적용 예제
```html
<html>
    <head>
        <meta content = "text/html"; charset = "utf-8"/>
        <style type = "text/css">
            div{
                background-color: aqua;
            }
        </style>
    </head>
    <body>

        <div>
            자바스크립트(영어: JavaScript)는 객체 기반의 스크립트 프로그래밍 언어이다. 이 언어는 웹 브라우저 내에서 주로 사용하며, 다른 응용 프로그램의 내장 객체에도 접근할 수 있는 기능을 가지고 있다. 또한 Node.js와 같은 런타임 환경과 같이 서버 프로그래밍에도 사용되고 있다. 자바스크립트는 본래 넷스케이프 커뮤니케이션즈 코퍼레이션의 브렌던 아이크(Brendan Eich)가 처음에는 모카(Mocha)라는 이름으로, 나중에는 라이브스크립트(LiveScript)라는 이름으로 개발하였으며, 최종적으로 자바스크립트가 되었다. 자바스크립트가 썬 마이크로시스템즈의 자바와 구문이 유사한 점도 있지만, 이는 사실 두 언어 모두 C 언어의 기본 구문에 바탕을 뒀기 때문이고, 자바와 자바스크립트는 직접적인 연관성은 약하다. 이름과 구문 외에는 자바보다 셀프나 스킴과 유사성이 많다. 자바스크립트는 ECMA스크립트(ECMAScript)의 표준 사양을 가장 잘 구현한 언어로 인정받고 있으며 ECMAScript 5(ES5)까지는 대부분의 브라우저에서 기본적으로 지원되었으나 ECMAScript 6 이후부터는 브라우저 호환성을 위해 트랜스파일러로 컴파일된다.[4]
        </div>
                                                                
    </body>
</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163759876-5493587b-9259-4af7-8b0d-1e5e16772a43.png)

### 배경 이미지 적용예제
```html
<html>
    <head>
        <meta content = "text/html"; charset = "utf-8"/>
        <style type = "text/css">
            div{
               
                background-image: url(bk.jpg)
                /*이미지 반복 출력 안되게 하는 법
                background-repeat: no-repeat;
                */
                        
               
            }
        </style>
    </head>
    <body>

        <div>
            자바스크립트(영어: JavaScript)는 객체 기반의 스크립트 프로그래밍 언어이다. 이 언어는 웹 브라우저 내에서 주로 사용하며, 다른 응용 프로그램의 내장 객체에도 접근할 수 있는 기능을 가지고 있다. 또한 Node.js와 같은 런타임 환경과 같이 서버 프로그래밍에도 사용되고 있다. 자바스크립트는 본래 넷스케이프 커뮤니케이션즈 코퍼레이션의 브렌던 아이크(Brendan Eich)가 처음에는 모카(Mocha)라는 이름으로, 나중에는 라이브스크립트(LiveScript)라는 이름으로 개발하였으며, 최종적으로 자바스크립트가 되었다. 자바스크립트가 썬 마이크로시스템즈의 자바와 구문이 유사한 점도 있지만, 이는 사실 두 언어 모두 C 언어의 기본 구문에 바탕을 뒀기 때문이고, 자바와 자바스크립트는 직접적인 연관성은 약하다. 이름과 구문 외에는 자바보다 셀프나 스킴과 유사성이 많다. 자바스크립트는 ECMA스크립트(ECMAScript)의 표준 사양을 가장 잘 구현한 언어로 인정받고 있으며 ECMAScript 5(ES5)까지는 대부분의 브라우저에서 기본적으로 지원되었으나 ECMAScript 6 이후부터는 브라우저 호환성을 위해 트랜스파일러로 컴파일된다.[4]
        </div>
                                                                
    </body>
</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163760424-ceae97af-4d67-442a-83a0-a7e9fa21f360.png)















