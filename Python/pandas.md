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
