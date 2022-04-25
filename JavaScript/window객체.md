## window 객체
- 객체 계층 구조의 최상위에 존재
- 윈도우나 프레임을 의미
- Window 객체를 기점으로 document 객체, navigator 객체, object 객체와 같은 하위 객체들이 갈라져 나옴
![image](https://user-images.githubusercontent.com/82345970/165024742-5ce47150-5ccc-4da6-a1a4-1d8c47b37f72.png)

- alert()함수 사용 시, window.alert()와 같이 사용해야함
- 계층구조 상 window.document.write() 사용해야 하지만 window는 생략하고, document.write()라고 사용한다

## window 객체 메소드
- 윈도우 열기- open() 메소드

![image](https://user-images.githubusercontent.com/82345970/165027844-8e976221-1900-4d0f-8b23-55d1dd89f63e.png)

### 실습
1. test.html 새 파일 작성 -> 
2. open.html
```html
<html>
    <head>
        <meta charset="utf-8">
    </head>
    <body>        
        
                 
        <script type = "text/javascript">
         
        var newWin;
        function newOpen()
        {
            newWin = window.open('test.html','new','width = 600, height = 300');
        }

        function winClose()
        {
            //window.close();
            newWin.close();
        }
        </script>
        <button onclick="newOpen()">새 윈도우 열기</button>
        <button onclick="winClose()">윈도우 닫기</button><p>


    </body>


</html>
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165029533-1425b52b-8c05-4b1e-88a1-f49d1382da84.png)

## window 객체메소드
### 일회성 시간 기능
- 일회성 사용 메소드로는 setTimeout()과 claerTimeout() 두가지 있다
- setTimeout() 메소드는 설정한 시간 이후 특정 기능을 수행하도록 한다
```html
timerID = window.setTimeout(함수 또는 명령,시간)
```
- clearTimeout() 메소드는 setTimeout() 기능을 무력화 시킴
```html
window.clearTimeout(timerID)
```

### 실습
```html
<html>
    <head>
        <meta charset="utf-8">
    </head>
    <body>        
        
                 
        <script type = "text/javascript">
         var timeID;
         function timeStart()
         {
            // alert('시한 폭탄 설정');
            timeID = window.setTimeout(function(){
                alert('꽝');
            }, 5000); // 5초 설정 -> 5초가 지나면 alert 수행
         }
         function timeStop()
         {
             window.clearTimeout(timeID);
            alert('폭탄이 해제되었습니다.');
         }
            
         </script>
         <button onclick="timeStart()"> 시한 폭탄 설정</button>
         <button onclick="timeStop()">시한 폭탄 해제</button>
    </body>


</html>
```

### 출력결과
- 시한 폭탄 설정 버튼 클릭 후 5초 지나면 꽝 
- 5초 전에 시한 폭탄 해제 누르면 alert -> 시한 폭탄 해제 알림창 

![image](https://user-images.githubusercontent.com/82345970/165031846-97e570a1-0a06-4f7d-80bd-9caab10dca20.png)


### setInterval() 타이머
```html
<html>
    <head>
        <meta charset="utf-8">
    </head>
    <body>        
        
                 
        <script type = "text/javascript">
            var timeID;
            var count = 0;

            function timestart()
            {
                timeID = window.setInterval(function(){
                    document.getElementById("result").innerHTML = count++;
                }, 100);
            }
            function timestop()
            {
                window.clearInterval(timeID);
            }
            
         </script>
         <button onclick="timestart()">카운트 시작</button>
         <button onclick="timestop()">카운트 중지</button><p>
         <h1><div id ="result"></div></h1>         
    </body>


</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165036081-d8ba7e30-1386-4a5d-b97c-7ff4c3be35e3.png)

### window 객체 이벤트
![image](https://user-images.githubusercontent.com/82345970/165036478-f92aa0b6-56cd-4eef-828a-a58abdeace40.png)

### 2개이상 이벤트핸들러 등록 가능 실습
- 문서모드는 최초 1번만 실행
```html
<html>
    <head>
        <meta charset="utf-8">
    </head>
    <body onload="myLoad()" onblur="myBlur()">        
        
                 
        <script type = "text/javascript">
          function myLoad()
          {
            alert("문서를 로드했습니다")
          }
          function myBlur()
          {
            alert("포커스를 잃었습니다")
          }
            
         </script>
         <h1>Window 객체에서 제공하는 이벤트</h1>
      
    </body>


</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165037630-ff510061-a4ae-45dc-8e86-2fa367ad11b9.png)

![image](https://user-images.githubusercontent.com/82345970/165037666-f23e4676-1a53-479a-a161-f6377043e60d.png)


