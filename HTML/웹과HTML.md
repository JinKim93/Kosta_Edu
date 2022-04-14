### 웹
- www(World Wide Wdb)

### 웹 VS 인터넷
- **인터넷**은 서비스로써 내 컴퓨터를 인터넷의 바다로 항해하도록 하는 물리적 망
- **웹**은 인터넷 망 서비스 중에 하나로 www,텔넷,FTP 등 의 서비스들이 있다

### HTML
- Hypertext Markup Langueage
- 하이퍼텍스트(문서간 이동가능) 와 마크업의 속성을 가진 언어
- 마크업 -> 문서의 실제 내용에 관한정보가 아니라, 문서내 의 표나 그림에 대한배치, 글자에대한 간격, 여백 등에 대한 정보

### visual studio code 설치
- visual studio code -> extension에서 하기 목록 다운 
- ESLint
- CSS peek
- HTML CSS Expport
- open in browser 


### HTML
```html
<html>
    <head>
        
    </head>

    <body>
        Hello HTML
    </body>

</html>
```

### 브라우저 출력결과
![image](https://user-images.githubusercontent.com/82345970/163315383-b64e673a-3522-4103-bde2-175b4ec9c01b.png)

### 태그(Tag)란
- 사전적 의미로 꼬리표
- 브라우저 상에 보여지지는 않지만 특정한 기능을 가진 문자를 태그(Tag)라 부른다

### 태그의 기본형태

```html
<태그 이름>
```

### HTML 기반 태그

```html
<html> ~ </html> HTML 문서으 시작과 끝을 알리는 태그
<head> ~ </head> HTML 문서의 정보를 담고 있는 부분
<body> ~ </body> HTML 문서로 보면 실제 문서상에 보여지는 모든 기능들을 처리 -> 실제로 수많은 태그들이 사용 
```

### \<i> 태그
- 이탤릭체

```html
<html>
    <head>

    </head>

    <body>
        Hello <i>HTML</i>
    </body>

</html>
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163318218-29b2eb08-63fc-4cfd-aee3-b4badbe6ba75.png)

### \<u> 태그
- 밑줄

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163318679-0f457e37-f14e-4858-abc1-db21f4e31706.png)

### \<mark> 태그
- 형광표시

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163318907-0d347cf3-caa1-4d27-a4b7-e4df1e262afa.png)

### meta 태그
- meta 태그의 charset 속성은 해당 HTML 문서의 문자 인코딩

```html
<html>
    <head>
        <meta content = "text/html"; charset="utf-8"/>
    </head>

    <body>
        Hello <mark>HTML</mark>
    </body>

</html>
```

### \<sub> 태그
- 아래첨자

```html
<html>
    <head>
        <meta content = "text/html"; charset="utf-8"/>
    </head>

    <body>
        안녕하세요 저는 H<sub>2</sub>O를 먹고 삽니다. <br/>
        2<sup>3</sup> = 8
    </body>

</html>
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163319491-df5fb8ab-43c9-4dcb-9732-9384d65d026d.png)


### \<sup> 태그
- 위 첨자

```html
<html>
    <head>
        <meta content = "text/html"; charset="utf-8"/>
    </head>

    <body>
        
        2<sup>3</sup> = 8
    </body>

</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163319577-ad4c6efb-709d-4871-b4ec-b89c670edd4c.png)

### \<blockquote> 태그
- 인용구

```html
<html>
    <head>
        <meta content = "text/html"; charset="utf-8"/>
    </head>

    <body>
       
        나는 직원들에게 말했다.

        <blockquote>"안녕히 계세요 여러분, 저는 이제 굴와 속박에서 벗어나 자유를 찾아 떠납니다"
        </blockquote>  
        그리고 떠났다.
    </body>

</html>
```

### 출력결과

![image](https://user-images.githubusercontent.com/82345970/163319878-7a2d7701-5579-4e84-8c43-ef2ec375313c.png)

### \<Marquee> 태그
- 텍스트 상하좌우로 움직이는 태그
```html
<html>
    <head>
        <meta content = "text/html"; charset="utf-8"/>
    </head>

    <body>
     <Marquee>세월은 오른쪽에서 왼쪽으로 흘러간다</Marquee>  
     
    </body>

</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163325031-c8f29ee2-b004-4e75-bb3b-145245b5f5dc.png)

### \<p> 태그
- 단락을 띄어줌
- 문단과 문단을 띄어줌

```html
<html>
    <head>
        <meta content = "text/html"; charset="utf-8"/>
    </head>

    <body>
        그리고 나한테 주어진 길을 걸어가야겠다<p>
        오늘밤에도 별이 바람에 스치운다</p>  
     
    </body>

</html>
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163325651-7526fc63-078c-48d8-a96b-8680e83d9410.png)

### \<br> 태그
- 개행문자

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163325795-9ec4ee25-fab3-4ce9-8694-8e2cca9e83ac.png)

### &nbsp
- 띄어쓰기(스페이스바 한번 클릭)
- 5칸 띄어쓰기 하고 싶으면 5번 작성하면된다

```html
<html>
    <head>
        <meta content = "text/html"; charset="utf-8"/>
    </head>

    <body>
        HTML과 CSS &nbsp&nbsp&nbsp자바스크립트
     
    </body>

</html>
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163326456-45239b96-076d-4de9-8dbd-db7bcddc2299.png)


