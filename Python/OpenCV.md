# OpenCV
- Opencv(open source Computer Vision)는 실시간 컴퓨터 비전을 처리하는 목적
- 크로스 플랫폼 라이브러리(윈도우,리눅스,Mac에서 무료로 사용)
- 기본적으로 c++로 작성
- 이미지, 영상처리, MotionDetection 등 다양항 기능을 제공
- 물체인식, 안면인식, 모바일 로보틱스, 제스쳐인식, 자율주행 등 응용
- 이미지 딥러닝에 많이 활용됨
### 모듈설치
- 터미널(CMD창)에서 **pip install opencv-python** 입력

### 버전확인
```py
import cv2
print(cv2.__version__)
```
![image](https://user-images.githubusercontent.com/82345970/163936551-eb02fb7c-9998-4d96-8329-04a7b549f38e.png)


### 이미지 읽는 함수imread()
![image](https://user-images.githubusercontent.com/82345970/163938070-62f55c8a-5938-4ef3-8959-1b0b4fc84aee.png)

### 이미지 읽기
```py
import cv2

img = cv2.imread('12.jpg',1)
cv2.imshow('Test image',img)
cv2.waitKey(0)
cv2.destroyWindow()
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163938342-5a924b4d-ad2b-43f9-9e68-89fa2fb83760.png)


### 이미지 읽기
```py
import cv2

img1 = cv2.imread('12.jpg',1)
img2 = cv2.imread('12.jpg',cv2.IMREAD_GRAYSCALE)
cv2.imshow('Test image1',img1)
cv2.imshow('Test image2',img2)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163938761-fd66b1d3-4445-4735-8bef-8d0639f7f4b8.png)


### 이미지 쓰기

```py
import cv2

img1 = cv2.imread('12.jpg',1)
img2 = cv2.imread('12.jpg',cv2.IMREAD_GRAYSCALE)
cv2.imshow('Test image1',img1)
cv2.imshow('Test image2',img2)
cv2.waitKey(0)
cv2.destroyAllWindows()

cv2.imwrite('test2.png',img1)
```

### 출력결과
- 사진 복사됨
![image](https://user-images.githubusercontent.com/82345970/163939098-22b8cb16-c91f-4cad-b115-646649d21c2e.png)

## 카메라 영상 처리
![image](https://user-images.githubusercontent.com/82345970/163939427-efdbd10b-b457-44e9-849e-ebab88ecb94d.png)

### 카메라 영상처리 예제
```py
import cv2

cap = cv2.VideoCapture(0) # cap = new cv2.VideoCapture(0) 첫번재 카메라 객체 받음

while cap.isOpened():
    #카메라 프레임 읽기
    success, frame = cap.read() # cap이라는 객체를 통해서 frame을 읽음
                                # success, frame 리턴값 2개 받음
    if success:
        #프레임 출력
        cv2.imshow('Camera Window', frame)

        #ESC 종료
        key = cv2.waitKey(1) & 0xFF 
        if(key == 27): #ESC 아스키코드
            break                              

cap.release()
cv2.destroyAllWindows()
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163941950-5036e01f-5854-4238-93e5-c4f1171c5196.png)

### 동영상 저장하기 
```py
import cv2

cap = cv2.VideoCapture(0) 

width = cap.get(cv2.CAP_PROP_FRAME_WIDTH)
height = cap.get(cv2.CAP_PROP_FRAME_HEIGHT)
print("size: {0} * {1}".format(width,height))

fourcc = cv2.VideoWriter_fourcc(*'XVID')
writer = cv2.VideoWriter('test.avi',fourcc,24, (int(width), int(height)))

while cap.isOpened():
    #카메라 프레임 읽기
    success, frame = cap.read() # cap이라는 객체를 통해서 frame을 읽음
                                # success, frame 리턴값 2개 받음
    if success:
        #프레임 출력
        writer.write(frame)
        cv2.imshow('Camera Window', frame)
        

        #ESC 종료
        key = cv2.waitKey(1) & 0xFF 
        if(key == 27): #ESC 아스키코드
            break                              

cap.release()
cv2.destroyAllWindows()
```

### 출력결과
- 동영상 저장 확인

![image](https://user-images.githubusercontent.com/82345970/163946388-3a777d7d-d3cd-4339-91fc-7249b416c417.png)

### opencv,matplotlib 예제
```py
import cv2 
from matplotlib import pyplot as plt # opencv 라이브러리

img = cv2.imread('sea.jpg',1)
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
plt.imshow(img)
plt.show()
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165897610-9d0197e2-63b1-4012-990e-b5a5ed9f90a8.png)


