### 1. API서버 만들기(10장)
1. lecture폴더생성
2. lecture폴더하위 nodebird-api, nodecat폴더생성

### 2. nodebird-api폴더로 이동후 npm init실행
- 패키지설치 
- npm i bcrypt cookie-parser dotenv express express-session morgan mysql2 nunjucks passport passport-local
- npm i sequelize uuid
- npm i passport-kakao
- npm i jsonwebtoken 패키지 설치
- npm i -D nodemon 패키지 설치 후 사진처럼 변경해주기
- 또한 메인이될 파일을 app.js로 변경해주기

![image](https://user-images.githubusercontent.com/82345970/177674981-9e0307b7-bd7d-4436-b942-f2430c0f5d84.png)

![image](https://user-images.githubusercontent.com/82345970/177675050-a81f9bac-dee1-43d3-98c9-7f2ac7306feb.png)

### 3. app.js파일생성(메인파일) -> lecture/nodebird-api폴더하위에 만들기

### 4. 9장에서 했던 config,models,passport폴더 복사해서,  nodebird-api폴더에 붙여넣기

### 5. nodebird-api폴더 하위에 routes,views폴더 생성

### 6. routes폴더하위에, 9장해서 했던 auth.js, middlewares.js폴더 복사,붙여넣기

### 7. 9장에있는 .env도 nodebird-api폴더 하위에 복사

### 8. views폴더하위에 9장에서 썻던 views/error.html파일 복사, 붙여넣기
- 9장에서 복사 붙여넣기 한다음 조금, 수정해주어야함(사진참고)

![image](https://user-images.githubusercontent.com/82345970/177676011-3b1fcec5-53c1-4357-9aa8-5247340635aa.png)

### 9. routes폴더 하위에 index.js파일생성 -> app.js코드 보면 indexRouter가있으므로 index.js 파일생성 해줌 

### 10. models폴더하위, domain.js파일생성
- mysql테이블에 domain이라는 테이블을 생성함 -> models폴더는 mysql(시퀄라이즈관련)

### 11. domain.js -> user.js관계
- belongTo이기때문에 user.js에서 수정해줘야함
 
![image](https://user-images.githubusercontent.com/82345970/177677931-b9c60725-cee2-4799-a599-e36d0a35d65d.png)

### 11.2 user.js 코드수정

![image](https://user-images.githubusercontent.com/82345970/177682524-0110766c-71e5-4510-a05c-84d03044851c.png)

### 11.3 index.js 코드수정

![image](https://user-images.githubusercontent.com/82345970/177678492-c811a712-bcea-4a7e-b5f6-1857a28d2f87.png)

![image](https://user-images.githubusercontent.com/82345970/177678565-9e413acc-fa29-47e9-b60c-4e184641ec55.png)

### 11.4 현재 Domain테이블 추가했으니까, 9장에도 Domain테이블추가를 해줘야함

### 12. 도메인등록화면만들기
- developer카카오.com에 있는 카카오웹등록햇던 페이지랑 비슷하다

### 12.2 views폴더에 login.html파일생성(도메인등록하는페이지)
- login.html
```js
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>API 서버 로그인</title>
    <style>
      .input-group label { width: 200px; display: inline-block; }
    </style>
  </head>
  <body>
    {% if user and user.id %}
      <span class="user-name">안녕하세요! {{user.nick}}님</span>
      <a href="/auth/logout">
        <button>로그아웃</button>
      </a>
      <fieldset>
        <legend>도메인 등록</legend>
        <form action="/domain" method="post">
          <div>
            <label for="type-free">무료</label>
            <input type="radio" id="type-free" name="type" value="free">
            <label for="type-premium">프리미엄</label>
            <input type="radio" id="type-premium" name="type" value="premium">
          </div>
          <div>
            <label for="host">도메인</label>
            <input type="text" id="host" name="host" placeholder="ex) zerocho.com">
          </div>
          <button>저장</button>
        </form>
      </fieldset>
      <table>
        <tr>
          <th>도메인 주소</th>
          <th>타입</th>
          <th>클라이언트 비밀키</th>
        </tr>
        {% for domain in domains %}
          <tr>
            <td>{{domain.host}}</td>
            <td>{{domain.type}}</td>
            <td>{{domain.clientSecret}}</td>
          </tr>
        {% endfor %}
      </table>
    {% else %}
      <form action="/auth/login" id="login-form" method="post">
        <h2>NodeBird 계정으로 로그인하세요.</h2>
        <div class="input-group">
          <label for="email">이메일</label>
          <input id="email" type="email" name="email" required autofocus>
        </div>
        <div class="input-group">
          <label for="password">비밀번호</label>
          <input id="password" type="password" name="password" required>
        </div>
        <div>회원가입은 localhost:8001에서 하세요.</div>
        <button id="login" type="submit">로그인</button>
      </form>
      <script>
        window.onload = () => {
          if (new URL(location.href).searchParams.get('loginError')) {
            alert(new URL(location.href).searchParams.get('loginError'));
          }
        };
      </script>
    {% endif %}
  </body>
</html>
```

### 12.3 nice라는 사람이 nodecat이라는 서비스를 준비하려고 하는대, -< nodebirdsns 짝퉁같은 서비스
### 12.3 즉 nodebirdAPI를 사용하기 위해서, 도메인을 등록해야함

### 13 JWT 사용하기

### 13.2 npm i jsonwebtoken 패키지 설치

### 13.3 JWT비밀키 .env저장

![image](https://user-images.githubusercontent.com/82345970/177685551-d49b16e7-e275-4ed5-8804-1965e83648ea.png)

### 13.4 routes폴더하위 middleware.js파일 코드추가(JWT관련 미들웨어)

![image](https://user-images.githubusercontent.com/82345970/177685900-0f9ea7a4-7687-4c27-bd2d-4d014ade12c2.png)

![image](https://user-images.githubusercontent.com/82345970/177685921-6d64a4df-0bdb-40e9-bed8-0466b7ae16bc.png)

```js
const jwt = require('jsonwebtoken');

exports.isLoggedIn = (req, res, next) => {
  if (req.isAuthenticated()) {
    next();
  } else {
    res.status(403).send('로그인 필요');
  }
};

exports.isNotLoggedIn = (req, res, next) => {
  if (!req.isAuthenticated()) {
    next();
  } else {
    res.redirect('/');
  }
};

exports.verifyToken = (req, res, next) => {
  try {
    req.decoded = jwt.verify(req.headers.authorization, process.env.JWT_SECRET);
    return next();
  } catch (error) {
    if (error.name === 'TokenExpiredError') { // 유효기간 초과
      return res.status(419).json({
        code: 419,
        message: '토큰이 만료되었습니다',
      });
    }
    return res.status(401).json({
      code: 401,
      message: '유효하지 않은 토큰입니다',
    });
  }
};
```

### 13.5 API서버이기 때문에 nodebirdsns에서 정보를 제공할 라우터를 뚫다? 만들어줘야함
### nodecat서비스 nodebirdAPI에 등록을 함 -> 등록이유: nodebird로 부터 데이터를 가져가고 싶은대
### 가져갈려면 nodebirdAPI서버에 요청을 보내야함 -> 요청을 처리할수 있는 라우터생성(routes폴더하위 v1.js파일생성)

### 13.6 routes폴더하위 v1.js파일 코드 -> app.js에 require
```js
const express = require('express');
const jwt = require('jsonwebtoken');

const { verifyToken } = require('./middlewares');
const { Domain, User } = require('../models');

const router = express.Router();

//토큰발급 라우터 
router.post('/token', async (req, res) => {
  const { clientSecret } = req.body;
  try {
    const domain = await Domain.findOne({
      where: { clientSecret },
      include: {
        model: User,
        attribute: ['nick', 'id'],
      },
    });
    if (!domain) {
      return res.status(401).json({
        code: 401,
        message: '등록되지 않은 도메인입니다. 먼저 도메인을 등록하세요',
      });
    }
    const token = jwt.sign({
      id: domain.User.id,
      nick: domain.User.nick,
    }, process.env.JWT_SECRET, {
      expiresIn: '1m', // 1분
      issuer: 'nodebird',
    });
    return res.json({
      code: 200,
      message: '토큰이 발급되었습니다',
      token,
    });
  } catch (error) {
    console.error(error);
    return res.status(500).json({
      code: 500,
      message: '서버 에러',
    });
  }
});

//토큰제대로 발급됬는지, test라우터
router.get('/test', verifyToken, (req, res) => {
  res.json(req.decoded);
});

module.exports = router;
```js
const express = require('express');
const path = require('path');
const cookieParser = require('cookie-parser');
const passport = require('passport');
const morgan = require('morgan');
const session = require('express-session');
const nunjucks = require('nunjucks');
const dotenv = require('dotenv');

dotenv.config();
const authRouter = require('./routes/auth');
const indexRouter = require('./routes');
const v1 = require('./routes/v1');
const { sequelize } = require('./models');
const passportConfig = require('./passport');

const app = express();
passportConfig();
app.set('port', process.env.PORT || 8002);
app.set('view engine', 'html');
nunjucks.configure('views', {
  express: app,
  watch: true,
});
sequelize.sync({ force: false })
  .then(() => {
    console.log('데이터베이스 연결 성공');
  })
  .catch((err) => {
    console.error(err);
  });

app.use(morgan('dev'));
app.use(express.static(path.join(__dirname, 'public')));
app.use(express.json());
app.use(express.urlencoded({ extended: false }));
app.use(cookieParser(process.env.COOKIE_SECRET));
app.use(session({
  resave: false,
  saveUninitialized: false,
  secret: process.env.COOKIE_SECRET,
  cookie: {
    httpOnly: true,
    secure: false,
  },
}));
app.use(passport.initialize());
app.use(passport.session());

app.use('/auth', authRouter);
app.use('/', indexRouter);
app.use('/v1', v1);

app.use((req, res, next) => {
  const error =  new Error(`${req.method} ${req.url} 라우터가 없습니다.`);
  error.status = 404;
  next(error);
});

app.use((err, req, res, next) => {
  res.locals.message = err.message;
  res.locals.error = process.env.NODE_ENV !== 'production' ? err : {};
  res.status(err.status || 500);
  res.render('error');
});

app.listen(app.get('port'), () => {
  console.log(app.get('port'), '번 포트에서 대기중');
});
```

### 13-6 nodebird-api폴더하위 app.js 소스코드


### 13-7 nodecat이라는 서비스가, nodebirdAPI사용시작, JWT토큰을발급해서, API요청을 쓸 것이다(v1.js코드확인)
- 도메인검사 후 -> 토큰발급해줌

### 14 NodeCat(호출서버) 만들기
- nodebirdsns(localhost:8001), nodebirdapi(localhost:8002) 서버 실행 시켜두자

### 14.2 nodecat폴더 이동후 npm init !!!!!

### 14.3 npm i axios cookie-parser dotenv express express-session morgan nunjucks, npm i -D nodemon 패키지 설치

### 14.4 nodecat폴더하위 app.js파일생성

### 14.5 nodebirdapi폴더에서 views폴더에 있는 error.html 붙여넣기

### 14.6 .env파일생성

![image](https://user-images.githubusercontent.com/82345970/177688107-e6f838df-8c44-469d-97aa-cbeba4b9b9cb.png)

- CLIENT_SECRET은 localhost:8002에서 생성한 키 적어주자

![image](https://user-images.githubusercontent.com/82345970/177688204-5d8c398d-5478-42a3-8ef3-c9ec096efb44.png)

### 14.7 nodecat폴더 하위 app.js 작성
- 포트 : 4000번
- 코드를보면 indexRouter가 보임 -> routes폴더 index.js파일생성
```js
const express = require('express');
const morgan = require('morgan');
const cookieParser = require('cookie-parser');
const session = require('express-session');
const nunjucks = require('nunjucks');
const dotenv = require('dotenv');

dotenv.config();
const indexRouter = require('./routes');

const app = express();
app.set('port', process.env.PORT || 4000);
app.set('view engine', 'html');
nunjucks.configure('views', {
  express: app,
  watch: true,
});

app.use(morgan('dev'));
app.use(cookieParser(process.env.COOKIE_SECRET));
app.use(session({
  resave: false,
  saveUninitialized: false,
  secret: process.env.COOKIE_SECRET,
  cookie: {
    httpOnly: true,
    secure: false,
  },
}));

app.use('/', indexRouter);

app.use((req, res, next) => {
  const error =  new Error(`${req.method} ${req.url} 라우터가 없습니다.`);
  error.status = 404;
  next(error);
});

app.use((err, req, res, next) => {
  res.locals.message = err.message;
  res.locals.error = process.env.NODE_ENV !== 'production' ? err : {};
  res.status(err.status || 500);
  res.render('error');
});

app.listen(app.get('port'), () => {
  console.log(app.get('port'), '번 포트에서 대기중');
});
```

### 14.8 routes폴더하위 index.js 코드작성
```js
const express = require('express');
const axios = require('axios');

const router = express.Router();

router.get('/test', async (req, res, next) => { // 토큰 테스트 라우터
  try {
    if (!req.session.jwt) { // 세션에 토큰이 없으면 토큰 발급 시도
      const tokenResult = await axios.post('http://localhost:8002/v1/token', {
        clientSecret: process.env.CLIENT_SECRET,
      });
      if (tokenResult.data && tokenResult.data.code === 200) { // 토큰 발급 성공
        req.session.jwt = tokenResult.data.token; // 세션에 토큰 저장
      } else { // 토큰 발급 실패
        return res.json(tokenResult.data); // 발급 실패 사유 응답
      }
    }
    // 발급받은 토큰 테스트
    const result = await axios.get('http://localhost:8002/v1/test', {
      headers: { authorization: req.session.jwt },
    });
    return res.json(result.data);
  } catch (error) {
    console.error(error);
    if (error.response.status === 419) { // 토큰 만료 시
      return res.json(error.response.data);
    }
    return next(error);
  }
});

module.exports = router;
```

### 14.9 토큰 재발급 받기









