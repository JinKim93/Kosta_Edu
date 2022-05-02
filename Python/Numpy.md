## Numpy 설치
1. cmd 창 열기
2. pip install numpy 명령어 입력

## Numpy란 무엇인가
- 데이터분석을 포함해 수학과 과학 연산을 위한 파이썬 기본패키지
- Numpy에서 제공하는 수학연산에 대한 구현이 C언어로 최적화 되어 있어 매우 빠름
- 다차원 배열을 효과적으로 처리할 수 있다.
- Vector / matrix 생성
- 행렬 곱
- Broadcast
- Index / slice / iterator

## Numpy의 차원
- 1차원 축(행) : axis 0 -> Vector(배열)
- 2차원 축(열) : axis 1 -> Matrix(행렬)
- 3차원 축(채널) : axis 2 -> tensor(3차원 이상)

![image](https://user-images.githubusercontent.com/82345970/165911830-0b7b3d85-4fdf-41e8-8060-7bf5c4386bc9.png)

### List를 numpy 배열로 바꾸기
```py
import numpy as np

list_data = [1,2,3]
array = np.array(list_data)

print(list_data)
print(array) #numpy 데이터구조
print(array.size)
print(array.dtype)
print(array[2])
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165912986-c164b3d2-c095-40ba-83e1-5a4a4cf56999.png)

```py
import numpy as np

list_data = [[1,2,3], [4,5,6]]
array = np.array(list_data)

print(list_data) #리스트
print(array) #numpy 데이터구조
print(array.size)
print(array.dtype)
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165913070-d71f8a01-f5b4-4340-aeba-2cb5ad33410d.png)

### 제곱근
```html
import numpy as np
print(np.sqrt(2))
```

### pi, sin 값
```html
import numpy as np

print(np.pi)
print(np.sin(0))
```

### 랜덤한 수
```html
import numpy as np

print(np.random.choice(6, 10)) # 0부터6까지, 10개의 숫자를 랜덤하게 출력
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/166197661-c61ad710-67cc-4096-a01c-41cbc8629ca6.png)

### 랜덤한 수(로또)
```html
import numpy as np

print(np.random.choice(46, 6, replace = False)) # 0부터45까지, 6개의 숫자를 랜덤하게 출력, replace = False 중복방지


```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/166197890-542a22ae-c6d1-423e-90b5-715a8dd129c1.png)

### 랜덤한 수
- 0 ~ 5 까지 확률 정하기 0.1 -> 10%로 확률
```html
import numpy as np

print(np.random.choice(6, 6, p=[0.1,0.2,0.3,0.2,0.1,0.1] )) #0 ~ 5 까지 확률 정하기 0.1 -> 10%로 확률
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/166198263-647be50a-3821-47d5-bb4b-d1a440c0ee11.png)

###  0부터 5까지 나온수 히스토그램으로 표현
```html
import matplotlib.pyplot as plt
import numpy as np

dice = np.random.choice(6,10)

plt.hist(dice)
plt.show()
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/166198634-b01a7473-7e05-4f21-bb41-d137f1e62b2c.png)

### 상기코드 Numpy 사용 안 할경우
```html
import matplotlib.pyplot as plt
import random

dice = []
for i in range(10):
  dice.append(random.randint(1,6)) # 1부터 5까지

plt.hist(dice)
plt.show()
  
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/166198896-07eeda7b-4bae-4094-91fb-bc1b0b5ac3b7.png)




