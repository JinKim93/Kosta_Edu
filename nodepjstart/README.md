# 노트프로젝트 시작 및 패키지 설치
1. 폴더생성(lecture)
2. 폴더로 이동후 -> npm init
2.1 패키지이름적기 -> license: MIT로 적기
3. 필수패키지 다운로드 -> npm i -D nodemon, npm i express express-session nunjucks morgan cookie-parser sequelize mysql2 sequelize-cli, npm i multer 설치
4. package.json 수정

### 수정 전 사진
![image](https://user-images.githubusercontent.com/82345970/177068288-57983d37-ad7d-4846-a414-5d16b66efb4d.png)

### 수정 후 사진
1. node appjs를 nodemon으로 실행 할려고 수정 함 
![image](https://user-images.githubusercontent.com/82345970/177068405-8028eeed-9bff-4059-b5ab-23d607010e3a.png)

5. npx sequelize init 명령어 입력
    4 하기사진처럼 4개폴더 생김
![image](https://user-images.githubusercontent.com/82345970/177068621-4d18df01-691d-453c-bbe4-2d41defeaf97.png)

6. lecutre 폴더에, .env파일생성 후, npm i dotenv명령어 입력
7. lecture폴더에, views,public,routes폴더생성, app.js파일생성

![image](https://user-images.githubusercontent.com/82345970/177069169-60a95f1e-daac-4548-b622-113f2ffc8f3b.png)

8. app.js 내용작성
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
app.set('port', process.env.PORT || 8001); //개발시 포트 8001, 배포시, 443포트사용
app.set('view engine', 'html');
//넌적스 생성예제
nunjucks.configure('views', {
  express: app,
  watch: true,
});
//6장예제
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
//next 안쓰더라도, 생략하면 안된다(에러처리미들웨어에 한해서)
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

9. routes폴더에 page.js파일생성
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
//app.js pageRouter부분 / 이어서, /profile 이런식으로함,
//만약 app.js 부분이 user면 /user/profile로 됨
router.get('/profile', (req, res) => {
  res.render('profile', { title: '내 정보 - NodeBird' });
});

router.get('/join', (req, res) => {
  res.render('join', { title: '회원가입 - NodeBird' });
});

router.get('/', (req, res, next) => {
  const twits = [];
  res.render('main', {
    title: 'NodeBird',
    twits,
  });
});

module.exports = router;
```

10. page.js에보면 router들이 profile.html, join.html, main.html이 보임
- views폴더에 profile.html, join.html, main.html, layout.html, error.html 파일생성
- app.js보면 css제공해주는 public 써있음, css 정적파일은 public폴더에 들어있어야함

11. public 폴더에 main.css파일 생성
### database생성
1. npx sequelize db::create 명령어 입력하자
2. 입력하기 전에 하기 방법을 이용해 수정하자
- **lecture폴더 아래, config폴더에 config.json에 있는대로 생성됨**

![image](https://user-images.githubusercontent.com/82345970/177073313-c78c1000-0be3-4723-9609-703ab91af858.png)

- 에러발생될수 있으니까 mysql에 쓰일 내아이디랑 비밀번호를 적어줘야함
- 또한 DB(스키마명)도 적어줘야함

![image](https://user-images.githubusercontent.com/82345970/177073541-ee1fe545-f128-4e50-8215-35c94c22a144.png)

### config폴더, config.json 설명
![image](https://user-images.githubusercontent.com/82345970/177073744-187a4d97-4a53-45fe-bebd-30b1c23dbf92.png)

3. npx sequelize db::create 입력 -> 스키마생성 됨
4. 이제 테이블 생성하면 됨
5. models폴더 아래, index.js랑 관련있음(시퀄라이즈)
6. 기존 생성되있는거 맘에 안드므로, 제로초님이 한 방식으로 변경

### index.js
```js
const Sequelize = require('sequelize');
const env = process.env.NODE_ENV || 'development';//config.json development 가져옴
const config = require('../config/config')[env];
//앞으로 만들 모델들
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

### 7. user.js 파일생성( models폴더 아래)
```js
const Sequelize = require('sequelize');

module.exports = class User extends Sequelize.Model {
  static init(sequelize) {
    //시퀄라이즈는 ID 컬럼 생략됨, 알아서 만들어줌
    return super.init({
      email: {
        type: Sequelize.STRING(40),
        allowNull: true, //비어있어도 됨
        unique: true,   // 고유해야함, 빈값 2개 있어도 고유하게 해줌
      },
      nick: {
        type: Sequelize.STRING(15),
        allowNull: false, //필수다 not null
      },
      password: {
        type: Sequelize.STRING(100),
        allowNull: true, //100글자 까지 선택, sns로그인할때 비밀번호 없어도 됨 
      },
      //로그인제공자 provider 
      provider: {
        type: Sequelize.STRING(10),
        allowNull: false,
        defaultValue: 'local', //local이면 내 서비스이메일 비밀번호로 가입한거
        //local이 카카오라고하면 카카오톡을 통해 로그인한거다
      },
      snsId: {
        type: Sequelize.STRING(30),
        allowNull: true,
      },
    }, {
      sequelize,
      timestamps: true, //update at ,create at, delete at 기록됨 timestamp: true, paranoid : true이면
      underscored: false,
      modelName: 'User',
      tableName: 'users',
      paranoid: true,
      //한글입력되게 설정
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

### 8.post.js ( models폴더 아래)
```js
const Sequelize = require('sequelize');

module.exports = class Post extends Sequelize.Model {
  static init(sequelize) {

    //아이디는 생략되어있고, content랑 img 컬럼 들어가있음 
    return super.init({
      content: {
        type: Sequelize.STRING(140),
        allowNull: false,
      },
      //img한개만 올리기 가능하다
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
      paranoid: false, //deleteat 을 안하므로 false이다
      charset: 'utf8mb4', //mb4는 이모티콘 넣는거 가능
      collate: 'utf8mb4_general_ci',
    });
  }

  static associate(db) {
    db.Post.belongsTo(db.User);
    db.Post.belongsToMany(db.Hashtag, { through: 'PostHashtag' });
  }
};
```

### 9.hashtag.js파일생성(models폴더아래)
```js
const Sequelize = require('sequelize');

module.exports = class Hashtag extends Sequelize.Model {
  static init(sequelize) {
    return super.init({
      title: { //해시태그이름 칼럼
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

### 테이블관계정의
- User,Post(게시글) 1 대 다 관계
- Post Hashtag 다 대 다 관계 -> 하나의 게시글, 여러개 해시태그 가질수 있고, 하나의해시태그에, 여러개 게시글 속해있을수 있음
- User, User 관계 -> 다 대 다 관계 -> 팔로잉, 팔로워 관계
```js
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
```


- 관계 부분은 하기코드 부분처럼 작성해야함(7장 참고)
```js
  static associate(db) {
    db.Post.belongsTo(db.User);
    db.Post.belongsToMany(db.Hashtag, { through: 'PostHashtag' });
  }
};
``` 
### app.js에 시퀄라이즈 모듈 연결
- 하기 코드 추가
```js const { sequelize } = require('./models');

    sequelize.sync({ force: false }) //force: true 테이블 지워졌다가 다시생성(데이터날라감) -> 실무사용금지
    .then(() => {                   
        console.log('데이터베이스 연결 성공');
    })
    .catch((err) => {
        console.error(err);
    });
```

- 전체코드
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
app.set('port', process.env.PORT || 8001); //개발시 포트 8001, 배포시, 443포트사용
app.set('view engine', 'html');
//넌적스 생성예제
nunjucks.configure('views', {
  express: app,
  watch: true,
});
sequelize.sync({ force: false }) //force: true 테이블 지워졌다가 다시생성(데이터날라감) -> 실무사용금지
    .then(() => {                   
        console.log('데이터베이스 연결 성공');
    })
    .catch((err) => {
        console.error(err);
    });
//6장예제
app.use(morgan('dev'));
//css제공해주는 부분 public, css정적파일은 public폴더에 들어있어야함
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
//next 안쓰더라도, 생략하면 안된다(에러처리미들웨어에 한해서)
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
- 테이블 변경 또는 삭제 할때 workbench 들어가서 drop 후, vs코드에서 수정후 npm start 다시해주자

### 로그인,로그아웃, 회원가입 진행
1. 필요한 passport모듈설치
- npm i passport passport-local passport-kakao bcrypt 명령어 입력
- bcrypt는 해시화 도와줄 모듈이다

### 패스포트 처리과정
- 로그인을 할려면 회원가입이 필요함
- 회원가입 부터 만들자
- routes폴더에 auth.js파일생성

### 엄청초기 회원가입라우터 소스코드(auth.js)
```js
const express = require('express');
const bcrypt = require('bcrypt');
const User = require('../models/user');

const router = express.Router();

router.post('/join',  async (req, res, next) => {
  const { email, nick, password } = req.body; //프론트에서 이메일,닉,비번 보내줌
  try {
    const exUser = await User.findOne({ where: { email } }); //기존이메일로가입한사람있나?
    if (exUser) {
      return res.redirect('/join?error=exist');//있으면 프론트에 알려줌(서버에존재한다)
    }
    //해시화 해준다
    const hash = await bcrypt.hash(password, 12); //12얼마나 복잡하게 해시할건지 나타냄
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

### 라우터를 생성했으니까, app.js에서 불러와야함
- app.js에 추가
- const authRouter = require('./routes/auth');
- app.use('/auth',authRouter);

![image](https://user-images.githubusercontent.com/82345970/177078169-2b138f1b-f4b6-477f-8cfd-2b4ecbe76370.png)

![image](https://user-images.githubusercontent.com/82345970/177078271-f4ab18c9-a735-452a-aaeb-37fc2a432f82.png)


### 프로젝트 폴더 하위에 passport 폴더생성
1. passport폴더 하위에 index.js파일생성
- indxe.js 소스코드
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

### passport폴더 하위에 localStrategy.js파일생성
- 패스포트는 전략을 사용함
- 로그인을 어찌할지 적어놓은 로직이다(전략)
- 소스코드
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

### routes폴더 하위 auth.js파일 소스코드 수정
- 하기코드 추가
- 미들웨어 확장소스코드
```js
router.post('/login', (req, res, next) => {
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
```
- 전체코드
```js
const express = require('express');
const bcrypt = require('bcrypt');
const User = require('../models/user');
const passport = require('../passport');

const router = express.Router();

router.post('/join',  async (req, res, next) => {
  const { email, nick, password } = req.body; //프론트에서 이메일,닉,비번 보내줌
  try {
    const exUser = await User.findOne({ where: { email } }); //기존이메일로가입한사람있나?
    if (exUser) {
      return res.redirect('/join?error=exist');//있으면 프론트에 알려줌(서버에존재한다)
    }
    //해시화 해준다
    const hash = await bcrypt.hash(password, 12); //12얼마나 복잡하게 해시할건지 나타냄
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


router.post('/login', (req, res, next) => {
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


module.exports = router;
```

### 로그아웃 라우터생성(routes폴더 -> auth.js)
- auth.js에 소스추가
```js
router.get('/logout', isLoggedIn, (req, res) => {
    req.logout();
    req.session.destroy();
    res.redirect('/');
  });
```  

### passport폴더 하위에 kakaoStrategy.js파일생성



