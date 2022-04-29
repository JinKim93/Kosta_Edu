### text 객체의 메소드
![image](https://user-images.githubusercontent.com/82345970/165871896-5c754aee-a5a8-4262-9c18-1d6e886f3743.png)

### text 객체의 메소드(focus 예제)
```html
<html>
    <head>
        <meta charset="utf-8"/>
    </head>
    <body onload = 'init()'> 
        <form name="test" onsubmit="register()" onReset="rewrite()">
            아이디:<input type="text" name="id" size="20" value=""><p>
            패스워드:<input type="password" name="password" size="10" value="">
            <p>
            <input type="submit" name="btn1" value="등록하기">
            <input type="reset" name="btn2" value="다시작성">

        </form>


        <script type="text/javascript">

            function init()
            {
                document.test.id.focus();
            }
            function register(){
                
                if(document.test.id.value == ""){
                    alert('ID를 입력하세요.');
                }
                else if(document.test.password.value == ""){
                    alert('password를 입력하세요.');
                }
                else{
                    alert("회원 가입을 축하합니다.");
                }
            }
            function rewrite(){
                alert("다시 입력하세요");
            }
        </script>
    </body>
</html>
```

### 출력결과
- 아이디 부분 이벤트 발생하면, 커서 깜빡 깜박 한다
 
![image](https://user-images.githubusercontent.com/82345970/165872453-f95c1edc-c9e3-4d85-9eaa-3dfc5d34319c.png)

### text 객체의 이벤트
![image](https://user-images.githubusercontent.com/82345970/165872827-645febd8-9364-4da9-b426-a7a3c345d0ff.png)

### text 객체의 이벤트(onchange 예제)
```html
<html>
    <head>
        <meta charset="utf-8"/>
    </head>
    <body onload = 'init()'> 
        <form name="test" onsubmit="register()" onReset="rewrite()">
            아이디:<input type="text" name="id" size="20" value="" onchange="change()"><p>
            패스워드:<input type="password" name="password" size="10" value="">
            <p>
            <input type="submit" name="btn1" value="등록하기">
            <input type="reset" name="btn2" value="다시작성">

        </form>


        <script type="text/javascript">

            function init()
            {
                document.test.id.focus();
            }

            function change()
            {
                alert("ID가 변경되었습니다.")
            }
            function register(){
                
                if(document.test.id.value == ""){
                    alert('ID를 입력하세요.');
                }
                else if(document.test.password.value == ""){
                    alert('password를 입력하세요.');
                }
                else{
                    alert("회원 가입을 축하합니다.");
                }
            }
            function rewrite(){
                alert("다시 입력하세요");
            }
        </script>
    </body>
</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165872893-8819a200-0840-4132-bbdb-90b22de5dc4b.png)

