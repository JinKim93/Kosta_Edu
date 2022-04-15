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
