# count() 함수 
- 문자(문자열) 개수 알아내기

### count() 함수 형태
```py
개수 = 문자열.count('검색할 문자 또는 문자열')
```

### count() 함수 예제
```py
string1 = '간장 공장 공장장은 강 공장장이고 된장 공장 공장장은 공 공장장이다'

chr1 = string1.count('공')
chr2 = string1.count('장')

print('"공"의 개수 : %d'% chr1)
print('"장"의 개수 : %d'% chr1)

string2 = '내가 그린 기린 그림은 잘 그린 기린 그림이고 네가 그린 기린 그림은 잘 못 그린 그림이다'

str1 = string2.count('그린')
str2 = string2.count('기린')
str3 = string2.count('그림')

print('"그린"의 개수 : %d'% str1)
print('"기린"의 개수 : %d'% str2)
print('"그림"의 개수 : %d'% str3)
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163113340-11f6cd50-2907-4ece-868c-a73bd2927037.png)

# 문자열 위치 찾기
- 내가 찾고 싶은 문자가 처음 나온 위치를 찾고 싶을때

```py
위치 = 문자열.find('검색할 문자 또는 문자열')
위치 = 문자열.index('검색할 문자 또는 문자열')
```

### 문자열 위치 찾기 예제
```py
string1 = '간장 공장 공장장은 강 공장장이고 된장 공장 공장장은 공 공장장이다'

chr1 = string1.find('공')
chr2 = string1.index('장')

print('"공"의 위치 : %d'% chr1)
print('"장"의 위치 : %d'% chr2)

string2 = '내가 그린 기린 그림은 잘 그린 기린 그림이고 네가 그린 기린 그림은 잘 못 그린 그림이다'

str1 = string2.count('그린')
str2 = string2.count('기린')
str3 = string2.count('그림')

print('"그린"의 위치 : %d'% str1)
print('"기린"의 위치 : %d'% str2)
print('"그림"의 위치 : %d'% str3)
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163114048-2877ef01-84a7-4014-b4a0-47372ec2932e.png)

# 문자열 삽입 및 분리
- 기존 문자열 사이에 구분자를 삽입하여 새로운 문자열로 합치는 기능
 
```py
새로운 문자열 = 구분자.join(문자열)
```

```py
train_str = '칙칙폭폭'
num_str = '123456789'

div_str1 = '_'.join(train_str)
div_str2 = '_'.join(num_str)

print(div_str1)
print(div_str2)
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163114613-ac64c580-51d6-47e8-b5cc-bf370c68c20b.png)

### 리스트 삽입 및 분리
```py
ani_list = ['강아지','고양이','원숭이','코끼리']
time_list = ['15','35','30']

ani_str = '+'.join(ani_list)
time_str = ':'.join(time_list)

print(ani_str)
print(time_str)
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163115239-e24283ff-9234-4841-94de-d0e89caa1378.png)


### 문자열 삽입 및 분리하기
```py
리스트 = 문자열.split(구분자)
```
- split() 함수는 구분자를 기준으로 분리하기 때문에 분리된 문자는 리스트 형태로 저장

```py
planet_str = '수성-금성-지구-화성-목성'
time_str = '12시:30분:55초'

planet_list = planet_str.split('-')
time_list = time_str.split(':')

print(planet_list)
print(time_list)
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163118497-7302c7c0-b4a3-4274-83cb-eb838c6b193a.png)

### 대문자/소문자 변환하기
- 영문의 대문자를 소문자로, 소문자를 대문자로 바꾸어주는 함수
```py
변경된 문자열 = 문자열.upper()
변경된 문자열 = 문자열.lower()
```
```py
eng_str = input('영문자를 입력하세요 :')

upper_str = eng_str.upper()
lower_str = eng_str.lower()

print("대문자로 변환 : %s" % upper_str)
print("소문자로 변환 : %s" % lower_str)
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163119111-066acc48-bb06-4a7a-9aa1-f4a39d1c0ab0.png)

### 문자열 공백 없애기
- 문자열 중 공백을 제거하는 함수가 제공
```py
변경된 문자열 = 문자열.lstrip() //왼쪽 공백 없애기
변경된 문자열 = 문자열.rstrip() //오른쪽 공백 없애기
변경된 문자열 = 문자열.strip()//양쪽 공백 없애기
```

```py
string1 = ' 죽는 날까지 하늘을 우러러 '
string2 = '한점 부끄럼이 없기를  '
string3 = '  잎새에 이는 바람에도  '

lstrip_str = string1.lstrip()
rstrip_str = string2.rstrip()
strip_str = string3.strip()

print("string 1   :%s"% string1)
print("string 2   :%s"% string2)
print("string 3   :%s"% string3)
print()
print("왼쪽 공백 없애기  :%s"% lstrip_str)
print("오른쪽 공백 없애기  :%s"% rstrip_str)
print("양쪽 공백 없애기  :%s"% strip_str)
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163120130-41beed2a-5299-4650-987a-3ac418dd8157.png)

### 문자열 구성 파악하기
![image](https://user-images.githubusercontent.com/82345970/163120451-d8244822-6b6e-43d3-a5e3-53faf232907a.png)

### 문자열 구성 파악 예제
```py
while True:
    string = input("문자열을 입력하세요 :")
    
    if string.isdigit():
        print("문자열은 숫자로 구성되어 있습니다")
    elif string.isalpha():
        print("문자열은 글자로 구성되어 있습니다")
        if string.isupper():
            print("문자열은 대문자로 구성되어 있습니다")
        elif string.islower():
            print("문자열은 소문자로 구성되어 있습니다")
    elif string.isspace():
        print("문자열은 공백으로 구성되어 있습니다")
        break                
    else:
        print("모르겠습니다")
    print()    
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163121254-ec077075-2d49-4be7-adbe-f637dadc2f93.png)

