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
- **내부스타일시트(Internal style sheet)**
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
- **외부스타일시트(External style sheet)**
