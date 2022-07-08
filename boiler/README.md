### 1. 폴더생성후 npm init
- 백엔드 시작점 -> index.js파일

### 2. express패키지설치 -> npm install express --save, npm i -D nodemon 

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
1. npm install body-parser --save 패키지 설치
- body-parser Dependecny는 클라이언트에서 보내주는 JSON, buffer 등등 즉 회원가입할때, 아이디를 적으면, parse(분석)해서 전달해줌

### 8.2 postman 설치
- 로그인 및 회원가입을 할때, 클라이언트 만들어진게 없어서, 데이터를 클라이언트에 보낼수 없으니까</br>
  대체하기 위해서 postman 설치를 함

### 8.3 Register Route만들기(index.js)
- 회원가입할때 필요한 정보들을 client에서 가져오면
- 그것들을 데이터베이스에 넣어줌 -> models/User.js를 가져와야함

![image](https://user-images.githubusercontent.com/82345970/177908360-8bd99819-ed4e-47fd-962c-7e5cb59097c9.png)

### 8.3 bodyParser 모듈로 require해줘야함(Register Route만들기)

![image](https://user-images.githubusercontent.com/82345970/177908527-91116df8-f774-4e36-b927-7465c54e757d.png)

### 8.3 bodyParser 옵션 추가(Register Route만들기) 

![image](https://user-images.githubusercontent.com/82345970/177910311-50844173-b432-4b56-9602-f760354c9fdc.png)

### 8.3 Register Route만들기(index.js)

![image](https://user-images.githubusercontent.com/82345970/177910066-5fbef1fc-a7b9-4eae-ab81-5ce929d3e811.png)

![image](https://user-images.githubusercontent.com/82345970/177910175-bc2caea9-b5ec-489c-8fed-b527561eb60b.png)

### 8.3 postman을 이용해서 회원가입라우터 동작 잘되나 확인

![image](https://user-images.githubusercontent.com/82345970/177910763-feeed0b1-4997-437d-bfda-c11a744b18b4.png)

### 8.3 회원가입기능 라우터 최종소스코드(index.js)
```js
const express = require('express');
const app = express();
const port = 5000;
const bodyParser = require('body-parser');
const { User } = require('./models/User');

//applicaion/x-www-form-urlencoded -> 이런 데이터분석해서 가져올수있게해줌
app.use(bodyParser.urlencoded({extended: true}));
//applicaion/json타입으로 된걸 분석해서 가져올수있게 해줌
app.use(bodyParser.json());

const mongoose = require('mongoose');
mongoose.connect('mongodb+srv://jinkim:abcd1234@boilerplate.3au6j4e.mongodb.net/?retryWrites=true&w=majority', {
    useNewUrlParser: true, useUnifiedTopology: true
}).then(() => console.log('mogodb connected'))
  .catch(err => console.log(err))  

app.get('/', (req, res) => {
  res.send('Hello World!')
});

//라우터 endpoint /register
app.post('/register',(req, res) => {
    //회원가입할때 필요한 정보들을 client에서 가져오면
    //그것들을 데이터베이스에 넣어줌 -> models/User.js를 가져와야함

    //회원가입창에 있는 정보들 데이터베이스에 넣기위한 작업
    /*
    req.body 안에는 json형식으로
    {
        id: "jinkim",
        password: "1234"
    }   
    이런식으로 req.body에 들어있는것이다.
    이렇게 req.body에 들어있을수 있게해주는게 bodyParser가 있어서 가능함
    */    
    const user = new User(req.body);

    //mongodb에서 오는 메소드
    //req.body에서 온 정보가 user모델에 저장이 됨
    //저장할때 에러가 있다고 하면, 클라이언트에 에러있다고 전달해줘야함
    //전달할때 json형식으로 전달해주고, err 메시지도 전달
    //성공을 할경우 status200을 json형식으로 전달
    user.save((err, userInfo) => {
        if(err) return res.json({ success: false, err})
        return res.status(200).json({ 
            sucess: true 
        })
    })

})

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
});
```

### 9. 소스안에 있는 비밀정보 보호 하기 
- mongodb연결 할때, 아이디랑, 비밀번호 노출됨

![image](https://user-images.githubusercontent.com/82345970/177911991-ff489f20-a215-49e1-8bb1-c348bf6675c8.png)

- 최상위폴더(boiler) 하위에 confing폴더생성, config폴더 하위에 dev.js파일생성

### 9.2 dev.js파일

![image](https://user-images.githubusercontent.com/82345970/177912421-a45defd7-5c5b-44b1-9e2a-b3a2d6f4d10e.png)

### 9.2 로컬환경(development) vs 배포(Deploy) 한후 구별을 해줘야함
- 로컬환경에서는 상기 처럼 해주면 됨
- 로컬환경에서는 변수를 dev.js에서 가져갈수 있음
- 하지만 배포를 할떄(heroku, 또는 클라우드서비스), heroku서비스를 이용하면 하기 처럼 따로 등록을 해야함

![image](https://user-images.githubusercontent.com/82345970/177912722-19f2a5a1-97ef-47b0-9acb-e3bade03e567.png)

### 9.2 로컬환경(development) vs 배포(Deploy) 한후 구별(config/prod.js파일생성)
- heroku에서 설정한 이름하고 같아야 함

![image](https://user-images.githubusercontent.com/82345970/177913312-0a2b7c92-7932-4b98-9e16-823df1c51547.png)

### 9.2 로컬환경(development) vs 배포(Deploy) 한후 구별(config/key.js파일생성)
- 로컬환경과, 배포환경 구분해줌

![image](https://user-images.githubusercontent.com/82345970/177913411-47ad5836-28ac-4d94-b676-39eed1713129.png)

![image](https://user-images.githubusercontent.com/82345970/177913444-013d1558-45d0-455d-a1b3-e02e27c75d48.png)


### 9.2 로컬환경(development) vs 배포(Deploy) index.js에 require 해줘야함

![image](https://user-images.githubusercontent.com/82345970/177913764-3107deda-f90d-4602-a24d-20f140a92f69.png)

![image](https://user-images.githubusercontent.com/82345970/177913856-6547bb0b-934b-479e-98cd-79d83bfa3fa5.png)

### 9.2 로컬환경(development) vs 배포(Deploy) index.js 수정된 소스코드
```js
const express = require('express');
const app = express();
const port = 5000;
const bodyParser = require('body-parser');

const config = require('./config/key');

const { User } = require('./models/User');


//applicaion/x-www-form-urlencoded -> 이런 데이터분석해서 가져올수있게해줌
app.use(bodyParser.urlencoded({extended: true}));
//applicaion/json타입으로 된걸 분석해서 가져올수있게 해줌
app.use(bodyParser.json());

const mongoose = require('mongoose');
mongoose.connect(config.mongoURI, {
    useNewUrlParser: true, useUnifiedTopology: true
}).then(() => console.log('mogodb connected'))
  .catch(err => console.log(err))  

app.get('/', (req, res) => {
  res.send('Hello World!')
});

//라우터 endpoint /register
app.post('/register',(req, res) => {
    //회원가입할때 필요한 정보들을 client에서 가져오면
    //그것들을 데이터베이스에 넣어줌 -> models/User.js를 가져와야함

    //회원가입창에 있는 정보들 데이터베이스에 넣기위한 작업
    /*
    req.body 안에는 json형식으로
    {
        id: "jinkim",
        password: "1234"
    }   
    이런식으로 req.body에 들어있는것이다.
    이렇게 req.body에 들어있을수 있게해주는게 bodyParser가 있어서 가능함
    */    
    const user = new User(req.body);

    //mongodb에서 오는 메소드
    //req.body에서 온 정보가 user모델에 저장이 됨
    //저장할때 에러가 있다고 하면, 클라이언트에 에러있다고 전달해줘야함
    //전달할때 json형식으로 전달해주고, err 메시지도 전달
    //성공을 할경우 status200을 json형식으로 전달
    user.save((err, userInfo) => {
        if(err) return res.json({ success: false, err})
        return res.status(200).json({ 
            sucess: true 
        })
    })

})

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
});
```








