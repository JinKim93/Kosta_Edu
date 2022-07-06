### 1. 폴더생성(lecture), lecture 폴더로 이동
### 2. npm init 
![image](https://user-images.githubusercontent.com/82345970/177228243-49533224-4d0b-4c0e-9616-2523cf926dc8.png)

### 3. npm i -D nodemon, npm i express express-session nunjucks morgan cookie-parser sequelize mysql2 sequelize-cli, npm i multer 패키지 설치

### 4. package.json파일 수정
![image](https://user-images.githubusercontent.com/82345970/177228456-949ae8ae-5c17-43a7-9ae1-40ebdcaa5a73.png)

### 5. npx sequelize init
- 폴더생김(config,migrations,models,seeders)

### 6. lecture폴더 하위에 .env파일생성
- npm i dotenv 패키지 설치

### 7. lecture폴더 하위에 views,routes,public 폴더생성, app.js파일생성

### 8. .env파일코드작성
```js
 COOKIE_SECRET=cookiesecret
```

### 9. app.js 코드작성(초기1)
```js
const express = require('express');
const cookieParser = require('cookie-parser');
const morgan = require('morgan');
const path = require('path');
const session = require('express-session');
const nunjucks = require('nunjucks');
const dotenv = require('dotenv');

dotenv.config();
const pageRouter = require('./routes/page');

const app = express();
app.set('port', process.env.PORT || 8001);
//15 ~ 19 넌적스 설정방법
app.set('view engine', 'html');
nunjucks.configure('views', {
  express: app,
  watch: true,
});

//6장에 상세한내용 있음
app.use(morgan('dev'));
app.use(express.static(path.join(__dirname, 'public')));
app.use(express.json());
app.use(express.urlencoded({ extended: true }));
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

app.use('/', pageRouter);
//404처리 미들웨어
app.use((req, res, next) => {
  const error =  new Error(`${req.method} ${req.url} 라우터가 없습니다.`);
  error.status = 404;
  next(error);
});

//에러 미들웨어, 인자 next 생략하면 안됨 -> 에러처리미들웨어는 무조건 next써야함
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

### 10. routes폴더 하위에 page.js파일생성
- page.js(초기코드)
```js
const express = require('express');

const router = express.Router();

router.use((req, res, next) => {
  res.locals.user = null;
  res.locals.followerCount = 0;
  res.locals.followingCount = 0;
  res.locals.followerIdList = [];
  next();
});
//app.js pageRouter에 /이기떄문에, router.get 앞에 /profile 이런식으로 작성
router.get('/profile', (req, res) => {
  res.render('profile', { title: '내 정보 - NodeBird' });
});

router.get('/join', (req, res) => {
  res.render('join', { title: '회원가입 - NodeBird' });
});

router.get('/', (req, res, next) => {
  const twits = []; //메인 게시물 넣어줄공간 -> 빈배열로
  res.render('main', {
    title: 'NodeBird',
    twits,
  });
});

module.exports = router;
```

### 11. views폴더 하위에 error.html, join.html, layout.html, main.html, profile.html 파일생성
- npm start 명령어 입력
- 여기까지는 css파일이 없다. css는정적파일이다. app.js코드중 (path.join(__dirname,'public')이 있음 -> css public폴더안에 있어야함
- css파일이 없어서 404에러 보인다
![image](https://user-images.githubusercontent.com/82345970/177230692-65ac1127-5d59-407f-acbe-a1ecca69f567.png)


### 12. public폴더 하위에 main.css파일생성

### 13. Database세팅 
- npx sequelize db:create 명령어를 입력하면, config폴더에, config.json을 찾는다
- 명령어 입력하기 전에 하기 사진처럼 본인이 만든 DB정보에 맞게 적어주자
- npx sequelize db:create 명령어입력
- 스키마를 생성함 -> npx sequelize db:create -> models폴더하위 -> index.js랑 관련(시퀄라이즈) -> index.js 스키마생성
- 이제는 아래 테이블을 만들면됨(user.js, post.js, hashtag.js
![image](https://user-images.githubusercontent.com/82345970/177231143-19b9d40d-b971-420b-a638-d379307610f8.png)


### 14. models폴더 하위 -> index.js파일 원래있던코드에서, 다른스타일로변경
- index.js(초기코드)
```js
const Sequelize = require('sequelize'); //시퀄라이즈 불러옴
//env.NODE_ENV 따로 설정하지 않으면 기본값은 development이다
const env = process.env.NODE_ENV || 'development';
//config.json에 있는 development 가져옴
const config = require('../config/config')[env];
//User,Post,Hashtab 앞으로 만들 모델들
const User = require('./user');
const Post = require('./post');
const Hashtag = require('./hashtag');

const db = {};
const sequelize = new Sequelize(
  config.database, config.username, config.password, config,
);

db.sequelize = sequelize;
db.User = User;
db.Post = Post;
db.Hashtag = Hashtag;

User.init(sequelize);
Post.init(sequelize);
Hashtag.init(sequelize);

User.associate(db);
Post.associate(db);
Hashtag.associate(db);

module.exports = db;
```

### 15.models폴더 하위에 user.js파일생성 -> 사용자만듬
- user.js 초기코드
```js
const Sequelize = require('sequelize');

//mysql 테이블하고 매칭됨 -> class User extends ~~~~
module.exports = class User extends Sequelize.Model {
  static init(sequelize) {
    return super.init({            //시퀄라이즈는 id생략되어있음 -> primary키
      email: { 
        type: Sequelize.STRING(40),
        allowNull: true, //비어있어도됨
        unique: true, //고유해야함
      },
      nick: {
        type: Sequelize.STRING(15),
        allowNull: false, //닉네임 15글자 필수
      },
      password: {
        type: Sequelize.STRING(100),
        allowNull: true, //비밀번호 선택 -> 비밀번호 없어도됨, -> 카카오 로그인할때 
      },
      //로그인제공자 
      provider: {
        type: Sequelize.STRING(10),
        allowNull: false,
        defaultValue: 'local', //local이 카카오면 카카오를 통해서 로그인한거다
      },
      snsId: {
        type: Sequelize.STRING(30),
        allowNull: true,
      },
    }, {
      sequelize,
      //timestamps, paranoid -> true -> createat, updateat, deleteat(생성일, 수정일, 삭제일) 기록됨
      timestamps: true, 
      underscored: false,
      modelName: 'User',
      tableName: 'users',
      paranoid: true,
      charset: 'utf8',
      collate: 'utf8_general_ci',
    });
  }

  static associate(db) {
    db.User.hasMany(db.Post);
    db.User.belongsToMany(db.User, {
      foreignKey: 'followingId',
      as: 'Followers',
      through: 'Follow',
    });
    db.User.belongsToMany(db.User, {
      foreignKey: 'followerId',
      as: 'Followings',
      through: 'Follow',
    });
  }
};
```

### 16. models폴더 하위에 post.js 파일생성
- post.js(초기코드)
```js
const Sequelize = require('sequelize');

module.exports = class Post extends Sequelize.Model {
  static init(sequelize) {
    return super.init({
      content: {
        type: Sequelize.STRING(140),
        allowNull: false,
      },
      img: {
        type: Sequelize.STRING(200),
        allowNull: true,
      },
    }, {
      sequelize,
      timestamps: true,
      underscored: false,
      modelName: 'Post',
      tableName: 'posts',
      paranoid: false,
      charset: 'utf8mb4', //mb4 이모티콘사용가능
      collate: 'utf8mb4_general_ci',
    });
  }

  static associate(db) {
    db.Post.belongsTo(db.User);
    db.Post.belongsToMany(db.Hashtag, { through: 'PostHashtag' });
  }
};
```

### 17. models폴더 하위에 hashtag.js 파일생성
```js
const Sequelize = require('sequelize');

module.exports = class Hashtag extends Sequelize.Model {
  static init(sequelize) {
    return super.init({
      title: {
        type: Sequelize.STRING(15),
        allowNull: false,
        unique: true,
      },
    }, {
      sequelize,
      timestamps: true,
      underscored: false,
      modelName: 'Hashtag',
      tableName: 'hashtags',
      paranoid: false,
      charset: 'utf8mb4',
      collate: 'utf8mb4_general_ci',
    });
  }

  static associate(db) {
    db.Hashtag.belongsToMany(db.Post, { through: 'PostHashtag' });
  }
};
```
### 테이블관계확인해보기
- 사용자, 게시글,해시태크 여러개 쓸수있다(1 대 다 관계)
- 게시글, 해시태그(다 대 다 관계) -> 하나의 게시글이 여러개 해시태그 가질수 있고, 하나의 해시태그 안에 여러개 속해있을수 있다
- 사용자, 사용자 관계(다 대 다 관계) -> 팔로워, 팔로잉
- 팔로워,팔로잉관계 소스코드 서로 반대되게 작성해야함
![image](https://user-images.githubusercontent.com/82345970/177234520-d1a76a39-607a-4b01-a637-c567e27cf688.png)

### 18. app.js에 시퀄라이즈 require 하기(소스코드 수정)
```js
const express = require('express');
const cookieParser = require('cookie-parser');
const morgan = require('morgan');
const path = require('path');
const session = require('express-session');
const nunjucks = require('nunjucks');
const dotenv = require('dotenv');

dotenv.config();
const pageRouter = require('./routes/page');
const { sequelize } = require('./models');
const app = express();
app.set('port', process.env.PORT || 8001);
app.set('view engine', 'html');
nunjucks.configure('views', {
  express: app,
  watch: true,
});
//시퀄라이즈 연결 -> sequelize.sync -> promise -> then,catch 붙이는게 좋음
sequelize.sync({ force: false }) //force: true -> 테이블지워졌다가 다시생성됨 -> 데이터 날라감
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

app.use('/', pageRouter);

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
![image](https://user-images.githubusercontent.com/82345970/177235345-8c6861c4-3838-4f2c-b5ff-8c9f2cdc20d9.png)

### 19. 로그인, 로그아웃, 회원가입 구현
- npm i passport passport-local passport-kakao bcrypt 패키지 설치

### 20. routes폴더 하위에 auth.js파일생성
- auth.js 초기소스코드
```
const express = require('express');
const bcrypt = require('bcrypt');
const User = require('../models/user');

const router = express.Router();

//회원가입 라우터
router.post('/join', async (req, res, next) => {
  const { email, nick, password } = req.body;
  try {
    const exUser = await User.findOne({ where: { email } });
    if (exUser) {
      return res.redirect('/join?error=exist');
    }
    const hash = await bcrypt.hash(password, 12);
    await User.create({
      email,
      nick,
      password: hash,
    });
    return res.redirect('/');
  } catch (error) {
    console.error(error);
    return next(error);
  }
});

module.exports = router;
```

### 21. auth.js를 만들었으니까, app.js에서 갖다써야함
- app.js 소스코드수정
```js
const express = require('express');
const passport = require('passport');
const cookieParser = require('cookie-parser');
const morgan = require('morgan');
const path = require('path');
const session = require('express-session');
const nunjucks = require('nunjucks');
const dotenv = require('dotenv');
dotenv.config();
const pageRouter = require('./routes/page');
const authRouter = require('./routes/auth');
const { sequelize } = require('./models');
const app = express();
app.set('port', process.env.PORT || 8001);
app.set('view engine', 'html');
nunjucks.configure('views', {
  express: app,
  watch: true,
});
//시퀄라이즈 연결 -> sequelize.sync -> promise -> then,catch 붙이는게 좋음
sequelize.sync({ force: false }) //force: true -> 테이블지워졌다가 다시생성됨 -> 데이터 날라감
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

app.use('/', pageRouter);
app.use('/auth', authRouter);
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

![image](https://user-images.githubusercontent.com/82345970/177236209-0c2660bc-be24-4147-bc2d-bcd7267c1db3.png)

### 22-1. 회원가입 부분 소스코드(auth.js)
```js
const express = require('express');
const passport = require('passport');
const bcrypt = require('bcrypt');
const User = require('../models/user');

const router = express.Router();

//회원가입 라우터
router.post('/join', async (req, res, next) => {
  //프론트에서 email.nick password 보내주면됨  
  const { email, nick, password } = req.body;
  //먼저 검사를 해봄, 기존에 email로 가입한 사람이 있는지
  try {
    const exUser = await User.findOne({ where: { email } });
    if (exUser) {
      return res.redirect('/join?error=exist'); //있으면 프론트에서 알림해줘야함 -> 이미가입한 이메일입니다 이런식으로
    }
    const hash = await bcrypt.hash(password, 12); //12는 얼마나 복잡하게 해시할건지를 나타냄 -> 숫자클수록 오래걸림 -> 해킹위험적음
    await User.create({
      email,
      nick,
      password: hash,
    });
    return res.redirect('/');
  } catch (error) {
    console.error(error);
    return next(error);
  }
});

module.exports = router;
```
### 22-2에서 auth라우터를 만들었으니까 app.js에서 쓰여야함
- app.js 표시한 부분추가 
![image](https://user-images.githubusercontent.com/82345970/177258962-048c8ed5-74aa-4c40-a418-2659a64d243f.png)


### 23. 로그인은 로직을 깔끔하게 하기위해 passport라는 라이브러리사용함(로그인구현)

### 24. lecture하위에 passport 폴더생성
- passport는 전략을 사용함
- 로그인 어찌할지 적어놓은파일 -> 전략
### 25. passport폴더 하위에 index.js, localStrategy.js(이메일,비번로그인방식), kakaoStrategy.js(카카오연동 로그인방식) 파일생성

### 26. index.js(초기 소스코드)
```js
const passport = require('passport');
const local = require('./localStrategy');
const kakao = require('./kakaoStrategy');
const User = require('../models/user');

module.exports = () => {
  passport.serializeUser((user, done) => {
    done(null, user.id);
  });

  passport.deserializeUser((id, done) => {
    User.findOne({ where: { id } })
      .then(user => done(null, user))
      .catch(err => done(err));
  });

  local();
  kakao();
};
```

### 27. localStrategy.js 초기소스코드
```js
const passport = require('passport');
const LocalStrategy = require('passport-local').Strategy;
const bcrypt = require('bcrypt');

const User = require('../models/user');

module.exports = () => {
  passport.use(new LocalStrategy({
    usernameField: 'email',
    passwordField: 'password',
  }, async (email, password, done) => {
    try {
      const exUser = await User.findOne({ where: { email } });
      if (exUser) {
        const result = await bcrypt.compare(password, exUser.password);
        if (result) {
          done(null, exUser);
        } else {
          done(null, false, { message: '비밀번호가 일치하지 않습니다.' });
        }
      } else {
        done(null, false, { message: '가입되지 않은 회원입니다.' });
      }
    } catch (error) {
      console.error(error);
      done(error);
    }
  }));
};
```

### 28. done함수 -> localStrategy.js에 나옴
- done함수 인수 3개를 받음
- done(null,false,{meesage: `가입되지 않은 회원입니다`});
- done(null, exUser)
- 첫번째 -> 서버에러, 두번째 -> 로그인성공했을때 유저객체, 세번째 -> 로그인실패했을때 메시지

### 29-1. 로그인구현소스코드(routes폴더 하위 auth.js)
```js
const express = require('express');
const passport = require('passport');
const bcrypt = require('bcrypt');
const User = require('../models/user');

const router = express.Router();

//회원가입 라우터
router.post('/join', async (req, res, next) => {
  //프론트에서 email.nick password 보내주면됨  
  const { email, nick, password } = req.body;
  //먼저 검사를 해봄, 기존에 email로 가입한 사람이 있는지
  try {
    const exUser = await User.findOne({ where: { email } });
    if (exUser) {
      return res.redirect('/join?error=exist'); //있으면 프론트에서 알림해줘야함 -> 이미가입한 이메일입니다 이런식으로
    }
    const hash = await bcrypt.hash(password, 12); //12는 얼마나 복잡하게 해시할건지를 나타냄 -> 숫자클수록 오래걸림 -> 해킹위험적음
    await User.create({
      email,
      nick,
      password: hash,
    });
    return res.redirect('/');
  } catch (error) {
    console.error(error);
    return next(error);
  }
});

//미들웨어 확장하는 패턴
//프론트에서 서버로 로그인요청을 보낼때 하기코드 라우터에 걸린다
// post -> authlogin을 하게 되면, 하기코드 실행됨
// passport.authenticate('local' -> 이부분 로컬이 실행되면, passport가 localStrategy를 찾는다
// passport폴더 -> index.js에 local();로 등록해줌
// local(); 등록을 해줘서 하기코드 router.post ~~~ 실행됨
// 프론트에서 로그인을 누를때, 이메일과비밀번호 같이보내줌
router.post('/login',(req, res, next) => {
    passport.authenticate('local', (authError, user, info) => {
      if (authError) {
        console.error(authError);
        return next(authError);
      }
      if (!user) {
        return res.redirect(`/?loginError=${info.message}`);
      }
      //로그인성공했을때 req.login을쓴다
      //req.login하는 순간 passport -> index.js로 간다
      //passport -> index.js -> passport.serializeUser 실행됨
      return req.login(user, (loginError) => {
        if (loginError) {
          console.error(loginError);
          return next(loginError);
        }
        //세션쿠키를 브라우저로 보내줌
        return res.redirect('/');
      });
    })(req, res, next); // 미들웨어 내의 미들웨어에는 (req, res, next)를 붙입니다.
  });

module.exports = router;
```

### 29-2. 로그인구현소스코드(passport폴더 하위 index.js)
```js
const passport = require('passport');
const local = require('./localStrategy');
const kakao = require('./kakaoStrategy');
const User = require('../models/user');

module.exports = () => {
  passport.serializeUser((user, done) => {
    done(null, user.id);//세션에 user의 id만 저장 



    
  });
  //세션에 id를 저장해야하는이유
  //{id: 3, 'connect.sid': s%3189203810391280 } -> connect.sid(세션쿠키)
  //세션쿠키는 브라우저로감
  //브라우저에서 요청을 보낼때마다 쿠키를 같이 넣어서 보내줌
  //서버가 s%3189203810391280 쿠키를 보고, 이 id는 3번id사용자의 쿠키구나 인지
  passport.deserializeUser((id, done) => {
    User.findOne({ where: { id } })
      .then(user => done(null, user))
      .catch(err => done(err));
  });
  //3번 id사용자를 deserializeUser에서 복구를 해줌 

  local();
  kakao();
};
```
### 29-3. 로그인구현소스코드(passport폴더 하위 localStrategy.js)
```js
const passport = require('passport');
const LocalStrategy = require('passport-local').Strategy;
const bcrypt = require('bcrypt');

const User = require('../models/user');

module.exports = () => {
  passport.use(new LocalStrategy({
    usernameField: 'email', //req.body.email가 되야함 -> 프론트에서 요청을해 이메일, 패스워드 보내줘야함
    passwordField: 'password', //req.body.password가 되야함 passwordField: 'password', //req.body.password password부분 같아야함
  }, async (email, password, done) => {
    try {
      const exUser = await User.findOne({ where: { email } });
      if (exUser) {
        const result = await bcrypt.compare(password, exUser.password);
        if (result) {
          done(null, exUser);
        } else {
          done(null, false, { message: '비밀번호가 일치하지 않습니다.' });
        }
      } else {
        done(null, false, { message: '가입되지 않은 회원입니다.' });
      }
    } catch (error) {
      console.error(error);
      done(error);
    }
  }));
};
```

### 29-4. 로그인구현소스코드(app.js)
```js
const express = require('express');
const cookieParser = require('cookie-parser');
const morgan = require('morgan');
const path = require('path');
const session = require('express-session');
const nunjucks = require('nunjucks');
const dotenv = require('dotenv');
dotenv.config();
const pageRouter = require('./routes/page');
const authRouter = require('./routes/auth');
const { sequelize } = require('./models');
const app = express();
app.set('port', process.env.PORT || 8001);
app.set('view engine', 'html');
nunjucks.configure('views', {
  express: app,
  watch: true,
});
//시퀄라이즈 연결 -> sequelize.sync -> promise -> then,catch 붙이는게 좋음
sequelize.sync({ force: false }) //force: true -> 테이블지워졌다가 다시생성됨 -> 데이터 날라감
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

app.use('/', pageRouter); 
app.use('/auth', authRouter);
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

### passport 과정(로그인)
- passport폴더하위 index.js 

![image](https://user-images.githubusercontent.com/82345970/177261047-e2b58d5f-4d3d-4c74-a68f-a81baa844a50.png)

1. serializeUser가 done 되는 순간
2. routes폴더하위 auth.js에 있는 하기소스코드 실행됨 -> 에러가 있으면 에러표시해주고, 없으면 return res.redirect('/'); (로그인성공)

![image](https://user-images.githubusercontent.com/82345970/177261521-1e3482ec-20ea-453a-877e-a726fb863f1e.png)


### passport 전체과정
1. routes폴더하위 auth.js 회원가입을 함

![image](https://user-images.githubusercontent.com/82345970/177261720-66931226-177d-4724-86d0-dc66d7434885.png)

2. 로그인요청이 들어오면 표시한 부분 local까지 실행되고

![image](https://user-images.githubusercontent.com/82345970/177262140-5f80dd10-baf6-450f-9de0-c073c0c8dba1.png)

3. passport폴더하위 localStrategy.js로가서 가입되지않은회원인지,비밀번호가 일치하지 않은지, 로그인성공인지 판별을 함
- 하기사진 로그인성공인지판별하는코드

![image](https://user-images.githubusercontent.com/82345970/177262454-f9167f5a-b828-46de-bccf-7d964d182d4d.png)

4. done실행되는 순간 routes폴더하위 auth.js로감
5. autherror부분 콜백함수가 실행됨

![image](https://user-images.githubusercontent.com/82345970/177262751-a1316c33-87b4-418c-86e5-2cf28710f94f.png)

6. 로그인성공하는순간(req.login)

![image](https://user-images.githubusercontent.com/82345970/177263123-e836bd62-6d16-4d7c-865b-9431caefbd65.png)

7. passport하위폴더 index.js로 감
- serializeUser로가서 user중에서 id만 {id: 3, 'connect.sid': s%3189203810391280 } 세션쿠키랑 id매칭되게 메모리에 들고있고

![image](https://user-images.githubusercontent.com/82345970/177263312-6c626064-52e7-493d-b5d0-4dc2150d6742.png)

8. 다시 done하는순간

![image](https://user-images.githubusercontent.com/82345970/177263634-f4ca368f-7095-4a0a-bd78-d43c943b764b.png)

9. routes폴더하위 auth.js에 있는 로그인에러가서 최종적으로 로그인에러있나 확인함

![image](https://user-images.githubusercontent.com/82345970/177263861-01096085-0b3f-4df9-93ad-51ebfa2f911d.png)

10. 로그인성공하면 다시 메인페이지로 돌려보내줌

![image](https://user-images.githubusercontent.com/82345970/177263927-10b8bbd8-66a5-44ee-a062-3ba796d5b054.png)

11. 여기서 req.login 하면서 숨겨져있는게 세션쿠키를 브라우저로 보내줌</br>
s%3189203810391280 } 이 쿠키를 브라우저로 보내줘서 res.redirect('/') 브라우저로 들어가는순간</br>
세션쿠키가 브라우저로 들어가게되고 그다음 요청부터는 세션쿠키가 보내줘서</br> 
서버가 그 요청을 누가 보냈는지 알수있게 됨  -> 즉 로그인된 상태가 됨 

### 30. 로그아웃구현(auth.js)
- routes하위폴더 auth.js로 이동
- 하키코드추가

![image](https://user-images.githubusercontent.com/82345970/177264948-3312ef3d-58c4-409d-8787-83a19da04922.png)

- auth.js소스코드
```js
const express = require('express');
const passport = require('passport');
const bcrypt = require('bcrypt');
const User = require('../models/user');

const router = express.Router();


router.post('/join', async (req, res, next) => {
 
  const { email, nick, password } = req.body;
 
  try {
    const exUser = await User.findOne({ where: { email } });
    if (exUser) {
      return res.redirect('/join?error=exist'); //있으면 프론트에서 알림해줘야함 -> 이미가입한 이메일입니다 이런식으로
    }
    const hash = await bcrypt.hash(password, 12); //12는 얼마나 복잡하게 해시할건지를 나타냄 -> 숫자클수록 오래걸림 -> 해킹위험적음
    await User.create({
      email,
      nick,
      password: hash,
    });
    return res.redirect('/');
  } catch (error) {
    console.error(error);
    return next(error);
  }
});

//미들웨어 확장하는 패턴
//프론트에서 서버로 로그인요청을 보낼때 하기코드 라우터에 걸린다
// post -> authlogin을 하게 되면, 하기코드 실행됨
// passport.authenticate('local' -> 이부분 로컬이 실행되면, passport가 localStrategy를 찾는다
// passport폴더 -> index.js에 local();로 등록해줌
// local(); 등록을 해줘서 하기코드 router.post ~~~ 실행됨
// 프론트에서 로그인을 누를때, 이메일과비밀번호 같이보내줌
router.post('/login',(req, res, next) => {
    passport.authenticate('local', (authError, user, info) => {
      if (authError) {
        console.error(authError);
        return next(authError);
      }
      if (!user) {
        return res.redirect(`/?loginError=${info.message}`);
      }
 
      return req.login(user, (loginError) => {
        if (loginError) {
          console.error(loginError);
          return next(loginError);
        }
        
        return res.redirect('/');
      });
    })(req, res, next); // 미들웨어 내의 미들웨어에는 (req, res, next)를 붙입니다.
  });

//라우터생성  
router.get('/logout', (req, res) => {
    req.logout(); //세션쿠키가 사라짐 -> 서버에서 세션쿠키지움 { id: 3, 'connect.sid': s%312312312312 }
    //서버에서 세션쿠키가 지워지면 로그아웃이 풀린거다
    //로그인이 풀렸는지 볼려면, 세션에 세션쿠키(s%312312312312)가 들어있나 확인하면 됨
    req.session.destroy();
    res.redirect('/');
  });  

module.exports = router;
```

### 31. 로그인 후 그다음 요청이 어찌되는지 확인
- 로그인을 해서, Strategy.js로 갔다가,   passport.serializeUser로 갔다가 결국 로그인해서 브라우저로 돌아감(return res.redirect('/');
- 그러면 브라우저에서 다음요청을 보낼것이다 -> 예를들어 게시글쓸래요, 팔로우할래요 등등
- 이런 요청들을 보낼때 app.js로 가서, 표시한 부분 추가 -> 즉 미들웨어 2개를 연결해줘야함

![image](https://user-images.githubusercontent.com/82345970/177265900-c0a723f0-8bfe-485a-a82d-7103f92b943c.png)

- router에 가기전에 미들웨어 2개를 연결해줘야함

![image](https://user-images.githubusercontent.com/82345970/177266353-f3c03597-70aa-4c59-a13b-72810c426d10.png)

- 또한 express세션보다 아래있어야함 -> express세션에 session을 저장했기때문에 

![image](https://user-images.githubusercontent.com/82345970/177266501-77c0479f-7fd1-4721-97bb-efc2ca8b2eac.png)

- 미들웨어 2개가 express세션보다 아래에 위치하므로써, 얻을수있는역할은, 로그인후 그다음요청부터 -> passport.session()이 실행될때
- passport폴더하위 index.js에 있는부분이 실행됨(하기사진참고)

![image](https://user-images.githubusercontent.com/82345970/177267089-3c361f18-de7c-4e9f-9258-61c9c706d881.png)

- 지금까지 app.js 소스코드
```js
const express = require('express');
const cookieParser = require('cookie-parser');
const morgan = require('morgan');
const path = require('path');
const session = require('express-session');
const nunjucks = require('nunjucks');
const dotenv = require('dotenv');
const passport = require('passport');

dotenv.config();
const pageRouter = require('./routes/page');
const authRouter = require('./routes/auth');
const { sequelize } = require('./models');
const app = express();
app.set('port', process.env.PORT || 8001);
app.set('view engine', 'html');
nunjucks.configure('views', {
  express: app,
  watch: true,
});
//시퀄라이즈 연결 -> sequelize.sync -> promise -> then,catch 붙이는게 좋음
sequelize.sync({ force: false }) //force: true -> 테이블지워졌다가 다시생성됨 -> 데이터 날라감
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

app.use('/', pageRouter); 
app.use('/auth', authRouter);

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

### 32-1. routes폴더하위에 middlewares.js파일생성
- 미들웨어 2개 직접만들거다.
- 미들웨어는 req, res, next가 있는함수
- 로그인되있나 판단하는(isLoggedIn)함수, 로그인안했나판단하는(isNotLoggedIn)함수
- middlewares.js 소스코드
```js
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
      const message = encodeURIComponent('로그인한 상태입니다.');
      res.redirect(`/?error=${message}`);
    }
  };
```

### 32-2 middleware.js에 만든 함수를 routes폴더하위 auth.js에 즉 다른라우터들에 만들어놓은 미들웨어를 가져다쓰자
- auth.js에 부분에 소스코드 추가하자

![image](https://user-images.githubusercontent.com/82345970/177268563-44d7d3e6-5e1f-4dd4-873a-aa76e818c489.png)

![image](https://user-images.githubusercontent.com/82345970/177268856-1616a8dc-b89e-4cdf-80c7-26d2975538d4.png)

![image](https://user-images.githubusercontent.com/82345970/177269113-a04abdc9-7350-446d-bbec-52f9b09f768b.png)

![image](https://user-images.githubusercontent.com/82345970/177269361-24a244e7-f010-4a0d-bf12-4aee325a431f.png)

### 32-2 auth.js소스코드
```js
const express = require('express');
const passport = require('passport');
const bcrypt = require('bcrypt');
const User = require('../models/user');
const { isLoggedIn, isNotLoggedIn } = require('./middlewares');

const router = express.Router();

//로그인한 사람이 회원가입하면 안되니까 isNotLoggedIn써주자
//즉 로그인 안한사람들만 접근할수있게 추가해주자
router.post('/join',isNotLoggedIn, async (req, res, next) => {
 
  const { email, nick, password } = req.body;
 
  try {
    const exUser = await User.findOne({ where: { email } });
    if (exUser) {
      return res.redirect('/join?error=exist'); //있으면 프론트에서 알림해줘야함 -> 이미가입한 이메일입니다 이런식으로
    }
    const hash = await bcrypt.hash(password, 12); //12는 얼마나 복잡하게 해시할건지를 나타냄 -> 숫자클수록 오래걸림 -> 해킹위험적음
    await User.create({
      email,
      nick,
      password: hash,
    });
    return res.redirect('/');
  } catch (error) {
    console.error(error);
    return next(error);
  }
});

//미들웨어 확장하는 패턴
//프론트에서 서버로 로그인요청을 보낼때 하기코드 라우터에 걸린다
// post -> authlogin을 하게 되면, 하기코드 실행됨
// passport.authenticate('local' -> 이부분 로컬이 실행되면, passport가 localStrategy를 찾는다
// passport폴더 -> index.js에 local();로 등록해줌
// local(); 등록을 해줘서 하기코드 router.post ~~~ 실행됨
// 프론트에서 로그인을 누를때, 이메일과비밀번호 같이보내줌

//로그인라우터도, 로그인 안한사람들만 할수있게 해줌
router.post('/login',isNotLoggedIn, (req, res, next) => {
    passport.authenticate('local', (authError, user, info) => {
      if (authError) {
        console.error(authError);
        return next(authError);
      }
      if (!user) {
        return res.redirect(`/?loginError=${info.message}`);
      }
 
      return req.login(user, (loginError) => {
        if (loginError) {
          console.error(loginError);
          return next(loginError);
        }
        
        return res.redirect('/');
      });
    })(req, res, next); // 미들웨어 내의 미들웨어에는 (req, res, next)를 붙입니다.
  });

//로그아웃 라우터생성
//로그아웃은 로그인 한 사람만 로그아웃되게 검사
router.get('/logout',isLoggedIn, (req, res) => {
    req.logout(); 
    req.session.destroy();
    res.redirect('/');
  });  

module.exports = router;
```

### 33. 카카오로그인연동(passport폴더하위 kakaoStrategy.js)
- kakaoStrategy.js소스코드 
```js
const passport = require('passport');
const KakaoStrategy = require('passport-kakao').Strategy;

const User = require('../models/user');

module.exports = () => {
  passport.use(new KakaoStrategy({
    clientID: process.env.KAKAO_ID,
    callbackURL: '/auth/kakao/callback',
  }, async (accessToken, refreshToken, profile, done) => {
    console.log('kakao profile', profile);
    try {
      const exUser = await User.findOne({
        where: { snsId: profile.id, provider: 'kakao' },
      });
      if (exUser) {
        done(null, exUser);
      } else {
        const newUser = await User.create({
          email: profile._json && profile._json.kakao_account_email,
          nick: profile.displayName,
          snsId: profile.id,
          provider: 'kakao',
        });
        done(null, newUser);
      }
    } catch (error) {
      console.error(error);
      done(error);
    }
  }));
};
```

### 33-2 카카오를통해서로그인하기누를때를 위한 서버쪽 라우터생성
- routes폴더하위 auth.js에 코드추가
 
![image](https://user-images.githubusercontent.com/82345970/177277744-a902ab24-f746-4769-9fb0-25df880e16d9.png)

### 33-3 routes폴더하위 auth.js 소스코드
```js
const express = require('express');
const passport = require('passport');
const bcrypt = require('bcrypt');
const User = require('../models/user');
const { isLoggedIn, isNotLoggedIn } = require('./middlewares');

const router = express.Router();

//로그인한 사람이 회원가입하면 안되니까 isNotLoggedIn써주자
//즉 로그인 안한사람들만 접근할수있게 추가해주자
router.post('/join',isNotLoggedIn, async (req, res, next) => {
 
  const { email, nick, password } = req.body;
 
  try {
    const exUser = await User.findOne({ where: { email } });
    if (exUser) {
      return res.redirect('/join?error=exist'); //있으면 프론트에서 알림해줘야함 -> 이미가입한 이메일입니다 이런식으로
    }
    const hash = await bcrypt.hash(password, 12); //12는 얼마나 복잡하게 해시할건지를 나타냄 -> 숫자클수록 오래걸림 -> 해킹위험적음
    await User.create({
      email,
      nick,
      password: hash,
    });
    return res.redirect('/');
  } catch (error) {
    console.error(error);
    return next(error);
  }
});

//미들웨어 확장하는 패턴
//프론트에서 서버로 로그인요청을 보낼때 하기코드 라우터에 걸린다
// post -> authlogin을 하게 되면, 하기코드 실행됨
// passport.authenticate('local' -> 이부분 로컬이 실행되면, passport가 localStrategy를 찾는다
// passport폴더 -> index.js에 local();로 등록해줌
// local(); 등록을 해줘서 하기코드 router.post ~~~ 실행됨
// 프론트에서 로그인을 누를때, 이메일과비밀번호 같이보내줌

//로그인라우터도, 로그인 안한사람들만 할수있게 해줌
router.post('/login',isNotLoggedIn, (req, res, next) => {
    passport.authenticate('local', (authError, user, info) => {
      if (authError) {
        console.error(authError);
        return next(authError);
      }
      if (!user) {
        return res.redirect(`/?loginError=${info.message}`);
      }
 
      return req.login(user, (loginError) => {
        if (loginError) {
          console.error(loginError);
          return next(loginError);
        }
        
        return res.redirect('/');
      });
    })(req, res, next); // 미들웨어 내의 미들웨어에는 (req, res, next)를 붙입니다.
  });


router.get('/logout',isLoggedIn, (req, res) => {
    req.logout(); 
    req.session.destroy();
    res.redirect('/');
  });  
//카카오 누르기하면, passport.authenticate('kakao')실행됨 -> 실행되면 kakaoStrategy.js로 이동
router.get('/kakao', passport.authenticate('kakao'));

router.get('/kakao/callback', passport.authenticate('kakao', {
  failureRedirect: '/',
}), (req, res) => {
  res.redirect('/');
});


module.exports = router;
```

### 33-4 카카오로그인연동을하기위한 방법
1. https://developers.kakao.com/ 접속
2. 메뉴 -> 내 애플리케이션 클릭 -> 애플리케이션 추가하기
3. 플랫폼 -> web플랫폼 등록

![image](https://user-images.githubusercontent.com/82345970/177278759-9a6279f5-3ae6-4226-8f78-f10efcc0dec1.png)

4. 제품설정 -> 카카오로그인 -> 활성화설정 ON으로 해주자
5. RedirectURL 등록하기
 
![image](https://user-images.githubusercontent.com/82345970/177084201-0f55d324-9cf6-4925-8690-339d6ce7b189.png)

- auth/kakao/callback은 kakaoStrategy.js파일에 있는 callbackURL 적은것이다
 
7. 제품설정 -> 동의항목 들어감 -> 내가 받을것을 설정해주면 된다.

![image](https://user-images.githubusercontent.com/82345970/177084454-6fc3a83b-302e-452c-a21a-0e3e60143a6d.png)

- 앱설정 -> 앱키 -> REST API키 복사
- 복사한키 들고 .env파일로 가서 하기 사진 처럼 적어주기

![image](https://user-images.githubusercontent.com/82345970/177084757-04c9d43a-dce9-4512-82b3-ada9282e19d9.png)

### 33-5 npm start 실행 후 오류발생(Unknown authentication strategy "local")
- 이메일, 비밀번호 입력 후 로그인 버튼 누름
- 오류발생

![image](https://user-images.githubusercontent.com/82345970/177282546-8acdb5b4-3665-4ab9-b789-1d8460417636.png)

### 33-5 오류발생이유
- passport폴더하위에 index.js파일을 생성해서 module.export를 만들었는대 함수실행을 안해줌

![image](https://user-images.githubusercontent.com/82345970/177282934-4618013b-f459-4a00-98b3-ac124d414a77.png)

### 33-5 오류해결
- app.js로 가서 코드추가

![image](https://user-images.githubusercontent.com/82345970/177283771-923bfa33-ad9d-42f2-b904-8d4b18ecac99.png)

- app.js 소스코드
```js
const express = require('express');
const cookieParser = require('cookie-parser');
const morgan = require('morgan');
const path = require('path');
const session = require('express-session');
const nunjucks = require('nunjucks');
const dotenv = require('dotenv');
const passport = require('passport');

dotenv.config();
const pageRouter = require('./routes/page');
const authRouter = require('./routes/auth'); 
const { sequelize } = require('./models');
const passportConfig = require('./passport');

const app = express();
app.set('port', process.env.PORT || 8001);
app.set('view engine', 'html');
nunjucks.configure('views', {
  express: app,
  watch: true,
});
//시퀄라이즈 연결 -> sequelize.sync -> promise -> then,catch 붙이는게 좋음
sequelize.sync({ force: false }) //force: true -> 테이블지워졌다가 다시생성됨 -> 데이터 날라감
  .then(() => {
    console.log('데이터베이스 연결 성공');
  })
  .catch((err) => {
    console.error(err);
  }); 
passportConfig();

  
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

app.use('/', pageRouter); 
app.use('/auth', authRouter);

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

### 34. 오류발생(로그인을했는대, 로그인했다고 표시가 안됨)

![image](https://user-images.githubusercontent.com/82345970/177285470-db229c5a-2665-4ae8-885c-a9db9699f385.png)

### 34. 오류이유(로그인을했는대, 로그인했다고 표시가 안됨)
- routes폴더하위 page.js에 user: req.user 추가해줘야함

### 34. 오류해결(로그인을했는대, 로그인했다고 표시가 안됨)
- main페이지를 보여줄때(routes폴더하위 page.js)

- routes폴더 -> page.js 
- user: req.user 코드추가

![image](https://user-images.githubusercontent.com/82345970/177286265-4e46ad48-399e-405a-ba1e-e8be0888803f.png)

- **하기 처럼 소스코드를 추가하면, main.html {% if user %} user가 있으면 저 부분으로 감
![image](https://user-images.githubusercontent.com/82345970/177086474-6c2a165f-d677-4336-83be-1b6468cb72c2.png)

- **layout.html에서도 {% if user and user.id %} 유저가 존재할경우 하기사진 부분 보여줌

![image](https://user-images.githubusercontent.com/82345970/177086554-603e5efb-703a-44c3-87d5-7b5630dd7f69.png)

- **user가 존재하지 않으면 하기사진 부분을 화면에서 보여줌
![image](https://user-images.githubusercontent.com/82345970/177086675-cd69f55a-cb70-49bb-af8b-bcf7d841af7f.png)

### 35. 오류발생(로그인후 로그아웃 안됨)
![image](https://user-images.githubusercontent.com/82345970/177289335-bd7048dc-849e-4762-8019-c544f1c6b279.png)

### 35. 오류발생 (로그인후 로그아웃 안됨)auth.js 소스코드
- routes폴더하위 auth.js 부분 수정

![image](https://user-images.githubusercontent.com/82345970/177289747-7889a84d-442c-4ef5-9f8d-4e075a4c0118.png)


### 35. 오류이유(로그인후 로그아웃 안됨)
passport@0.6 버전 출시로 req.logout에 문제가 생김

### 35. 오류해결(로그인후 로그아웃 안됨)
- 콜백 함수를 제공하고 그 안에서 응답
 
![image](https://user-images.githubusercontent.com/82345970/177290017-45f3ba94-18ec-4976-ac9d-7571691cc25c.png)

### 35. 오류발생해결 후(로그인후 로그아웃 안됨) auth.js 소스코드
```js
const express = require('express');
const passport = require('passport');
const bcrypt = require('bcrypt');
const User = require('../models/user');
const { isLoggedIn, isNotLoggedIn } = require('./middlewares');

const router = express.Router();

//로그인한 사람이 회원가입하면 안되니까 isNotLoggedIn써주자
//즉 로그인 안한사람들만 접근할수있게 추가해주자
router.post('/join',isNotLoggedIn, async (req, res, next) => {
 
  const { email, nick, password } = req.body;
 
  try {
    const exUser = await User.findOne({ where: { email } });
    if (exUser) {
      return res.redirect('/join?error=exist'); //있으면 프론트에서 알림해줘야함 -> 이미가입한 이메일입니다 이런식으로
    }
    const hash = await bcrypt.hash(password, 12); //12는 얼마나 복잡하게 해시할건지를 나타냄 -> 숫자클수록 오래걸림 -> 해킹위험적음
    await User.create({
      email,
      nick,
      password: hash,
    });
    return res.redirect('/');
  } catch (error) {
    console.error(error);
    return next(error);
  }
});

//미들웨어 확장하는 패턴
//프론트에서 서버로 로그인요청을 보낼때 하기코드 라우터에 걸린다
// post -> authlogin을 하게 되면, 하기코드 실행됨
// passport.authenticate('local' -> 이부분 로컬이 실행되면, passport가 localStrategy를 찾는다
// passport폴더 -> index.js에 local();로 등록해줌
// local(); 등록을 해줘서 하기코드 router.post ~~~ 실행됨
// 프론트에서 로그인을 누를때, 이메일과비밀번호 같이보내줌

//로그인라우터도, 로그인 안한사람들만 할수있게 해줌
router.post('/login',isNotLoggedIn, (req, res, next) => {
    passport.authenticate('local', (authError, user, info) => {
      if (authError) {
        console.error(authError);
        return next(authError);
      }
      if (!user) {
        return res.redirect(`/?loginError=${info.message}`);
      }
 
      return req.login(user, (loginError) => {
        if (loginError) {
          console.error(loginError);
          return next(loginError);
        }
        
        return res.redirect('/');
      });
    })(req, res, next); // 미들웨어 내의 미들웨어에는 (req, res, next)를 붙입니다.
  });

router.get('/logout',isLoggedIn, (req, res) => {
    req.logout(()=>{
      req.session.destroy();
      res.redirect('/');
    }); 
  });

  
//카카오 누르기하면, passport.authenticate('kakao')실행됨 -> 실행되면 kakaoStrategy.js로 이동
router.get('/kakao', passport.authenticate('kakao'));

router.get('/kakao/callback', passport.authenticate('kakao', {
  failureRedirect: '/',
}), (req, res) => {
  res.redirect('/');
});


module.exports = router;
```

### 36.1 이미지 업로드 

![image](https://user-images.githubusercontent.com/82345970/177438984-7071cc2a-3a74-4075-89dc-ad51f01d8254.png)

- 로그인, 회원가입 formdata전송이 되긴하는대, app.js에서 보면 urlencoded라서 body-parser가 해석할수 있음
- main.html에 있는 enctype="multipart/form-data"는 body-parser로는 요청본문을 해석할 수 없음
- 해석을 하기위해서 **multer패키지** 필요

### 36.2 이미지 업로드 라우터구현
- routes폴더하위에 post.js파일생성(게시글작성한 라우터들을 모아놓음)
- **app.js에 소스코드 추가

![image](https://user-images.githubusercontent.com/82345970/177441296-36029242-696f-4a59-bfc1-4f1190e63834.png)

![image](https://user-images.githubusercontent.com/82345970/177441455-e2356150-a41a-4ef7-bed0-72781d5a14c8.png)

### 36.3 이미지 업로드 라우터구현(post.js 초기소스코드)
```js
const express = require('express');
const multer = require('multer');
const path = require('path');
const fs = require('fs');

const { Post, Hashtag } = require('../models');
const { isLoggedIn } = require('./middlewares');

const router = express.Router();

try {
  fs.readdirSync('uploads');
} catch (error) {
  console.error('uploads 폴더가 없어 uploads 폴더를 생성합니다.');
  fs.mkdirSync('uploads');
}

const upload = multer({
  storage: multer.diskStorage({
    destination(req, file, cb) {
      cb(null, 'uploads/');
    },
    filename(req, file, cb) {
      const ext = path.extname(file.originalname);
      cb(null, path.basename(file.originalname, ext) + Date.now() + ext);
    },
  }),
  limits: { fileSize: 5 * 1024 * 1024 },
});

router.post('/img', isLoggedIn, upload.single('img'), (req, res) => {
  console.log(req.file);
  res.json({ url: `/img/${req.file.filename}` });
});

module.exports = router;
```
### 36.3 express.static역할(post.js, app.js)
- app.js 부분 
![image](https://user-images.githubusercontent.com/82345970/177442561-a0928665-4bf2-4e68-865e-a89eba642db8.png)

- post.js 부분
![image](https://user-images.githubusercontent.com/82345970/177443159-5b56ca1a-d3d0-4d22-a60b-b4c3fa095d4d.png)

### 36.4 post.js코드수정
- 코드 수정전 **npm i multer 패키지설치**
- 코드 수정 후 **npm start**

![image](https://user-images.githubusercontent.com/82345970/177448059-de0923b4-1be4-4a64-9e15-6664d287406d.png)

```js
const express = require('express');
const multer = require('multer');
const path = require('path');
const fs = require('fs');

const { Post, Hashtag } = require('../models');
const { isLoggedIn } = require('./middlewares');
const { nextTick } = require('process');

const router = express.Router();

//업로드 폴더 만들어줌
try {
  fs.readdirSync('uploads');
} catch (error) {
  console.error('uploads 폴더가 없어 uploads 폴더를 생성합니다.');
  fs.mkdirSync('uploads');
}

const upload = multer({
  storage: multer.diskStorage({
    destination(req, file, cb) {
      cb(null, 'uploads/');
    },
    filename(req, file, cb) {
      const ext = path.extname(file.originalname);
      cb(null, path.basename(file.originalname, ext) + Date.now() + ext);
    },
  }),
  limits: { fileSize: 5 * 1024 * 1024 },
});
//img는 upload폴더에 들어있는대, 요청주소는 img가 된다. 
//요청과 실제파일주소가 다름 -> 이런역할을 해주는게 app.js에있는 express.static이다
router.post('/img', isLoggedIn, upload.single('img'), (req, res) => {
  console.log(req.file);
  res.json({ url: `/img/${req.file.filename}` });
});

router.post ('/', isLoggedIn, upload.none(), async (req, res, next)=> {
    try {
        const post = await Post.create({
            content: req.body.content,
            img: req.body.url,
            UserId: req.user.id,
        });
        res.redirect('/');
      } catch (error) {
        console.error(error);
        next(error);
      }
});

module.exports = router;


```

### 36.5 업로드폴더생성코드

![image](https://user-images.githubusercontent.com/82345970/177447597-1cd8d3db-0698-4cdf-8aef-f4baafae686d.png)

- post.js코드 보면 업로드폴더 만들어줌

![image](https://user-images.githubusercontent.com/82345970/177447611-269939fb-a289-4583-ba5d-ca105f69efab.png)


### 36.6 사진 업로드 후 메인에 업로드 안됨현상(오류)
- 상기오류랑 같다 -> 로그인 후 유저 정보 안뜸현상

![image](https://user-images.githubusercontent.com/82345970/177448540-5e5802be-1990-4beb-b584-88d460d632f7.png)


### 오류해결 전 소스코드(route폴더하위 page.js)

![image](https://user-images.githubusercontent.com/82345970/177448663-5217d7db-687e-4466-94f9-09550075b28c.png)

### 오류해결 소스코드(route폴더하위 page.js)
- 오류해결 소스코드는 user: req.user, 추가만해줬는대, render에 넣는 변수들은 res.locals로 뺌

![image](https://user-images.githubusercontent.com/82345970/177449268-c7b17562-a631-40cb-9acf-0af8e3b69ebc.png)

- 또한 로그인했는지, 안했는지는 user변수는 모든라우터에 쓰일거라서 뺴놓음(중복제거해줌)

![image](https://user-images.githubusercontent.com/82345970/177449403-6a4db802-15d0-4ece-a5a9-527d4bf534e2.png)

### 상기문제 오류해결 소스코드 (route폴더하위 page.js)
```js
const express = require('express');

const router = express.Router();

router.use((req, res, next) => {
  res.locals.user = req.user; //로그인했는지, 안했는지는 user변수는 모든라우터에 쓰일거라서 뺴놓음(중복제거해줌)
  next();
});

//app.js pageRouter에 /이기떄문에, router.get 앞에 /profile 이런식으로 작성
router.get('/profile', (req, res) => {
  res.render('profile', { title: '내 정보 - NodeBird' });
});

router.get('/join', (req, res) => {
  res.render('join', { title: '회원가입 - NodeBird' });
});

router.get('/', async (req, res, next) => {
  try {
      
    const posts = await Post.findAll({
      include: {
        model: User,
        attributes: ['id', 'nick'],
      },
      order: [['createdAt', 'DESC']],
    });
    //render에 넣는 변수들 res.locals로 뺄수있다 
    res.render('main', {
      title: 'NodeBird',
      twits: posts,
      //user: req.user,  -> res.locals.user = req.user;
    });
  } catch (err) {
    console.error(err);
    next(err);
  }
});

module.exports = router;
```

### 오류발생(Post is not defined)

![image](https://user-images.githubusercontent.com/82345970/177449619-bbd0eeeb-9286-4ebe-901b-82400bc63e82.png)

### 오류해결(Post is not defined)
- routes폴더하위 page.js에 소스코드 추가

![image](https://user-images.githubusercontent.com/82345970/177450160-d9db2833-f7d1-422b-b385-125aba3296c6.png)

### 오류발생(user is not defined)

![image](https://user-images.githubusercontent.com/82345970/177450207-e77449db-9750-4d0b-92e9-6c166c744549.png)

### 오류해결(user is not defined)
- routes폴더하위 page.js에 소스코드 추가

![image](https://user-images.githubusercontent.com/82345970/177450385-37927d96-7c98-4814-b2ec-54e75a02a3f2.png)


### 오류발생((D:\nodejs-book-master\ch9\lecture\views\main.html) [Line 32, Column 45] Error: Unable to call `followerIdList["includes"]`, which is undefined or falsey

![image](https://user-images.githubusercontent.com/82345970/177450417-93c11ad4-1cd0-4248-bfbe-8aee661aa511.png)

### 오류이유((D:\nodejs-book-master\ch9\lecture\views\main.html) [Line 32, Column 45] Error: Unable to call `followerIdList["includes"]`, which is undefined or falsey
- 프론트쪽코드는 완성되코드에, 팔로우,팔로잉기능을 넣어줬는대, 아직 백엔드쪽에서는 구현을 안해줬서 오류발생

### 오류해결((D:\nodejs-book-master\ch9\lecture\views\main.html) [Line 32, Column 45] Error: Unable to call `followerIdList["includes"]`, which is undefined or falsey
- 소스코드 추가(routes폴더하위 page.js)

![image](https://user-images.githubusercontent.com/82345970/177450835-45266375-f725-43e0-b949-327683451d36.png)

### 37.1 팔로잉 기능 구현
1. routes폴더하위 user.js파일생성

2. app.js에 user와연결할 라우터 추가 및 require 추가 

![image](https://user-images.githubusercontent.com/82345970/177456819-e75274f8-79b5-49b1-ac40-15071d930a95.png)

![image](https://user-images.githubusercontent.com/82345970/177457030-32fedef5-5849-43f0-b8f9-ede592c2e85b.png)

### 37.2 팔로잉 기능구현(user.js)소스코드
```js
const express = require('express');

//팔로우는 로그인한사람만 해야하니까 isLoggedIn
const { isLoggedIn } = require('./middlewares');
const User = require('../models/user');

const router = express.Router();

// POST /user/1/follow -> restapi를 따름
router.post('/:id/follow', isLoggedIn, async (req, res, next) => {
  try {
    const user = await User.findOne({ where: { id: req.user.id } });
    if (user) {                                               //getFollowings -> 팔로잉가져오기
      await user.addFollowings([parseInt(req.params.id, 10)]); // setFollowings -> 수정할수있음 
      //addFollowings가 복수기 때문에 배열쓴다 []
      res.send('success');
    } else {
      res.status(404).send('no user');
    }
  } catch (error) {
    console.error(error);
    next(error);
  }
}); 

module.exports = router;
```

### 37.3 팔로우,팔로잉 한 숫자 증가 기능

![image](https://user-images.githubusercontent.com/82345970/177458485-bcbc5453-2592-490e-9c14-2cd8207ebe24.png)

- views하위 layout.html소스코드랑 관련있음

![image](https://user-images.githubusercontent.com/82345970/177458634-8b135268-7166-4d7e-9f5d-88c5ebc79638.png)

- routes하위 page.js에서 작성한, 부분에 추가를 해줘야함
- 사진에서 보이는부분에 추가를 해도 되지만,

![image](https://user-images.githubusercontent.com/82345970/177458933-63f3c1da-9849-4273-8c26-036a07db432b.png)

- user를 넣은것 처럼 위에 올려서 넣을수도 있다
- 하지만 사진처럼 followerCount=0, 그부분이 0으로 되어있어서, 정보가 안들어가 있다 
![image](https://user-images.githubusercontent.com/82345970/177459028-6eacc403-51c8-47d9-86d4-243f1670b5ce.png)

- 하기사진처럼 page.js 부분 수정하자

![image](https://user-images.githubusercontent.com/82345970/177460007-618e6cd5-3b39-4bb5-8655-6852e00d107d.png)

### 37.4 팔로우,팔로잉 한 숫자 증가기능 코드설명

![image](https://user-images.githubusercontent.com/82345970/177460007-618e6cd5-3b39-4bb5-8655-6852e00d107d.png)

- 로그인한경우(req.user), 팔로우,팔로잉 수를 알려줌
- followerIdList -> followingIdList가 변수명이 적합함
- 팔로잉한사람들 리스트를 가져야하는 이유는, 팔로우하기버튼은 이미팔로우한사람은 안보여줘도 됨 -> 오히려 unfollow를 보여줘야함
- 이런 경우가 있어서 followerIdList를 가지고 있어야함
- req.user 어디서나왔을까? passport폴더하위 index.js에 있는 deserializeUser에서 나온다
- passport폴더하위 index.js 수정해주자

![image](https://user-images.githubusercontent.com/82345970/177463264-c447520b-e5ff-48c8-9ff3-833d7f1a32cc.png)

- 결론 req.user는 deserializeUser에서 생성됨
- 게시글을 가지고 오고 싶으면 하기사진처럼 추가해주면 됨

![image](https://user-images.githubusercontent.com/82345970/177463675-8ac4111f-3b70-4220-b7b5-463cfc1ccd47.png)

### 37.5 팔로우,팔로잉 한 숫자 증가기능 코드(passport하위 index.js)
```js
const passport = require('passport');
const local = require('./localStrategy');
const kakao = require('./kakaoStrategy');
const User = require('../models/user');

module.exports = () => {
  passport.serializeUser((user, done) => {
    done(null, user.id);
  });

  passport.deserializeUser((id, done) => {
    User.findOne({
      where: { id },
      include: [{
        //둘다 model: User라서, as로 구별을 해줘야함
        model: User,
        attributes: ['id', 'nick'],
        as: 'Followers',
      }, {
        model: User,
        attributes: ['id', 'nick'],
        as: 'Followings',
      }],
    })
      .then(user => done(null, user))
      .catch(err => done(err));
  });

  local();
  kakao();
};
```




