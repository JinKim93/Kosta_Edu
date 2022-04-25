## Pandas
- 파이썬 언어로 만들어진 빅데이터 분석을 쉽게해주는 프레임워크
- Pandas DataFrame은 표와 같은 스프레드시트 구조로 데이터를 다룰 수 있다
- 데이터 셋을 받을 수 있는 사이트 https://www.kaggle.com/datasets

## Pandas 설치방법
- cmd창 -> pip install pandas


### Pandas가 처리하는 데이터
- 데이터를 matrix 단위로 처리
- 테이블의 데이터에서 특정 컬럼이나 특정 레코드의 값을 가져와서 변수에 저장
- 행이나 열 단위의 접근이 가능
- 데이터의 처리 속도가 빠름
![image](https://user-images.githubusercontent.com/82345970/164650771-5638b697-28a7-499f-8912-9f514879072b.png)

## Pandas 사용
### Pandas
- 코드에 import pandas as pd 선언
- 함수를 사용할 때마다 pandas.어쩌구()식으로 사용
- as pd를 하는 이뉴는 pandas의 반복이 불편하므로 pd라는 별칭을 붙여줌 

### Pandas 예제
```py
import pandas as pd

num_series = pd.Series([1,2,3,4,5])
num_df = pd.DataFrame([1,2,3,4,5])

print(num_series) # 벡터 -> 배열형. 0번인덱스 -> 1들어가 있음, 출력결과 확인시 비교
print(num_df) # 데이터프레임 -> 매트릭스 -> 표의형태
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/164655142-9f81c7d0-3d42-42d5-b3f7-3b218b20dd29.png)

### pnadas 예제
```py
import pandas as pd

dates = pd.date_range('20220425',periods=5)
num_series = pd.Series([10,20,30,40,50],index= dates)
print(num_series)
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165039715-d0c8ceb9-e8f4-422e-9375-f368de9aee7f.png)

### pandas 에제
```py

import matplotlib.pyplot as plt
import pandas as pd

dates = pd.date_range('20220425',periods=5)
num_series = pd.Series([100,20,300,40,250],index= dates)
print(num_series)
num_series.plot()
plt.show()
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165040428-32f0302c-024d-4c4f-9443-c6ea06b7ac54.png)

![image](https://user-images.githubusercontent.com/82345970/165040389-d2486436-1349-4da5-af0d-62f66ad626a9.png)

### pandas 예제
- bar형태 출력
```py

import matplotlib.pyplot as plt
import pandas as pd

dates = pd.date_range('20220425',periods=5)
num_series = pd.Series([100,20,300,40,250],index= dates)
print(num_series)
num_series.plot(kind = 'bar')
plt.show()
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165040734-1de27fbb-04d9-4654-8bac-8e17a781ef00.png)

### 2차원데이터 형태
```py
import pandas as pd

num_df = pd.DataFrame({"col1" : [10,20,30,40,50], "col2" : [60,70,80,90,100]})
print(num_df)
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165041766-2f83b462-6468-4d10-8604-70e99be45d3e.png)


### 2차원데이터 형태
- plt 이용

```py
import pandas as pd
import matplotlib.pyplot as plt
num_df = pd.DataFrame({"col1" : [10,30,50,40,100], "col2" : [100,70,50,30,10]})
print(num_df)
num_df.plot()
plt.show()
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165045909-b93d5861-0dd5-4f67-8b75-0880765e9bef.png)

### 2차원데이터 형태
- bar 그래프 이중형식

```py
from inspect import stack
import pandas as pd
import matplotlib.pyplot as plt
num_df = pd.DataFrame({"col1" : [10,30,50,40,100], "col2" : [100,70,50,30,10]})
print(num_df)
num_df.plot(kind = 'bar',stacked = True)
plt.show()
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165046414-c1a82ed9-cf64-43d2-aef2-764a0aae5e9f.png)

### 대중교통 데이터 실습
- subwayfee.csv 사용
```py
import csv
f = open('./subwayfee.csv','r',encoding='cp949')
data = csv.reader(f)

next(data)

for row in data:
    print(row)
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/165049251-032b8cff-c143-4d86-8acb-fa83b43984a2.png)



