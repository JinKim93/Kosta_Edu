# password 객체의 사용법
![image](https://user-images.githubusercontent.com/82345970/165873690-c5db9c7d-c816-49db-a0c7-c866c9aaab6d.png)

### password 객체 예제
```html
<html>
    <head>
        <meta charset="utf-8"/>
    </head>
    <body onload = 'init()'> 
        <form name="test" onsubmit="register()" onReset="rewrite()">
            아이디:<input type="text" name="id" size="20" value="" onchange="change()"><p>
            패스워드:<input type="password" name="password" size="10" value="">
            (8자 이상 12자 이하)
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
                else if(document.test.password.value == "")
                {
                    alert('password를 입력하세요.');
                }
                else
                {
                    var pwlen = document.test.password.value.length;
                    if(pwlen < 8 || pwlen > 12)
                    {
                        alert("8자 이상 12자 이하로 입력해주세요.");
                    }
                    else
                    {
                        alert("회원 가입을 축하합니다.");
                    }
                    
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
![image](https://user-images.githubusercontent.com/82345970/165874204-50e90bd8-8463-4afd-b31d-135bd88014ea.png)
