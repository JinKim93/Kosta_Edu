## submarine 게임설계

### 게임 정보
- 해저에서 탐사하며 장애물을 피해다니는 잠수함을 구현한다.

### 구조설계
![image](https://user-images.githubusercontent.com/82345970/167980916-27681184-a549-4a09-9d77-4bf98f0841a4.png)

###
```html
<!DOCTYPE html>
<head>
    <meta charset="utf-8">
    <title>Submarine</title>
    <style>
        body{
            background-color: black;
            margin: 0px;
        }
        canvas{
            background-color: #0099FF;
        }
    </style>
</head>
<body>
    <canvas id="canvas" width="800" height="600">

    </canvas>
    <script type="text/javascript">
        //캔버스 객체
        var canvas;
        var cx;
        var canvasBuffer;
        var bifferCtx;
        var threadSpeed = 16;

        //잠수함 캐릭터 객체(변수 선언)
        var submarine;
        var sx, sy, sw = 60, sh = 35;

        //배경이미지
        var background;

        //장애물
        var enemy = new Array(); //배열의 객체만 생성(크기 등 지정 x)
        var enemyColor = ["red", "blue", "white"]; //세개의 요소가 있는 배열
        var ellapse = 10; //크기
        
        //타이머 인스턴스
        var loopInstance;

        //게임의 상태
        var STATE_START = false; //start가 안되어있는 상태로 시작(초기값)
        var STATE_GAMEOVER = false;

        //키 상태
        var keyPressed = [];

        //경과시간
        var oldTime;
        var startTime;
        var totalTime;

        //load되면 initialize함수 발생 (초기화함수)
        window.addEventListener("load", initialize, false);
        window.addEventListener("keydown", getkeydown, false);
        window.addEventListener("keyup", getkeyup, false);

        function initialize()
        {
            //canvas의 id를 가져옴
            canvas = document.getElementById("canvas")
            if(canvas == null || canvas.getContext == null)
                return;
            //ctx : 그림을 그릴 수 있는 메모리
            ctx = canvas.getContext('2d');

            //메모리 상의 element
            canvasBuffer = document.createElement("canvas");
            canvasBuffer.width = canvas.width;
            canvasBuffer.height = canvas.height;
            bufferCtx = canvasBuffer.getContext('2d');

            //게임 시작 메시지
            startMessage();

            //이미지 설정
            setImage();

            //반복 동작 설정
            loopInstance = setInterval(update, threadSpeed)

            //장애물 생성
            createObstacle();
        }

        function createObstacle()
        {
            enemy.length = 0;
            for(var i =0; i < 60; i++)
            {
                //공 한개의 정보 -> enemy배열에 저장
                enemy.push(
                    { 
                        x : Math.random() * canvas.width,
                        y : (i < 60/2 ? 20 : canvas.height-20),
                        vx : Math.random() * 200 - 100, //방향을 나타냄 -> 벡터 계산함
                        vy : Math.random() * 200 - 100,
                        color : Math.floor(Math.random() * 3)

                    }
                );
            }
        }

        function moveObstacle(ellapse)
        {
            //장애물 이동
            for(var i = 0; i < 60; i++)
            {
                var mx = enemy[i].vx * ellapse/1000;
                var my = enemy[i].vy * ellapse/1000;

                enemy[i].x = enemy[i].x + mx;
                enemy[i].y = enemy[i].y + my;

                if(enemy[i].x > canvas.width) enemy[i].x = 0;
                if(enemy[i].x < 0 ) enemy[i].x = canvas.width;          
                if(enemy[i].y > canvas.height) enemy[i].y = 0;
                if(enemy[i].y < 0 ) enemy[i].y = canvas.height;

                //충돌검사
                crashObstacle(i);
            }
        }

        function crashObstacle(idx)
        {
            var mx = enemy[idx].x;
            var my = enemy[idx].y;

            if(mx > sx-sw/2 && mx < sx + sw/2 && my > sy - sh /2 && my < sy + sh/2)
            {
                STATE_GAMEOVER = true;
            }


        }

        function getCurrentTime()
        {
            var date = new Date();
            var time = date.getTime();
            delete date;
            return time;

        }
        
        function update()
        {
            //아스키코드에서 13 = enter키
            if((keyPressed[13] == true) && !STATE_START)
            {
                startGame();
            }

            // 아스키코드에서 38은 위쪽 키 
            if(keyPressed[38])
            {
                sy = sy - 3; //한번 눌렀을때 3픽셀 올라가도록 움직이겠다
            }
            if(keyPressed[40])
            {
                sy = sy + 3; 
            }
            if(keyPressed[37])
            {
                sx = sx - 3; 
            }
            if(keyPressed[39])
            {
                sx = sx + 3; 
            }
            if(keyPressed[32] == true)
            {
                document.location.reload();
                startGame();
            }
            moveObstacle(ellapse);
            drawAll();
        }

        function setImage()
        {
            submarine = new Image();
            submarine.src = "jamsuham.png"
            background = new Image();
            background.src = "sea.jpg";
        }

        function drawText(ctx, text, x, y, font, color, align, base)
        {
            if(font != undefined) ctx.font = font;
            if(color != undefined) ctx.fillStyle = color;
            if(align != undefined) ctx.textAlign = align;
            if(base != undefined) ctx.textBaseline = base;
            ctx.fillText(text, x, y);
        }

        function startMessage()
        {
            drawText(ctx, "Enter to Start", canvas.width/2, canvas.height/2 - 60, "bold 30px ACC어린이마음고운OTF", "#ffff00", "center", "top");
            drawText(ctx, "조작 : 방향키 ←↑→↓", canvas.width/2, canvas.height/2 - 20, "bold 30px ACC어린이마음고운OTF", "#ffff00", "center", "top");
        }

        function getkeydown()
        {
            keyPressed[event.keyCode] = true;
        }

        function getkeyup()
        {
            keyPressed[event.keyCode] = false;
        }

        function drawAll()
        {
            if(!STATE_START) //게임시작 전
            {
                return;
            }
            else if(STATE_GAMEOVER) //게임 오버 되었을 때
            {
                stopGame();
                drawText(ctx, "Game over", canvas.width/2, canvas.height/2 - 60, "bold 30px ACC어린이마음고운OTF", "#ffff00", "center", "top");
                drawText(ctx, "Spacebar to Restart", canvas.width/2, canvas.height/2 - 20, "bold 30px ACC어린이마음고운OTF", "#ffff00", "center", "top");
            }
            else //게임플레이할 때
            {
                drawBg();
                drawPlayer();
                ctx.drawImage(canvasBuffer, 0, 0);

                //장애물 출력
                drawObstacle();

                //경과 시간 출력
                totalTime = (getCurrentTime() - startTime);
                drawText(ctx, totalTime, canvas.width - 10, 10, "bold 20px ACC어린이마음고운OTF", "yellow", "right", "top");
            }
        }

        function drawObstacle()
        {
            for(var i =0; i < 60; i++)
            {
                ctx.beginPath();
                ctx.arc(enemy[i].x, enemy[i].y, 5, 0, 2*Math.PI);
                ctx.fillStyle = enemyColor[enemy[i].color];
                ctx.closePath();
                ctx.fill();
            }
        }
        

        function stopGame()
        {
            STATE_START = false;
        }

        function drawBg()
        {
            //bufferCtx : 메모리DC, (0,0) : 처음부터끝까지 그리겠다
            bufferCtx.drawImage(background, 0, 0);
        }

        function drawPlayer()
        {
            bufferCtx.drawImage(submarine, sx - sw/2, sy - sh/2);
        }

        function startGame()
        {
            //게임 시작 상태
            STATE_START = true;

            //캐릭터의 초기 위치
            sx = canvas.width/2 - 18;
            sy = canvas.height/2 - 18;
            sw = 60;
            sh = 35;

            startTime = getCurrentTime();
        }

    </script>
</body>
```
