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


