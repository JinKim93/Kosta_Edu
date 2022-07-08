### 1. 폴더생성후 npm init
- 백엔드 시작점 -> index.js파일

### 2. express패키지설치 -> npm install express --save, npm i -D nodemon, npm install cookie-parser --save

### 3. npm install mongoose --save 패키지설치, npm install jsonwebtoken --save 패키지설치

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

### 10. 비밀번호 암호화 하기(Bcrypt사용)
- npm install bcrypt --save 패키지설치

### 10.2 비밀번호 암호화 하기(index.js)
- new User(req,body) 모든 정보가 user.save에서 save 하기전에 비밀번호 암호화를 해줘야함 
- 그러기 위해서는 mongoose의 기능을 이용해야함

![image](https://user-images.githubusercontent.com/82345970/177914784-0327caeb-dad5-4f13-8327-81619b2ff3e7.png)


### 10.2 비밀번호 암호화 하기(mongoose기능 이용)
- models/User.js로 이동
- 모듈 require
- salt를 이용해서 비밀번호를 암호화 해야함 -> salt를 먼저생성
 
![image](https://user-images.githubusercontent.com/82345970/177915535-a937ea8b-191a-48f7-a0ae-21752294abf8.png)

### 10.2 비밀번호 암호화 하기(index.js) 소스코드
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


### 10.2 비밀번호 암호화 하기(models/User.js) 소스코드
```js
//mogoose 모듈가져오기
const mongoose = require('mongoose');

//Bcrypt 모듈 가져오기
const bcrypt = require('bcrypt');
const saltRounds = 10; //salt가 몇글자인지 나타냄

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

userSchema.pre('save', function(next){
    var user = this;

    //패스워드가 변경될때만, bcrypt를 이용해 암호화를 해준다
    if(user.isModified('password')){
    
    //비밀번호를 암호화 시킨다
    bcrypt.genSalt(saltRounds,function(err, salt){
        if(err) return next(err)

        bcrypt.hash(user.password,salt,function(err, hash){
            if(err) return next(err)
            user.password = hash;
            next();
            })
        })
    } 
    else {
        next();
    }

   
})

//상기만든 스키마를 models로 감싸줌
const User = mongoose.model('User',userSchema); //User:모델이름, 스키마이름 적기

//models을 다른파일에서 쓰기위해 exports
module.exports = { User };
```

### 11. 로그인기능 만들기
1. 로그인라우터가 필요 -> 로그인 라우터만들자

### 11.2 로그인라우터(index.js)
- 요청된 이메일을 데이터베이스에 있는지 찾는다
- 요청된 이메일이 데이터베이스에 있다면 비밀번호가 맞는 비밀번호 인지 확인
- 비밀번호 까지 맞다면 토큰을 생성하기

### 11.3 로그인라우터(index.js)
- 요청된 이메일을 데이터베이스에 있는지 찾는다

![image](https://user-images.githubusercontent.com/82345970/177919650-a9b44926-9790-4e17-98c3-1932a99aa34e.png)


### 11.4 로그인라우터(index.js, models/User.js)
- 요청된 이메일이 데이터베이스에 있다면 비밀번호가 맞는 비밀번호 인지 확인
1. index.js
 
![image](https://user-images.githubusercontent.com/82345970/177919800-63660d64-e96a-44a7-b8d0-fca7b59b0856.png)


2.comparePassword 매소드를 만듬(models/User.js)
- 두가지 argument를 넣어줌
- req.body.password -> 요청할때주는 패스워드
- (err, isMatch ) 콜백함수를 줌
	- 에러가나오면 에러, 비밀번호를 비교해서, 웹사이트에서친 비밀번호랑, DB에있는 비밀번호 비교할거다
	- 메소드는 models/User.js에서 만들어줘야함

![image](https://user-images.githubusercontent.com/82345970/177920640-5997a6a8-f4d3-4c25-91f7-c7de9fcd93ad.png)


### 11.5 로그인라우터
- 비밀번호 까지 맞다면 토큰을 생성하기
- 토큰생성하기 위해서는 JSONWEBTOKEN 라이브러리 사용해야함
- npm install jsonwebtoken --save
1. index.js

2. models/User.js jsonwebtoken모듈추가

![image](https://user-images.githubusercontent.com/82345970/177921644-1e8ea32e-1379-49e5-aaf5-e5f2a6fe7dff.png)

### 11.5 로그인라우터(index.js)
```js
const express = require('express');
const app = express();
const port = 5000;
const bodyParser = require('body-parser');
const cookieParser = require('cookie-parser');
const config = require('./config/key');

const { User } = require('./models/User');


//applicaion/x-www-form-urlencoded -> 이런 데이터분석해서 가져올수있게해줌
app.use(bodyParser.urlencoded({extended: true}));
//applicaion/json타입으로 된걸 분석해서 가져올수있게 해줌
app.use(bodyParser.json());
//쿠키파써 사용
app.use(cookieParser());

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

//로그인라우터
app.post('/login',(req, res) => {
    //요청된 이메일을 데이터베이스에 있는지 찾는다
    User.findOne({ email: req.body.email }, (err, user) => {
        if(!user) {
            return res.json({
                loginSuccess: false,
                message: "제공된 이메일에 해당하는 유저가 없습니다"
            })
        }
        //요청된 이메일이 데이터베이스에 있다면 비밀번호가 맞는 비밀번호 인지 확인
        //comparPassword라는 메소드를 만듬
        user.comparePassword(req.body.password, (err, isMatch) => {
            if(!isMatch)
                return res.json({ loginSuccess: false, message: "비밀번호가 틀렸습니다"})
            //비밀번호 까지 맞다면 토큰을 생성하기
            //generateToken 매소드를 만들어줌 -> models/User.js에 만들어줘야함
            user.generateToken((err, user) => {
                if (err) return res.status(400).send(err);
                    //토큰을 저장한다. 어디에? 쿠키, 로컬스토리지 등등
                    //쿠키에 저장을할거다 npm install cookie-parser --save 패키지설치
                    res.cookie("x_auth", user.token)
                    .status(200)
                    .json({ loginSuccess: true, userId: user._id })


            })    

        })
    })
})

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
});
```

### 11.5 로그인라우터(models/User.js)
```js
//mogoose 모듈가져오기
const mongoose = require('mongoose');

//Bcrypt 모듈 가져오기
const bcrypt = require('bcrypt');
const saltRounds = 10; //salt가 몇글자인지 나타냄

//jsonwebtoken모듈 가져오기
const jwt = require('jsonwebtoken');

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

userSchema.pre('save', function(next){
    var user = this;

    //패스워드가 변경될때만, bcrypt를 이용해 암호화를 해준다
    if(user.isModified('password')){
    
    //비밀번호를 암호화 시킨다
    bcrypt.genSalt(saltRounds,function(err, salt){
        if(err) return next(err)

        bcrypt.hash(user.password,salt,function(err, hash){
            if(err) return next(err)
            user.password = hash;
            next();
            })
        })
    } 
    else {
        next();
    }

   
})

userSchema.methods.comparePassword = function(plainPassword, cb) {
    //plainPassword 12345 === 암호화된 비밀번호$123123cvcdfd
    bcrypt.compare(plainPassword, this.password, function(err, isMatch){
        if(err) return cb(err);
        cb(null, isMatch)//에러가없다 = null, 비밀번호같다 = isMatch -> true
    })
}

userSchema.methods.generateToken = function(cb){

    var user = this;
    //jsonwebtoken을 이용해서 token을 생성하기

    var token = jwt.sign(user._id.toHexString(), 'secretToken')
    user.token = token;
    user.save(function(err, user){
        if(err) return cb(err)
        cb(null, user)
    })
}

//상기만든 스키마를 models로 감싸줌
const User = mongoose.model('User',userSchema); //User:모델이름, 스키마이름 적기

//models을 다른파일에서 쓰기위해 exports
module.exports = { User };
```

### 12. Auth 기능 만들기(지금까지 만든 route express에서 제공하는 Route로 바꿀것이다)
- 기능이 필요한 이유
- 어떤 사이트 들어갔을때, 여러가지 페이지들이 있다. -> 어떤페이지는 로그인된유저만이용할수 있고, 다른페이지는 어느누구나 이용할수있다
- 로그인한사람만 이용할수있고, 관리자만 이용할수 있고 -> 구분해줄려면 Auth라우터가 필요함
- 클라이언트측 토큰을 쿠키에, 서버측 토큰을 DB에 넣어줌

![image](https://user-images.githubusercontent.com/82345970/177928803-1d9077a8-9dff-4755-a44e-d520ea2eb16a.png)

### 12.2 Auth라우터생성(index.js)
- 최상위폴더 하위에 middleware폴더생성 -> auth라우터를 위해서
- middleware/auth.js파일생성

### 12.2 Auth라우터생성(middleware/auth.js)

![image](https://user-images.githubusercontent.com/82345970/177930337-5f1e9910-f996-4ef8-b13d-24a900a49fb0.png)

### 12.3 index.js에서 auth를 쓰기 위해서 import 해주기(index.js)

![image](https://user-images.githubusercontent.com/82345970/177930748-ed82d32b-886a-4b33-88fd-7c4916d9cc4f.png)


![image](https://user-images.githubusercontent.com/82345970/177930520-f9ab5490-8222-4ec6-af26-71d8047cfe0b.png)

### 12.4 middleware/auth.js 코드작성

![image](https://user-images.githubusercontent.com/82345970/177932106-c076f201-b516-49cf-8fa6-3801593e5759.png)

```js
const { User } = require('../models/User');

let auth = (req, res, next) => {

    //인증처리를 하는곳

    //1. 클라이언트 쿠키에서 토큰을 가져온다(cookie parser이용)
    //index.js에서 쿠키를 넣을때  x_auth로 넣어서 하기처럼 작성
    let token = req.cookies.x_auth; // ->쿠키를 토큰에서 가져옴

    //2. 토큰을 복호화 한후 유저를 찾는다
    //User.를 사용하기 위해 User모듈을 불러온다 맨위에 적기
    //const { User } = require('../models/User');
    //User.findByToken() 만들어줬으니까, models/User.js가서 작업해줘야함
    User.findByToken(token, (err,user) => {
        if(err) throw err;
        if(!user) return res.json({ isAuth: false, error: true})

        req.token = token;
        req.user = user;
        next();
    })
    //3. 유저가 있으면 인증 okay
    //4. 유저가 없으면 인증 no

}

//auth를 다른파일에 쓸수있게 정의
module.exports = { auth};
```


### 12.5 상기사진에 표시한부분 작성하기 위해 models/User.js로 이동
- userSchema작성 할 거다

![image](https://user-images.githubusercontent.com/82345970/177933147-554895e5-3430-4d93-9eda-475188fca5aa.png)

### 12.6 Auth라우터생성(index.js) 소스코드

![image](https://user-images.githubusercontent.com/82345970/177934624-4a9b702f-b374-4623-af18-de94a90e24fc.png)

```js
const express = require('express');
const app = express();
const port = 5000;
const bodyParser = require('body-parser');
const cookieParser = require('cookie-parser');
const config = require('./config/key');
const { auth } = require('./middleware/auth');
const { User } = require('./models/User');


//applicaion/x-www-form-urlencoded -> 이런 데이터분석해서 가져올수있게해줌
app.use(bodyParser.urlencoded({extended: true}));
//applicaion/json타입으로 된걸 분석해서 가져올수있게 해줌
app.use(bodyParser.json());
//쿠키파써 사용
app.use(cookieParser());

const mongoose = require('mongoose');
mongoose.connect(config.mongoURI, {
    useNewUrlParser: true, useUnifiedTopology: true
}).then(() => console.log('mogodb connected'))
  .catch(err => console.log(err))  

app.get('/', (req, res) => {
  res.send('Hello World!')
});

//라우터 endpoint /register
app.post('api/users/register',(req, res) => {
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

//로그인라우터
app.post('api/users/login',(req, res) => {
    //요청된 이메일을 데이터베이스에 있는지 찾는다
    User.findOne({ email: req.body.email }, (err, user) => {
        if(!user) {
            return res.json({
                loginSuccess: false,
                message: "제공된 이메일에 해당하는 유저가 없습니다"
            })
        }
        //요청된 이메일이 데이터베이스에 있다면 비밀번호가 맞는 비밀번호 인지 확인
        //comparPassword라는 메소드를 만듬
        user.comparePassword(req.body.password, (err, isMatch) => {
            if(!isMatch)
                return res.json({ loginSuccess: false, message: "비밀번호가 틀렸습니다"})
            //비밀번호 까지 맞다면 토큰을 생성하기
            //generateToken 매소드를 만들어줌 -> models/User.js에 만들어줘야함
            user.generateToken((err, user) => {
                if (err) return res.status(400).send(err);
                    //토큰을 저장한다. 어디에? 쿠키, 로컬스토리지 등등
                    //쿠키에 저장을할거다 npm install cookie-parser --save 패키지설치
                    res.cookie("x_auth", user.token)
                    .status(200)
                    .json({ loginSuccess: true, userId: user._id })


            })    

        })
    })
})

//Auth라우터생성
//auth라는 미들웨어 추가
//미들웨어란 엔드포인트에서(/api/users/auth) request를 받은다음에
//(req, res)콜백function 하기 전에 중간에서 해주는역할
app.get('/api/users/auth',auth,(req, res) => {
    //여기까지 미들웨어를 통과해 왔다는 이야기는 Authentication이 True 라는 말
    res.status(200).json({
        _id: req.user._id,
        //role 0 -> 일반유저 , role 0이 아니면 관리자
        isAdmin: req.user.role === 0 ? false : true,
        isAuth: true,
        email: req.user.email,
        name: req.user.name,
        lastname: req.user.lastname,
        role: req.user.role,
        image:req.user.image
    })    

})


app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
});
```

### 로그아웃 기능 만들기(index.js)
![image](https://user-images.githubusercontent.com/82345970/177936354-41ee61c2-e084-436c-a312-c129cf17185c.png)

```js
const express = require('express');
const app = express();
const port = 5000;
const bodyParser = require('body-parser');
const cookieParser = require('cookie-parser');
const config = require('./config/key');
const { auth } = require('./middleware/auth');
const { User } = require('./models/User');


//applicaion/x-www-form-urlencoded -> 이런 데이터분석해서 가져올수있게해줌
app.use(bodyParser.urlencoded({extended: true}));
//applicaion/json타입으로 된걸 분석해서 가져올수있게 해줌
app.use(bodyParser.json());
//쿠키파써 사용
app.use(cookieParser());

const mongoose = require('mongoose');
mongoose.connect(config.mongoURI, {
    useNewUrlParser: true, useUnifiedTopology: true
}).then(() => console.log('mogodb connected'))
  .catch(err => console.log(err))  

app.get('/', (req, res) => {
  res.send('Hello World!')
});

//라우터 endpoint /register
app.post('api/users/register',(req, res) => {
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

//로그인라우터
app.post('api/users/login',(req, res) => {
    //요청된 이메일을 데이터베이스에 있는지 찾는다
    User.findOne({ email: req.body.email }, (err, user) => {
        if(!user) {
            return res.json({
                loginSuccess: false,
                message: "제공된 이메일에 해당하는 유저가 없습니다"
            })
        }
        //요청된 이메일이 데이터베이스에 있다면 비밀번호가 맞는 비밀번호 인지 확인
        //comparPassword라는 메소드를 만듬
        user.comparePassword(req.body.password, (err, isMatch) => {
            if(!isMatch)
                return res.json({ loginSuccess: false, message: "비밀번호가 틀렸습니다"})
            //비밀번호 까지 맞다면 토큰을 생성하기
            //generateToken 매소드를 만들어줌 -> models/User.js에 만들어줘야함
            user.generateToken((err, user) => {
                if (err) return res.status(400).send(err);
                    //토큰을 저장한다. 어디에? 쿠키, 로컬스토리지 등등
                    //쿠키에 저장을할거다 npm install cookie-parser --save 패키지설치
                    res.cookie("x_auth", user.token)
                    .status(200)
                    .json({ loginSuccess: true, userId: user._id })


            })    

        })
    })
})

//Auth라우터생성
//auth라는 미들웨어 추가
//미들웨어란 엔드포인트에서(/api/users/auth) request를 받은다음에
//(req, res)콜백function 하기 전에 중간에서 해주는역할
app.get('/api/users/auth',auth,(req, res) => {
    //여기까지 미들웨어를 통과해 왔다는 이야기는 Authentication이 True 라는 말
    res.status(200).json({
        _id: req.user._id,
        //role 0 -> 일반유저 , role 0이 아니면 관리자
        isAdmin: req.user.role === 0 ? false : true,
        isAuth: true,
        email: req.user.email,
        name: req.user.name,
        lastname: req.user.lastname,
        role: req.user.role,
        image:req.user.image
    })    

})

//로그아웃 라우터
//로그아웃 전에는 로그인된 상태니까 auth미들웨어 넣어줌
app.get("/api/users/logout", auth, (req, res) => {
    User.findOneAndUpdate({ _id: req.user._id }, { token: "" }, (err, user) => {
    if (err) return res.json({ success: false, err });
    return res.status(200).send({
      success: true,
    });
  });
});
    




app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
});
```











 













