## TEXT형태로 받는방법
### 1. ApiController클래스생성
```java
package com.example.hello.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/api")
public class ApiController {

    //TEXT 형태
    @GetMapping("/text")
    public String text(@RequestParam String account) {
        return account;

    }




}
```
### 결과확인
![image](https://user-images.githubusercontent.com/82345970/188763816-0a9dcdc8-d425-4166-8767-08d65ac2a260.png)
![image](https://user-images.githubusercontent.com/82345970/188763837-3f88d75c-7751-435c-a88c-e318790063c0.png)<br></br>

## JSON형태로 받기
### 1. 카멜케이스로 동작하게 body 만들어줌
```java
package com.example.hello.controller;

import com.example.hello.dto.User;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api")
public class ApiController {

    //TEXT 형태
    @GetMapping("/text")
    public String text(@RequestParam String account) {
        return account;

    }

    //JSON형태
    // req -> object mapper ->
    // User객체를 @RequestBody로 받아서 User로 리턴을 해줌
    //동작순서
    // req -> object mapper를 통해서 -> object로 바뀜 -> 현재method를탐 -> response나갈때 object를던짐 ->
    // objecct mapper를통해서 -> json으로 바뀐다음 -> response가 됨
    @PostMapping("/json")
    public User json(@RequestBody User user){
        return user;

    }





}
```
![image](https://user-images.githubusercontent.com/82345970/188764925-e168ad46-647f-4f0e-b37c-5cb839a45dd0.png)



### 2. dto패키지생성 -> User클래스생성(return하고 싶은 데이터 작성)
```java
package com.example.hello.dto;

public class User {
    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getPhoneNumber() {
        return phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    private String phoneNumber;
    private String address;

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", phoneNumber='" + phoneNumber + '\'' +
                ", address='" + address + '\'' +
                '}';
    }
}
```

### 1에서 작성한거 스네이크케이스로 바꿀것이다 -> dto패키지 -> User클래스 수정
![image](https://user-images.githubusercontent.com/82345970/188765164-e149a51d-efc5-400e-a318-c978b01bd08e.png)<br></br>

## PUT 리소스생성시 201 OK를 내려줌 -> 201 OK응답을 내려주는 방법
```java
package com.example.hello.controller;

import com.example.hello.dto.User;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api")
public class ApiController {

    //TEXT 형태
    @GetMapping("/text")
    public String text(@RequestParam String account) {
        return account;

    }

    //JSON형태
    // req -> object mapper ->
    // User객체를 @RequestBody로 받아서 User로 리턴을 해줌
    //동작순서
    // req -> object mapper를 통해서 -> object로 바뀜 -> 현재method를탐 -> response나갈때 object를던짐 ->
    // objecct mapper를통해서 -> json으로 바뀐다음 -> response가 됨
    @PostMapping("/json")
    public User json(@RequestBody User user){
        return user;

    }

    @PutMapping("/put")
    //PUT status을 201 응답내려주는 방법
    //ResponseEntity 사용
    public ResponseEntity<User> put(@RequestBody User user) {
        return ResponseEntity.status(HttpStatus.CREATED).body(user);


    }






}
```

## 페이지를 리턴해주는 컨트롤러 -> @Controller
### 1. Controller패키지 -> PageController 클래스생성
```java
package com.example.hello.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class PageController {
    @RequestMapping("/main")
    public String main() {
        return "main.html";
    }
}
```
### 2. 해당사진 경로에 main.html파일생성
![image](https://user-images.githubusercontent.com/82345970/188766541-a4484b97-a0fc-4c00-9c03-e755a48e2d2d.png)

### 결과확인
![image](https://user-images.githubusercontent.com/82345970/188766604-b32a42bd-5439-4ddc-abb4-18dcf233c672.png)

## @Controller에서 JSON을 내려주는 방식
### 1. @ResponseEntity 이용하는방법
### 2. @ResponseBody 이용하는 방법 -> 여기서는 2번방식이용할거다 -> PageController클래스 수정
```java
package com.example.hello.controller;

import com.example.hello.dto.User;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class PageController {
    @RequestMapping("/main")
    public String main() {
        return "main.html";
    }

    @ResponseBody
    @GetMapping("/user")
    public User user() {

        //타입추론 -> User user = new User();
        var user = new User();
        user.setName("jinkim");
        user.setAddress("KJ컴패니");
        return user;

    }
}
```

### 결과확인
![image](https://user-images.githubusercontent.com/82345970/188767587-25d3d493-b3c2-4342-b839-fcd86519835e.png)<br></br>

### 결과보면 dto패키지 -> User클래스에 있는것 중 name,address만 작성해서 나머지속성은 0, null로 나옴
### int default는 0, String default는 null이다<br></br>

## int에 대한 default null로 변경하는방법
### Integer 타입으로 변경
![image](https://user-images.githubusercontent.com/82345970/188767916-cb1dae11-838b-4711-9ee1-c2395ca57c78.png)

### 결과확인
![image](https://user-images.githubusercontent.com/82345970/188767967-f4837f4e-8953-437e-a95c-24444b102c91.png)<br></br>

## Response내릴때 null값 포함 안시키는방법
### dto패키지 -> User클래스
![image](https://user-images.githubusercontent.com/82345970/188768246-288e265d-f9f8-4584-9eb5-ad56a6c7c1ef.png)<br></br>

## 결론
### PageController에서는 @ResponseBody을 안내려주고, 따로 ApiController를 만들어서,@RestController 붙여서 정의하는게 정석이다







