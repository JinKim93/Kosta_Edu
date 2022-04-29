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


