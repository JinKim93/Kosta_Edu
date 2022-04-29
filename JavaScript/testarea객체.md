## testarea 객체

### testarea 객체의 사용법
![image](https://user-images.githubusercontent.com/82345970/165874875-ad1b8774-2b5a-4840-80f1-bf7be218adf5.png)

### textarea 객체의 속성
![image](https://user-images.githubusercontent.com/82345970/165874595-a5008205-dae7-4659-8d01-9f3a3343638f.png)

### textarea 객체의 메소드
![image](https://user-images.githubusercontent.com/82345970/165874693-c7451c4d-bdc7-49be-8c39-6f3adafc360e.png)

### textarea 객체의 이벤트
![image](https://user-images.githubusercontent.com/82345970/165874835-ff588a05-ee9f-4c7e-8a8b-e4ce032cb350.png)


### textarea 객체 예제
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
            하고 싶은 말 : <P><textarea name ="diary" rows ="7" cols = "50"></textarea></P> 
            <input type="submit" name="btn1" value="등록하기">
            <input type="reset" name="btn2" value="다시작성">
            <input type="button" name = "btn3" value="전체선택" onclick="selectAll()">

        </form>


        <script type="text/javascript">
            function selectAll()
            {
                document.test.diary.select(); // 전체선택 버튼
            }

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
![image](https://user-images.githubusercontent.com/82345970/165875141-426049be-be48-47db-ba31-b3bed825a958.png)
