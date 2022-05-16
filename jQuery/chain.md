## chain이란
- 제이쿼리의 메소드들은 반환값을 자기 자신을 반환해야 하는 규칙
- 한 번 선택한 대상에 대해 연속적인 제어가 가능
- 제이쿼리로 작성한 체인

### 제이쿼리와 자바스크립트의 코드 비교(Jquery)
- **한번 선택한 element(tutorial)에 대해서 연속적으로 요소제어(attr) 가능 함 -> 이런걸 chain이라고 부름**
 
```html
<html>
    <head>
        <title>Jquery 이용</title>
        <script src = "http://code.jquery.com/jquery-latest.min.js"></script>
         
    </head>
    <body>
        <a id = "tutorial" href ="http://jquery.com" target = "_self">jQuery</a>
        <script type = "text/javascript">
            jQuery('#tutorial').css("color", "red").attr('target','_blank').attr('href','https://www.naver.com'); //새창에서 나오도록 설정 -> _blank
        </script>
    </body>
</html>
```

### 제이쿼리와 자바스크립트의 코드 비교(자바스크립트)
```html
<html>
    <head>
        <title>javascript 이용</title>
        <script src = "http://code.jquery.com/jquery-latest.min.js"></script>
         
    </head>
    <body>
        <a id = "tutorial" href ="http://jquery.com" target = "_self">jQuery</a>
        <script type = "text/javascript">
            let tutorial = document.getElementById('tutorial');
            tutorial.setAttribute('href','https://www.naver.com');
            tutorial.setAttribute('target','_blank');
            tutorial.style.color = 'red';
        </script>
    </body>
</html>
```

### chain 장점
- 코드가 간결해짐
- 인간의 언어와 유사하게 사고의 자연스러운 과정과 일치<br> (주어 + 서술어 + 서술어..) : 여러 개의 서술어가 가능
- **제이쿼리 관점** : 나는 밥을 먹으면서 TV를 보았다
- **자바스크립트 관점** : 나는 밥을 먹는다. 나는 TV를 본다

## 탐색이란
- chain의 대상을 바꿔서 체인을 계속 연장시킬 수 있는 방법
- 너무 복잡한 chain은 코드의 가독성을 떨어뜨릴 수 있다

### 탐색 예제
```html
<html>
    <head>
        <title>Traverse</title>
        
         
    </head>
    <body>
        <ul class = "first">
            <li class = 'foo'>list item 1</li>
            <li>list item 2</li>
            <li class = "bar">list item 3</li>
        </ul>

        <ul class = "second">
            <li class = 'foo'>list item 1</li>
            <li>list item 2</li>
            <li class = "bar">list item 3</li>
        </ul>

        <script src = "http://code.jquery.com/jquery-latest.min.js"></script>
        <script type = "text/javascript">
            $('ul.first').find('.foo').css('background-color', 'red').end().find('.bar').css('background-color', 'green');
            
            
        </script>
    </body>
</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/168507958-cebd4a0b-4b78-483e-9856-21155cf0a98a.png)


