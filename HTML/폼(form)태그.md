## 폼(form)태그
- 폼 태그는 텍스트 필드, 라디오 버튼, 체크 박스, 전송 버튼 등이 위치하게 함
- 사용자가 브라우저에 입력한 정보를 submit 버튼을 누르면 지정한 url로 정보를 전송

```html
<form method = "get" action = "confirm.php">
</form>
```

## 폼 태그 속성
- 폼은 사용자로부터 입력한 데이터를 처리해야 하기 때문에 기본적으로 통신방식을 설정하고, 처리하는 루틴을 읽어와야함
- **method** : 통신방법을지정, **get,post**방식 두가지가 있다.<br/>**get 방식**은 1KB이상의 데티러를 처리할때 사용, **post방식**은 1KB미만의 데이터를 처리할때 사용 
- **action** : 입력된 정보를 처리하는 프로그램의 경로를 지정

## 입력(input)태그
- 입력태그는 입력 양식 중 가장 기본적인 형태로 타입 속성값에 따라 여러가지 형태로 출력을 할수 있다 

## 입력 태그 속성
![image](https://user-images.githubusercontent.com/82345970/163739700-1df6f1e3-54e7-4f34-a080-dc9a4d017141.png)

### 텍스트(Text) 필드
- 임의의 문자를 입력 받을 때 사용하는 필드
```html
<input type="text" name="my_id">
```
- type 속성은 비단 텍스트 필드 뿐만 아니라 , 폼 태그 내에서는 필수적 속성
 
### 텍스트(Text) 필드 부가적 속성
![image](https://user-images.githubusercontent.com/82345970/163739784-51662907-4835-4386-8dff-d81a1591ea10.png)

### 텍스트(Text) 필드 예제
- maxlength="8" 8글자까지 작성할수 있게 설정
```html
<html>
    <head>
        <meta content = "text/html"; charset="utf-8"/>
    </head>

    <body>
        <form method="get" action="">
            아이디 : 
            <input type = "text" name = "my_id" size = "30" maxlength="8"
                value="이름을 입력하세요">
            비밀번호 : 
            <input type = "password" name = "my_pwd" size = "30" maxlength="15"
                value="비밀번호을 입력하세요">
                
        </form>


    </body>

</html>
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163740280-78698538-9e0d-4b33-8248-8bfb208150f2.png)

### 체크박스 만들기
- 출력결과에서 checked 작성 한거랑, 안 한거 비교해보기
```html
<html>
    <head>
        <meta content = "text/html"; charset="utf-8"/>
    </head>

    <body>
        <form method="get" action="">
            아이디 : 
            <input type = "text" name = "my_id" size = "30" maxlength="8"
                value="이름을 입력하세요"><p>
            비밀번호 : 
            <input type = "password" name = "my_pwd" size = "30" maxlength="15"
                value="1111"><p>
            
            * 평소에 선호하는 언어의 종류를 고르시오 <p>
            <input type = "checkbox" name = "cb1" value= "C++" >C++
            <input type = "checkbox" name = "cb2" value= "자바" >자바
            <input type = "checkbox" name = "cb3" value= "아랍어" >아랍어
            <input type = "checkbox" name = "cb4" value= "자바스크립트" >자바스크립트
            <input type = "checkbox" name = "cb5" value= "파이썬" checked>파이썬        
                
        </form>


    </body>

</html>
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163740731-ddae38ca-004d-4b36-b51b-5e686f88f082.png)

