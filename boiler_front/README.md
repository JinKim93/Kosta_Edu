## boiler_front

### 1. 서버만든 폴더(boiler)하위에 client,server 폴더생성

### 2. server폴더에, server관련 코드 move

![image](https://user-images.githubusercontent.com/82345970/178127213-a7c55aa2-ddc5-4ce8-aad6-82d79025d457.png)

### 3. client 폴더로 이동후 , npx create-react-app . 설치

### 4. react 실행해보기
- react설치되 있는 폴더 이동후 npm run start src폴더/APP.js파일이 랜더링되서 실행됨

### 5. webpack(모아준다)이 관리하는 범위 src폴더 하위만 관리함

![image](https://user-images.githubusercontent.com/82345970/178127472-d6b3b47d-867e-4fe2-8fc4-3e86926b626e.png)

### webpack은 pulic폴더는 관리 안하므로, 이미지파일을 넣을때, src폴더 안에 넣자


### 6. 하기 사진처럼 구조 변경

![image](https://user-images.githubusercontent.com/82345970/178127514-db4aa50f-c5cf-4e78-a603-22ed56fdbd01.png)

![image](https://user-images.githubusercontent.com/82345970/178127526-c67b94da-ee0d-4ccb-b2f5-b4cb3c14fab3.png)

### 7. redux를 위한 폴더생성 client/src폴더 하위에 만들기

![image](https://user-images.githubusercontent.com/82345970/178127628-260d424c-5fd2-4cc7-b190-e6bf521671fa.png)


### 8. src폴더하위, componets폴더생성, 그하위에, views폴더, LandingPage(처음페이지화면)폴더생성

![image](https://user-images.githubusercontent.com/82345970/178127679-13fb728d-8b8d-4fb5-8070-8f4469b961b8.png)

### 9. src폴더하위 -> Config.js파일생성

### 10. src폴더하위 -> App.test.js파일삭제, logo.svg파일삭제

![image](https://user-images.githubusercontent.com/82345970/178127714-babf12ee-62c0-4cde-91c2-ed5bd3192071.png)

### 11. componets/views폴더하위에 Footer,LoginPage,NavBar,RegisterPage 폴더 만들기

### 12. src폴더하위 utils,hoc폴더 만들기

### 13. Landingpage폴더 하위에, LandingPage.js파일생성(메인페이지화면)

### 13.2 LandingPage.js 코드작성
- rfce 친다음에 엔터누르면 자동완성 됨

![image](https://user-images.githubusercontent.com/82345970/178127836-706544e1-54e6-4ae4-94b4-d45f99901792.png)

### 14. LoginPage폴더하위에, LoginPage.js파일생성

### 14.2 LoginPage.js 코드작성
- rfce 친다음에 엔터누르면 자동완성 됨

![image](https://user-images.githubusercontent.com/82345970/178127859-0f1a9a52-6fb0-40a8-841b-18d16e7aec8c.png)

### 15. NavBar폴더하위에, NavBar.js파일생성

### 15.2  NavBar.js 코드작성
- rfce 친다음에 엔터누르면 자동완성 됨

![image](https://user-images.githubusercontent.com/82345970/178127879-35c4bcb8-4b2b-4ea6-b1b3-4d1a12c056c1.png)

### 16. RegisterPage폴더하위에, RegisterPage.js파일생성

### 16.2 RegisterPage.js 코드작성

![image](https://user-images.githubusercontent.com/82345970/178127915-64e61a4b-2919-4934-9d84-f1d12d131112.png)

### 17. Footer폴더하위, Footer.js파일생성

### 17.2 Footer.js 코드작성

![image](https://user-images.githubusercontent.com/82345970/178127930-0b1f1548-402a-443e-890c-6ed440eeaa2c.png)

### 18. 페이지 이동할때 React Router Dom을 사용함
- 강의에서는 v5기준으로 되있음, 2022년7월 V6버전으므로 하기 20번 처럼 코드 작성하자

### 19. react-router-dom 패키지 다운 받자
- npm install react-router-dom --save

### 20. App.js 코드작성(App.js 작성한 코드 페이지 라우팅 할수있게 코드작성)
- v5에 있는 switch -> route, component -> element

![image](https://user-images.githubusercontent.com/82345970/178128436-dedcdd89-002d-4b03-aa76-481344eced22.png)

```js
import { BrowserRouter, Route, Routes } from "react-router-dom";
import LandingPage from "./components/views/LandingPage/LandingPage";
import LoginPage from "./components/views/LoginPage/LoginPage";
import RegisterPage from "./components/views/RegisterPage/RegisterPage";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route exact path="/" element={<LandingPage />} />

        <Route exact path="/login" element={<LoginPage />} />

        <Route exact path="/register" element={<RegisterPage />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

### 20.2 페이지 작성한거 login 등 잘 넘어가는 게 보인다(즉 App.js파일 라우팅할수있게 해주었다)

![image](https://user-images.githubusercontent.com/82345970/178128483-0cdc6002-b33f-44fc-a83c-6b38cbe8928b.png)


### 21. 데이터 Flow & Axios

![image](https://user-images.githubusercontent.com/82345970/178128709-91c123ce-a656-464b-9bc7-529e01421657.png)

### 21.2 server에서 cleint 요청 보낼때 AXIOS라이브러리 사용함
- AXIOS란 JQuery사용할때 AJAX라고 보면됨

### 21.3 AXOIS 라이브러리 설치 npm install axios --save (client 폴더 이동후 설치하자)

### 22. requet를 서버에 임의로 보내기 test(componets/views/LandingPage.js)

![image](https://user-images.githubusercontent.com/82345970/178130268-c0534539-205b-4589-a9c5-3f51144e4a69.png)

```js
import React, { useEffect } from 'react';
import axios from 'axios';


function LandingPage() {

    useEffect(() =>{
        axios.get('/api/hello')//get request 서버에 보냄, endpoint/api.hello
        //서버쪽 index.js에서 cleint에서 보낸거 받아줌
        .then(response => console.log(response.data))//서버에서 response오는거 콘솔창으로 띄움
    }, []) 

  return (
    <div>
        LandingPage
    </div>
  )
}

export default LandingPage
```


### 22.2 cleint에서 requet한거 서버에받기 위한 소스코드작성(서버폴더이동(boiler)/index.js)

![image](https://user-images.githubusercontent.com/82345970/178130311-9082a5a0-fbd5-4e50-beaf-f907393264e5.png)

```index.js
const express = require('express');
const app = express();

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

//request 받는 라우터만듬
//초기test용 client쪽 LandingPag.js
app.get('/api/hello',(req,res)=>{

    res.send("안녕하세요~")//메시지를 프론트에 전달함
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
    


const port = 5000;

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
});
```

### 22.3 서버쪽 npm start, cleint 쪽 npm start


### 22.4 오류발생

![image](https://user-images.githubusercontent.com/82345970/178130249-2d4cd037-f279-421c-bbf1-3d46ae4c69fb.png)

### 22.4 오류발생이유(CORS이슈)
- 현재 설정으로 server는 포트 5000번, client는 포트 3000번 이다.
- client가 요청을 보내도, 서로 포트가 달라서, server는 받지 못하고 있음
- 사진에서 보는 origin는 server, client 각각 origin이다
- proxy 사용으로 해결가능

![image](https://user-images.githubusercontent.com/82345970/178130377-f3ff2c47-b9e3-4841-9a3f-b657b5bbafb4.png)

### 22.4 오류해결(proxy이용하자)
- react 공식문서 읽어보기 -> proxy관련
- npm install http-proxy-middleware --save 설치
- client폴더에 있는 src/setupProxy.js파일 생성하자

### src/setupProxy.js파일 소스코드
- 강의에서 하는대로 그대로 따라하면 안됨.


![image](https://user-images.githubusercontent.com/82345970/178130492-d6f94c4c-ac9f-480a-8818-97d4a3235d3f.png)

```js
const { createProxyMiddleware } = require('http-proxy-middleware');

module.exports = function(app) {
 app.use(
 '/api',
 createProxyMiddleware({
 //프론트 3000번에서 데이터 줄때, target을 5000번으로 주겠다
 target: 'http://localhost:5000',
 changeOrigin: true,
 }) );
};
```

### 22.4 이슈해결 후, 클라이언트에서 요청 받으면 res.send로 잘 보내진게 보인다

![image](https://user-images.githubusercontent.com/82345970/178130602-7c058c20-98e2-40cb-a8c7-812617fe62da.png)

### 23. proxy서버란

![image](https://user-images.githubusercontent.com/82345970/178130650-b076ab45-7480-4903-bb1f-cc734fc7b2ba.png)

### 24. concurrently 이용해서, back,front 서버 한번에 켜기
- 백,프론트 폴더 있는 최상위에서 npm install concurrently --save 패키지 설치

![image](https://user-images.githubusercontent.com/82345970/178131035-b2beed4a-0507-40f8-aaba-260278b48a32.png)

- 프로젝트구조가 boiler폴더/client/boiler2(서버) 이렇게 되있음
- boiler로 디렉토리 이동 후 패키지설치, 그다음 package.json에서도 상기사진처럼 수정

### 25. CSS Framwork사용하기(antd 사용하기)
- client 디렉토리 이동 후 
- 패키지 설치 npm install antd --save
- https://ant.design/docs/react/introduce 공식사이트

### 25.2 client폴더/src/index.js
- antd 관련 모듈 import 

![image](https://user-images.githubusercontent.com/82345970/178131174-3ba8c445-a3cd-4386-a3cc-a29d8b442135.png)

### 26. redux란?
- 상태 관리라이브러리
- redux is a predictable state container for JavaScript apps
- redux는 state를 관리해주는 tool라고 생각!!

### 26. state란?

![image](https://user-images.githubusercontent.com/82345970/178131213-9f6dee3e-9678-4b5c-b86b-b6abcec261f2.png)

- props 처럼, 부모컴포넌트에서 자식컴포넌트한테 주는게 아니다.
- 그냥 컴포넌트 안에서 이뤄짐
- 데이터를 교환, 전달 할려면 state를 사용해야함
- state은 컴포넌트에 안에서 value를 1에서 2로 변하게 할수 있다.
- state이 1에서 2로 변하면 re-render 된다

### 26. Props란?

![image](https://user-images.githubusercontent.com/82345970/178131240-4da55426-f0d0-44a3-be8e-0a6341a2879f.png)

- 하나의 부모컴포넌트가 있고, 자식컴포넌트가 부모 컴포넌트에 들어갈수 있다 
- 컴포넌트간 무엇인가 주고받을때에는 prop을 이용해줘야함
- prop은 소통하는 방식이, 부모 -> 자식, 위에서 아래로만 소통이 가능하다
- 부모컴포넌트에서, 자식컴포넌트한테 1이라는 value를 주었을때, 자식컴포넌트안에 있는 value 1은 변할수가 없다(불변 -> immutable)
- 변경을 할려면, 부모컴포넌트에서 값을 다시 내려줘야지 변경할수 있다. 


### 27. redux 패키지설치(client 디렉토리)
- npm install redux react-redux redux-promise redux-thunk --save
- redux-promise, redux-thunk는 react에서 redux를 잘 사용할수있게 해주는 미들웨어다

### 28. redux 모듈 추가 및 시작하기(client폴더하위/src/index.js)

![image](https://user-images.githubusercontent.com/82345970/178131932-9c9442f6-56e6-4d58-b2c4-67fa9a50bf1c.png)

### 28.2 src폴더하위/_reducers폴더하위에 index.js파일생성
- 현재 작성 기준에서 user는 없어서 주석처리 해줌

![image](https://user-images.githubusercontent.com/82345970/178132007-c99a6c8e-49a4-458b-887c-9be49160b247.png)


### 28.3 상기에 작성한 코드 import해주기(client폴더하위/src/index.js)

![image](https://user-images.githubusercontent.com/82345970/178132108-e47c536d-6f9a-4fe6-94fc-fba9c34d20d6.png)


### 28.4 reudx extension 다운로드
- 크롬에서 redux extension 검색 후 다운로드

### 28.5 redux extension 쓰기 위해서 소스코드 추가(client폴더하위/src/index.js) 어플리케이션에 redux 연결

![image](https://user-images.githubusercontent.com/82345970/178132162-3f6d638f-dd81-42e9-82f3-3b70f0cf6f59.png)


### 28.6 28.5까지 진행했을때 오류 생성

![image](https://user-images.githubusercontent.com/82345970/178133372-bb8e71cd-2c96-4a34-8230-15559840d9b4.png)

- 처음코드로 하면 안됨 -> 버전이 달라서 ??? createStore도 사진처럼 나옴

![image](https://user-images.githubusercontent.com/82345970/178133412-258098b4-d550-48ec-b079-7c351cb5d33e.png)

- 처음코드로 해서 실행하면 오류는 안나옴 하지만 localhost에 아무것도 안나옴 

![image](https://user-images.githubusercontent.com/82345970/178133441-6ea5b1ea-71a0-47d0-bc47-eb31bec7030d.png)

![image](https://user-images.githubusercontent.com/82345970/178133467-3f8ad994-8ecb-45c4-9ab2-6a22558fd866.png)


- 두번째 코드로 실행시 나오는 화면 

![image](https://user-images.githubusercontent.com/82345970/178133455-276bbc0a-aaa1-4928-841e-a298c03e02a1.png)



- 두번째코드는 됨 

```js
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';
import { Provider } from 'react-redux';
import 'antd/dist/antd.min.css';
//import 'antd/dist/antd.css';
import { applyMiddleware, createStore} from 'redux';
import promiseMiddleware from 'redux-promise';
import ReduxThunk from 'redux-thunk';
import Reducer from './_reducers';


const createStoreWithMiddleware = applyMiddleware(promiseMiddleware,ReduxThunk)(createStore)
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
   <React.StrictMode>
     <Provider>
       store={createStoreWithMiddleware(Reducer,
           window.__REDUX_DEVTOOLS_EXTENSION__ &&
           window.__REDUX_DEVTOOLS_EXTENSION__()

         )}
    

    <App />
    </Provider>
    
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();

```

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
//import * as serviceWorker from './serviceWorker';
import { Provider } from 'react-redux';
//import 'antd/dist/antd.css'; 이걸로 쓰면 안됨 
import 'antd/dist/antd.min.css';
import { applyMiddleware, createStore } from 'redux';
import promiseMiddleware from 'redux-promise';
import ReduxThunk from 'redux-thunk';
import Reducer from './_reducers';

const createStoreWithMiddleware = applyMiddleware(promiseMiddleware, ReduxThunk)(createStore)

ReactDOM.render(
    <Provider
        store={createStoreWithMiddleware(Reducer,
            window.__REDUX_DEVTOOLS_EXTENSION__ &&
            window.__REDUX_DEVTOOLS_EXTENSION__()
        )}
    >
        <App />
    </Provider>
    , document.getElementById('root'));

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
//serviceWorker.unregister();
```

### 오류해결된 소스코드 /src/index.js
- 표시한 부분 문제

![image](https://user-images.githubusercontent.com/82345970/178133827-c63904e1-65f7-403d-9bcf-6a66bf12449d.png)

### 29. 로그인페이지구현(Landingpage.js)코드수정 -> 메인페이지변경
- 하기부분 수정했음

![image](https://user-images.githubusercontent.com/82345970/178175720-bb80189e-ddb6-4eb2-b44f-aa27396f8e6e.png)

![image](https://user-images.githubusercontent.com/82345970/178175804-f1b32460-2043-49da-bdda-2d1880188079.png)


```js
import React, { useEffect } from 'react';
import axios from 'axios';


function LandingPage() {

    useEffect(() =>{
        axios.get('/api/hello')//get request 서버에 보냄, endpoint/api.hello
        //서버쪽 index.js에서 cleint에서 보낸거 받아줌
        .then(response => console.log(response.data))//서버에서 response오는거 콘솔창으로 띄움
    }, []) 

  return (
    <div style={{ display:'flex', justifyContent: 'center', alignItems: 'center'
                  , width: '100%', height: '100vh'
    }}>
        <h2>시작 페이지</h2>
    </div>
  )
}

export default LandingPage
```


### 30. 로그인페이지구현(LoginPage.js)
- 아직까지 메인페이지(LandingPage)에서 login페이지로 넘어가는게 구현 안되있어서,
- url에서 localhost:3000/login으로 들어가자

![image](https://user-images.githubusercontent.com/82345970/178176328-ab357af9-7804-4e34-949a-4c395ac8ec6d.png)

### 30.2 로그인페이지구현 초반부분(LoginPage.js)

![image](https://user-images.githubusercontent.com/82345970/178176465-0ea011fa-6d67-4d7e-b64e-288f4420735e.png)

![image](https://user-images.githubusercontent.com/82345970/178176507-42068878-3ead-4cd2-b390-bd77daaf62e0.png)


### 30.3 로그인페이지구현 초반부분(LoginPage.js)
- 현재까지 만든창에 타이핑을해도 입력 안됨

![image](https://user-images.githubusercontent.com/82345970/178176747-c1885a9d-e4cb-4b99-b40b-c9234ed49d19.png)

![image](https://user-images.githubusercontent.com/82345970/178176799-408c0501-a180-4d8f-a231-6394776c8457.png)

### 30.4 로그인페이지구현 초반부분(LoginPage.js) 

![image](https://user-images.githubusercontent.com/82345970/178178638-15cb0cc5-41e2-4aaa-91bb-13ea1d44fde9.png)

![image](https://user-images.githubusercontent.com/82345970/178178731-e855e654-8dc1-4bed-baab-d9c248928dfb.png)

```js
import React, { useState } from 'react'

function LoginPage() {

  //onChange변화주기 위해 state 구성
  //처음에는 빈칸이므로("")로 표현해줌
  const [Email, setEmail] = useState("")
  const [Password, setPassword] = useState("")

  const onEmailHandler = (event) => {

    setEmail(event.currentTarget.value)

  }

  const onPasswordHandler = (event) => {
    setPassword(event.currentTarget.value)
  }

  return (
    <div style={{ display:'flex', justifyContent: 'center', alignItems: 'center'
                  , width: '100%', height: '100vh'
    }}>

        <form style = {{ display:'flex', flexDirection:'column'}}>
            <label>Email</label>
            <input type="email" value = {Email} onChange = {onEmailHandler} />
            <label>Password</label>
            <input type="password" value = {Password} onChange = {onPasswordHandler} />
            <br />
            <button>
                Login
            </button>
        </form>
    </div>

      
  )
}

export default LoginPage
```

### 30.4 로그인페이지구현 초반부분(LoginPage.js) 

![image](https://user-images.githubusercontent.com/82345970/178180090-c44e7d4c-65a8-4fc3-976c-d1d9754871b8.png)

![image](https://user-images.githubusercontent.com/82345970/178180430-3f5bf9c2-b0e2-4a58-b0af-9c802156bbc9.png)

![image](https://user-images.githubusercontent.com/82345970/178180694-3cbad497-02d1-4305-a63f-3261a3ed2382.png)

![image](https://user-images.githubusercontent.com/82345970/178180649-517b406b-e26a-46d9-b72a-766740aefa29.png)


### 30.4 로그인페이지구현 -> 서버쪽에 데이터보내기


### 30.5 로그인페이지 로직
- 서버로 보낼대는 Axios를 이용 -> post라는 http메소드를이용 Axios.post('/api/users/login',Email,Password) -> 이런식으로 넣어줌

![image](https://user-images.githubusercontent.com/82345970/178181788-e6c2403d-d2bc-4588-90b5-6f4ac8751326.png)

- 서버쪽 index.js를 보면, 로그인을위한 api 등등 만들어 놓음 -> 여기다 보내는거다(하기사진 서버쪽 index.js)

![image](https://user-images.githubusercontent.com/82345970/178181428-3b8588f7-efe5-4825-ac9c-88d702754df8.png)

- 이메일을 받은걸 찾을것이다(하기사진 서버쪽 index.js)

![image](https://user-images.githubusercontent.com/82345970/178181547-834175df-2ef6-464a-98b5-655ea34c211b.png)

- 이메일이 있으면, 비밀번호가 맞는지 확인(하기사진 서버쪽 index.js)

![image](https://user-images.githubusercontent.com/82345970/178181607-7b06ce3a-bfc0-474c-9dc8-b64b003b5c12.png)

- 맞으면, 토큰생성 후 cookiel에 저장을 한 후, 클라이언트에 로그인성공 전달

![image](https://user-images.githubusercontent.com/82345970/178181683-5e5a283b-f05a-4b6d-953a-4c9957530c2c.png)

- 전해진걸 response로 받은 다음, 함수 안에서 처리할거 처리하면 됨(LoginPage.js)

![image](https://user-images.githubusercontent.com/82345970/178181859-b74ccd4d-2893-41eb-b68b-8c45e1be59c3.png)

### 하지만 필자는 redux를 사용할 것이다

### 31. 로그인페이지(LoginPage.js)
- Dispatch 모듈 import

![image](https://user-images.githubusercontent.com/82345970/178189578-18dcecca-c5a3-4e2f-84fd-951ddfaa979d.png)


### 31.2 Redux 데이터 Flow

![image](https://user-images.githubusercontent.com/82345970/178189514-796f491d-d731-4336-9b14-f26a0db9c784.png)

### 31.3 Redux사용하는 과정(Loginpage.js)

![image](https://user-images.githubusercontent.com/82345970/178190137-655b4880-0b5f-4fff-9a7a-002a00b35b46.png)

![image](https://user-images.githubusercontent.com/82345970/178190442-5780cd7a-bdd2-4d7c-a76e-cd802a146c46.png)

- loginUser만들지 않았는대, _actions폴더 안에 user_action.js 파일생성

### 31.4 user_action.js 설정
- 사진에 보면 오타 있음 reponse -> response로 바꿔야함

![image](https://user-images.githubusercontent.com/82345970/178191405-a8e3d7be-6f5b-4349-abb2-e9f9c7e7036b.png)


### 31.5 user_action.js Reducer로 보내는 방법 
- _reducers/user_action.js파일로 이동

- Reducer는 전 state하고, action(현재)을 nextstate
![image](https://user-images.githubusercontent.com/82345970/178191735-f2504c83-48a1-4144-8860-3cc6b9e0c239.png)

### 31.6 _actions/types.js파일생성
- type: "LOGIN_USER" 이런 type을 관리하기 위한 파일생성
- type을 따로 지정해줌(types.js)

![image](https://user-images.githubusercontent.com/82345970/178192825-0145a2b9-d40d-41c6-aaa5-97413981c54b.png)

- user_action.js 코드 수정

![image](https://user-images.githubusercontent.com/82345970/178192662-a8c2f653-1750-45d1-93ff-0a59239027f7.png)

### 31.7 _reducers/user_reducer.js에서도 type을 types.js에서 가져오게 import

![image](https://user-images.githubusercontent.com/82345970/178192988-749b4e53-d7c4-44cf-b4a4-d5e389cd9379.png)

### 31.8 user_reducer.js 코드수정

![image](https://user-images.githubusercontent.com/82345970/178193447-a5db7932-e7bf-4cf1-8059-a6a14f6a68ac.png)

### 31.9 Login[age.js 코드수정

![image](https://user-images.githubusercontent.com/82345970/178193702-7958763f-12e7-448b-815d-f41e210127d7.png)

### 31.10 user_action.js 코드수정

![image](https://user-images.githubusercontent.com/82345970/178193975-0df935b3-f850-4981-bab1-4f07887bba61.png)

































































































