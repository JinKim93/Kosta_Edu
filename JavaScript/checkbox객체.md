## checkbox객체

### checkbox 객체의 사용법
![image](https://user-images.githubusercontent.com/82345970/165876836-bc153072-f923-4ad4-a7a1-ef378a3f1278.png)

### checkbox 객체의 속성
![image](https://user-images.githubusercontent.com/82345970/165876888-1d4b6663-0c38-4fd0-aac5-32f0ec1e433e.png)

### checkbox 객체의 메소드
![image](https://user-images.githubusercontent.com/82345970/165876906-eab09f1f-f5c9-494f-a142-b781268600b5.png)

### checkbox 객체의 이벤트
![image](https://user-images.githubusercontent.com/82345970/165876931-e340c876-827b-4fe5-ab6c-42e154657c95.png)

### checkbox 예제
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
            하고 싶은 말 : <p><textarea name ="diary" rows ="7" cols = "50"></textarea></p> 
            <hr>
            <h2>개인 정보 동의(필수)</h2><p>
            <input type="checkbox" name="chk1" value="1">개인정보 수집<p>
            <input type="checkbox" name="chk2" value="2">개인정보 조회<p>
            <input type="checkbox" name="chk3" value="3">개인정보 제공<p>
            <hr>

            <input type="submit" name="btn1" value="등록하기">
            <input type="reset" name="btn2" value="다시작성">
            <input type="button" name = "btn3" value="전체선택" onclick="selectAll()">
            <input type ="button" name ="btn4" value="버튼이름 바꾸기" onclick="changeName()">

        </form>


        <script type="text/javascript">
            var bToggle = true;

            function changeName()
            {
                if(bToggle)
                {
                    document.test.btn1.value = "안등록하기";
                    bToggle = false;
                }
                else
                {
                    document.test.btn1.value = "등록하기";
                    bToggle = true;
                }
                
            }

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
            function register()
            {
                var check1 = document.test.chk1.checked;
                var check2 = document.test.chk2.checked;
                var check3 = document.test.chk3.checked;


                
                if(document.test.id.value == "")
                {
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
                        if(check1&check2&check3)
                        {
                            alert("회원 가입을 축하합니다.");     
                        }
                        else
                        {
                            alert('모든 항목을 체크하여 주십시오.');
                        }
                        
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
![image](https://user-images.githubusercontent.com/82345970/165878154-940b826e-cc4b-4aad-8bbd-988948015cbf.png)
