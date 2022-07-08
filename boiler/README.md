### 1. 폴더생성후 npm init
- 백엔드 시작점 -> index.js파일

### 2. express패키지설치 -> npm install express --save

### 3. npm install mongoose --save 패키지설치

### 4. mogoDB연결 안될시 ip 추가해줘야함

![image](https://user-images.githubusercontent.com/82345970/177903530-90923574-09ed-499a-acf5-30e388c91bf0.png)

### 5. usermodel 생성하기 -> user라는 스키마를 models로 감싸줌
- 회원가입 시 기본정보 -> user 데이터 보관하기 위한, 스키마생성

### 6. modesl폴더생성
- User.js 파일생성

### 6.2 models폴더하위 User.js소스코드(User테이블? 생성)
```js
//mogoose 모듈가져오기
const mongoose = require('mongoose');

//스키마 생성
const userSchema = mongoose.Schema({
    name: {
        type: String,
        maxlength:50
    },
    email: {
        type: String,
        trim: true, //trim은 rlawls 123 -> 스페이스공백을 없애주는 역할을 함
        unique: 1 //같은 이메일 못쓰게 설정
    },
    password: {
        type: String,
        minlength:5
    },
    lastname: {
        type: String,
        maxlength:50
    },
    //role 주는 이유-> 관리자가 될수도 있고, 일반유저가 될수 있게 구분
    role:{
        type: Number, //Number 1이면관리자, 0이면 일바유저
        default: 0
    },
    image: String,
    token: {    //유효성검사를 하기위해 token 테이블추가
        type: String
    },
    tokenExp: {  //토근사용할수있는 유효기간
        type: Number

    }

});

//상기만든 스키마를 models로 감싸줌
const User = mongoose.model('User',userSchema); //User:모델이름, 스키마이름 적기

//models을 다른파일에서 쓰기위해 exports
module.exports = { User };
```

### 7. git Repository에 올릴때, 예외파일 적용(.gitignore)
1. .gitignore파일생성
2. ignore할 폴더 or 파일명 .gitignore파일에 작성

![image](https://user-images.githubusercontent.com/82345970/177906325-9bca1814-5cab-4bee-8fbe-247de2a828fb.png)

### 8. 회원가입 기능 만들기







