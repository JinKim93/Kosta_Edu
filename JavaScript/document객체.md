## document 객체
- document 객체
- anchor 객체
- link 객체

### document 객체 속성
![image](https://user-images.githubusercontent.com/82345970/165657231-4c2a2b07-76a2-4012-9dfa-cdfbae5acb20.png)

### document 객체 예제
- 배경색, 글자색 변경
 
```html
<html>
    <head>
        <meta charset="utf-8">
    </head>
    <body>
        <script type ="text/javascript">
            var colorValue;

            function backColor()
            {
                colorValue = document.getElementById("colorValue");
                document.bgColor = colorValue.value;
            }
            
            function textColor()
            {
                colorValue = document.getElementById("colorValue");
                document.fgColor = colorValue.value;
            }
        </script>
        <h1>배경색과 글자색을 변경합니다.</h1>
        색상 입력 : <input type = "text" id = "colorValue" value=""><p>
        <button onclick="backColor()">배경색 변경하기</button>           
        <button onclick="textColor()">글자색 변경하기</button>             
    </body>
</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165658528-12aee5d4-094b-48d9-bd2a-3cab099cc6ef.png)

### document 객체 예제 
```html
<html>
    <head>
        <meta charset="utf-8">
    </head>
    <body>
        <script type ="text/javascript">
            
            function chagneTitle()
            {
                var docValue = document.getElementById("titleValue");
                document.title =  docValue.value;
            }
            function printInfo()
            {
                var docInfo = "문서가 최근 바뀐 날짜 : " + document.lastModified + "\n\n" 
                + "현재 URL : " + document.URL + "\n\n"      
                + "문서 제목 : " + document.title + "\n\n";   
                alert(docInfo);
                
            }
        </script>
        <h1>문서 타이틀 변경 및 문서 정보 출력하기</h1>
        타이틀 입력 : <input type = "text" id = "titleValue" value="새문서"></p>
        <button onclick="chagneTitle()">타이틀 변경하기</button>           
        <button onclick="printInfo()">문서 정보 출력하기</button>             
    </body>
</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165661656-a31ef6ea-c367-4652-857a-f59ed81397d7.png)

### document 객체 메소드
![image](https://user-images.githubusercontent.com/82345970/165661786-025ba6c1-ee10-498b-8853-04ad1506fe3f.png)


### document 객체 메소드 예제
```html
<html>
    <head>
        <meta charset = "utf-8">
    </head>
        <body>
            <script type = "text/javascript">
                var newWin;
                function newOpen()
                {
                    newWin = window.open('','','width = 350, height = 600');
                    newWin.document.open(); 
                    newWin.document.write("<h1><center>이달의 베스트셀러</center></h1>");
                    newWin.document.write("<img src = 'cake.jpg' width = 330 height = 460>");
                    newWin.document.close();
                }
                function newClear()
                {
                    newWin.document.open();
                    newWin.document.clear();
                    newWin.document.close();
                }
            </script>
            <h1> 새 문서 직접 만들기</h1>
            <button onclick = "newOpen()">새 문서 열기</button>
            <button onclick = "newClear()">문서 지우기</button>
        </body>
    
</html>
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165668206-45f46d0c-ec4b-47d4-b1d0-a1ff1364ef3c.png)


### document 객체 메소드
- 문자열 안에 문자열 출력하기

![image](https://user-images.githubusercontent.com/82345970/165664959-8ba55cfd-53f2-4774-9d91-32ee16b2580b.png)

### anchor 객체 속성
![image](https://user-images.githubusercontent.com/82345970/165665237-cd055bc6-d3f1-4e99-b739-8e7f010d3218.png)

### anchor 객체 속성 예제
```html
<html>
    <head>
        <meta charset="utf-8">
    </head>
    <body>
        <a href = "#MFC">MFC 시스템 프로그래밍</a><p>
        <a href ="#API">API 프로그래밍</a>    
        <a href ="#C++">C++ 프로그래밍</a>
        <br><br><br><br><br><br><br><br><br><br><br><br>  
        <a name = "MFC">MFC 시스템 프로그래밍</a><p>
        <img src = "cake.jpg"><br><br>
        <a name = "API">MFC 시스템 프로그래밍</a><p>
        <img src = "bread.jpg"><br><br>
        <a name = "C++">MFC 시스템 프로그래밍</a><p>
        <img src = "bread.jpg"><br><br>

        <script type ="text/javascript">
            document.write("<h1>anchor의 개수 : " + document.anchors.length + "<h1><br>")
            
                for(var i =0; i < document.anchors.length; i++)
                {
                    document.write("<h1>" + document.anchors[i].name + "</h1><br>")
                }

        </script>
      
               
    </body>
</html>
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165668008-f46fa131-fb4e-45fa-b74d-f946b8748768.png)

### write()함수 vs writeln()함수
- \<pre>태그를 써줘야 됨

