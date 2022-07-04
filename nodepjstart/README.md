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
5. moduels폴더 아래, index.js랑 관련있음(시퀄라이즈)
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

### 7. user.js 파일생성( moduels폴더 아래)
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

### 8 post.js ( moduels폴더 아래)



