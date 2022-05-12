## submarine 게임설계

### 게임 정보
- 해저에서 탐사하며 장애물을 피해다니는 잠수함을 구현한다.

### 구조설계
![image](https://user-images.githubusercontent.com/82345970/167980916-27681184-a549-4a09-9d77-4bf98f0841a4.png)

###
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Submarine</title>
        <style>
            body{
                background-color: #000000;
                margin:0px;
            }
            canvas{
                background-color: #0099FF;
            }
        </style>
    </head>
    <body>
        <canvas id = "canvas" width = "800" height = "600">

        </canvas>
        <script type = "text/javascript">
           //캔버스 객체
           var canvast;
           var ctx;
           var canvasBuffer;
           var bufferCtx;
           var threadSpeed = 16;

           //잠수함
           var submarine;
           var sx, sy, sw, sh = 35; //sx, sy 서브마린좌표, sh 높이 

           //배경이미지
           var background;


           //장애물
           var enemy = new Array();
           var enemyColor = ["red", "blue", "white"];
           var ellapse = 10;

           //타이머 인스턴스
           var loopInstance;

           //게임의 상태
           var STATE_START = false;
           var STATE_GAMEOVER = false;

           //키 상태
           var keyPressed = [];

           //경과시간
           var oldTime;
           var startTime;
           var totalTime;

           window.addEventListener("load", initialize, false);
           window.addEventListener("keydown", getKeyDown, false);
           window.addEventListener("keyup", getKeyUp, false);

           
        </script>
    </body>
</html>
```
