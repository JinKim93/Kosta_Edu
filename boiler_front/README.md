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




























