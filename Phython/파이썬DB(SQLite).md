### SQLite 스키마(DB) 생성
```db
.open bookSroreDB -> DB 생성 명령어
``` 
![image](https://user-images.githubusercontent.com/82345970/163531520-580718f1-6b3a-4d0e-9b31-b5791b72edbd.png)

### table 생성
```db
create table bookitem(item char (100), author char(50), publisher char(50), stock int);
```

### table 목록확인
```db
.table 명령어
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163532257-38028bb7-2681-48a0-9bb8-ae719f332072.png)


### schema 목록 확인
```db
.schema bookitem
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163532228-d1ae5c41-1bd9-4c86-9e8c-ea8db207ef3b.png)

### 데이터 insert 
```db
insert into bookitem values('C programming', 'chlee', 'digitalbooks', '100');
insert into bookitem values('python', 'chlee', 'digitalbooks', '200');
insert into bookitem values('javascript', 'khcn', 'hanbit', '400');
insert into bookitem values('pipline', 'kj', 'hanbit', '300');
```

### 데이터 select
- .header on
- .mode column 위 두개 명령어 입력하면 select시 터미널 상에서 이쁘게 출력 됨
 
```db
select * from bookitem;
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163538047-26c65a3d-bfa0-4231-9ccd-8b6c40eeafff.png)

### 데이터 delete
```db
delete from bookitem where  author = 'kj';
 ```
 ### 출력 결과
 ![image](https://user-images.githubusercontent.com/82345970/163539098-bc277590-33a3-4b07-ab96-1964f44ee74f.png)
 
 ### 파이썬 코드에서 SQLite 데이터베이스 사용 순서
 ![image](https://user-images.githubusercontent.com/82345970/163539408-3e15b9ce-9851-4022-ac24-b8c868ae67fd.png)

 ```py
 import sqlite3
conn = sqlite3.connect('bookStoreDB')
print('1. DB 연결 성공')

cur = conn.cursor()
print('2. 커서 생성 성공')

cur.execute('create table if not exists bookitem(item char (100), author char(50), publisher char(50), stock int)') # if not exists 존재 하지 않으면 create 해라 

print('3 테이블 생성')
cur.execute("insert into bookitem values('C programming', 'chlee', 'digitalbooks', '100')")
cur.execute("insert into bookitem values('java', 'chlee', 'digitalbooks', '200')")
cur.execute("insert into bookitem values('python', 'chlee', 'digitalbooks', '300')")
cur.execute("insert into bookitem values('C++', 'chlee', 'digitalbooks', '400')")

print('4. 데이터 입력')

conn.commit()
print('5. 데이터 저장')

cur.execute('select * from bookitem')
print('6. 데이터 조회')
while True:
  row = cur.fetchone()
  if row == None:
    break
  print(row)  
print('7. 데이터 출력')  

conn.close()
print('8.DB 연결 종료')
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/163542174-6a25a151-341c-46ca-b772-3160baa19929.png)


