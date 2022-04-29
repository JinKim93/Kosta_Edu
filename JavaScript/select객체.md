## select 객체

### select 객체의 사용법
![image](https://user-images.githubusercontent.com/82345970/165887952-1673194d-baab-47fe-8fa1-25945afee13e.png)


### select 객체의 속성
![image](https://user-images.githubusercontent.com/82345970/165887988-f35ba3fa-3758-4c55-a52c-9492901a1729.png)

### select 객체의 메소드
![image](https://user-images.githubusercontent.com/82345970/165888002-e84bbf83-fd3a-4410-9081-9eb19ef75c44.png)

### select 객체의 이벤트
![image](https://user-images.githubusercontent.com/82345970/165888012-d2efad10-526a-4055-bc9c-47680369048c.png)

### select 객체 예제
```html
<html>
    <head>
        <meta charset="utf-8"/>
    </head>
    <body> 
        <h1>가볼만한 사이트</h1>
        <form name ="test">
            <select name = "page" onchange="changePage()" onfocus="alertMsg()" onblur="bytMsg()">
                <option value = "#">사이트 선택</option>
                <option value = "https://www.youtube.com/premium">유튜브</option>
                <option value = "https://www.naver.com/">네이버</option>
                <option value = "https://sunonline.hangame.com/event/20160303_update/">썬온라인</option>
            </select>


        </form>
        <script type="text/javascript">
            function changePage()
            {
                var obj = document.test.page;
                location.href = obj.options[obj.selectedIndex].value; //선택된 인덱스가 누구냐
            }
     
        </script>
    </body>
</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165889198-641b2bf9-d433-41c6-a60b-2ce83013dcac.png)