```html
<html>
    <head>
        <meta charset = "utf-8">
    </head>
        <body>
            <pre>
            <script type = "text/javascript">
                //write() 메소드
                document.write("<h1>write() 메소드 </h1>");
                document.write("<h2>별 하나에 추억과</h2>");
                document.write("별 하나에 사랑과");
                document.write("별 하나에 쓸쓸함과<p>");

                //writeln() 메소드
                document.writeln("<h1>writeln() 메소드 </h1>");
                document.writeln("<h2>별 하나에 추억과</h2>");
                document.writeln("별 하나에 사랑과");
                document.writeln("별 하나에 쓸쓸함과<p>");  
    
            </script>
            </pre>
        </body>
    
</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165669683-903aba6f-cf48-443e-8e0d-866fc820b79e.png)

### link 객체 
![image](https://user-images.githubusercontent.com/82345970/165670069-c988e456-79e1-4e04-ac8b-55cc601f7a5f.png)

### link 객체 예제
```html
<html>
    <head>
        <meta charset = "utf-8">
    </head>
        <body>
            <a href = "https://www.youtube.com/premium" target = "_blank">유튜브</a><br>
            <a href = "https://gyoogle.dev/blog/" target = "_blank">기술블로그</a><br>
            <a href = "https://www.nate.com/" target = "_blank">네이트</a><br>
            <hr>
            <script type = "text/javascript">
                for(var i =0; i < document.links.length; i++)
                {
                    document.write("<h1>href : " + document.links[i].href  + "<br><hr>");
                    document.write("pathname : " + document.links[i].pathname  + "<br><hr>");
                    document.write("target : " + document.links[i].target  + "<br><hr></h1>");
                }
                
            </script>
           
        </body>
    
</html>
 ```
 
 ### 출력결과
 ![image](https://user-images.githubusercontent.com/82345970/165678417-9cc67e1c-b04c-4fe7-ac79-ed48523bd064.png)

### image 객체 속성
- **image 객체를 사용하는 형태**
  - image 객체는 \<img> 태그와 같은 이미지 요소들과 연관
  - \<img> 태그와 같이 문서 상에 삽입된 이미지를 모두 탐색
  - image 정보는 배열 형태로 저장 

![image](https://user-images.githubusercontent.com/82345970/165678731-d5f088dd-194f-4613-a66d-321bdf0fe8b5.png)

### image 객체 속성
![image](https://user-images.githubusercontent.com/82345970/165678771-7719eadb-3e8a-45e9-81a7-91cd0b35bc42.png)

### image 객체 속성 예제
```html
<html>
    <head>
        <meta charset = "utf-8">
    </head>
        <body>
          <h1><center>베스트셀러</center></h1>
          <hr>

          <img src = "cake.jpg">
          <img src = "bread.jpg">
          <img src = "contact.png">
          <hr>
            <script type = "text/javascript">
                document.write("image 개수 : " + document.images.length + "<br>");

                for(var i = 0; i < document.images.length; i++)
                {
                    document.images[i].border = 10;
                    document.images[i].width = "210";
                    document.images[i].height = "300";

                }
                for(var i =0; i < document.images.length; i++)
                {
                    document.write("파일 경로 : " + document.images[i].src + "<br>");
                    document.write("넓이 : " + document.images[i].width + "<br>");
                    document.write("높이 : " + document.images[i].height + "<br>");
                }

               

            </script>
           
        </body>
    
</html>
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165679706-073d67e1-aeb1-46f8-8e80-b1974956cd86.png)

### 폼 객체 
- 폼 형태는 대표적으로 회원 가입 페이지를 보면 됨
- 자바스크립트를 이용하여 각 필드의 요소들을 제어할 수 있다.

### 폼 객체
- 폼 객체는 document 객체의 하위에 있는 내장 객체로써 기존 \<form> 태그를 자바스크립트로 정의 한것
```html
document.폼 이름.속성(메소드)
```

###  폼 객체의 계층 구조도
![image](https://user-images.githubusercontent.com/82345970/165680308-a2dda2d0-9a0f-4fa1-995e-ba0ec361d4f2.png)

### 폼 객체의 속성
![image](https://user-images.githubusercontent.com/82345970/165680490-8e2fe009-7a5d-49fd-97d9-717b061ca027.png)

### 폼 객체 예제
```html
<html>
    <head>
        <meta charset = "utf-8">
    </head>
        <body>
            <form name ="test" method="get">
                <input type = "text" name = "text1" size = "20" value="첫 번쨰 입력"><p>
                <input type = "text" name = "text2" size = "10" value="두 번쨰 입력"><p>
                <input type = "button" name = "btn1" value="첫 번째 버튼">
                <input type = "button" name = "btn2" value="두 번째 버튼">
            </form>
         
            <script type = "text/javascript">
                           
                document.write("name : " + document.test.name + "<p>");
                document.write("method : " + document.test.method + "<p>");
                document.write("length : " + document.test.length + "<p>");
                 
                    for(var i =0; i < document.test.length; i++)
                    {
                        document.write("elements[x].name : " + document.test.elements[i].name + "<p>");
                        document.write("elements[x].value : " + document.test.elements[i].value + "<p>");
                    }
                

         
            </script>
           
        </body>
    
</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165682235-877449f7-6ca8-4d8b-8395-20cb5432c364.png)

### 폼 객체의 메소드
- 폼 양식을 보면 '등록' 버튼과 '다시작성' 버튼이 배치 됨
- 등록은 \<submit> 다시작성은 \<reset> 태그를 사용함

![image](https://user-images.githubusercontent.com/82345970/165682532-54070224-c203-492d-9f15-28e69852f1eb.png)

- 이벤트 핸들러를 직접 작성하여 submit() 메소드를 호출
- action으로 지정한 루팅이 없기 때문에 실제 등록처리를 하지는 않는다
