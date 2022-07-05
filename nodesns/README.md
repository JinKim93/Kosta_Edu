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

### 22. 회원가입 부분 소스코드(auth.js)
```js
const express = require('express');
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

### 23. 로그인은 로직을 깔끔하게 하기위해 passport라는 라이브러리사용함

### 24. lecture하위에 passport 폴더생성
- passport는 전략을 사용함
- 로그인 어찌할지 적어놓은파일 -> 전략
### 25. passport폴더 하위에 index.js, localStrategy.js(기본 아이디,비번로그인방식), kakaoStrategy.js(카카오연동 로그인방식) 파일생성

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

