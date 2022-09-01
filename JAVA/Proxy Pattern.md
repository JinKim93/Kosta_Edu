# Proxy Pattern
#### Proxy는 대리인 이라는 뜻, 뭔가를 대신해서 처리하는 것
#### Proxy Class를 통해서 전달 하는 형태로 설계되며, 실제 Client는 Proxy로 부터 결과를 받는다
#### cache 기능으로 활용이 가능하다
#### SOLID중에서 개방폐쇄원칙(OCP)와 의존역전원칙(DIP)를 따른다

# Proxy Pattern 실습 -> cache 할용
#### 캐시기능은 브라우저에서 활용한다, 인터넷통신에서 임의 받아온 결과가 있다면, 결과를 그대로 내려줌
#### 서버에서도 특정한데이터, 자주변경되지 않는 데이터, 메모리에 캐싱해놨다가 같은결과를 요청해 왔을때 사용함

### 1. IBrowser 인터페이스 생성
```java
package com.company.design.proxy;

public interface IBrowser {
    //Html 리턴을 함
    Html show();
}
```

### 2. Html 클래스 생성
```java
package com.company.design.proxy;

public class Html {

    private String url;

    public Html(String url) {
        this.url = url;
    }
}
```

### 3. Browser 클래스 생성
```java
package com.company.design.proxy;

public class Browser implements IBrowser{

    private String url;

    public Browser(String url) {
        this.url = url;
    }

    @Override
    public Html show() {
        //브라우저에서 어떤페이지 show하면, 매번 새로운주소(url)로딩하면서
        //html파일을 만들어서 내려주는 형태
        System.out.println("browser loading html from : " + url);
        return new Html(url);
    }
}
```
### 4. main 클래스 생성
```java
package com.company.design;

import com.company.design.proxy.Browser;
import com.company.design.proxy.BrowserProxy;
import com.company.design.proxy.IBrowser;

public class Main {
    public static void main(String[] args) {
        Browser browser = new Browser("www.naver.com");
        browser.show();
        browser.show();
        browser.show();

//        IBrowser browser = new BrowserProxy("www.naver.com");
//        browser.show();
//        browser.show();
//        browser.show();
//        browser.show();


    }

}
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/187832057-0753e241-2b50-4913-a204-e4ffd0b898fa.png)

### 5. 4번까지 작성한 코드 출력결고랑 5번 이후 출력결과 비교 할것이다 -> BrowserProxy 클래스생성
```java
package com.company.design.proxy;

public class BrowserProxy implements IBrowser{

    private String url;
    private Html html;

    public BrowserProxy(String url) {
        this.url = url;
    }

    @Override
    public Html show() {

        //캐싱기능
        if(html == null) {
            this.html = new Html(url);
            System.out.println("BrowserProxy loading html from : "+url);
        }
        System.out.println("BrowserProxy use cache html: "+url);
        return html;
    }
}
```
### 6. main클래스
```java
package com.company.design;

import com.company.design.proxy.Browser;
import com.company.design.proxy.BrowserProxy;
import com.company.design.proxy.IBrowser;

public class Main {
    public static void main(String[] args) {
//        Browser browser = new Browser("www.naver.com");
//        browser.show();
//        browser.show();
//        browser.show();

        IBrowser browser = new BrowserProxy("www.naver.com");
        browser.show();
        browser.show();
        browser.show();
        browser.show();


    }

}
```

### 출력결과
#### 한번요청된거 캐싱된걸로 요청결과를 받음

![image](https://user-images.githubusercontent.com/82345970/187832242-976d70d5-9d2a-456c-a9cb-73e2f827f21b.png)<br></br>

# AOP(관점 지향 프로그래밍)활용 예제
#### 특정한 메서드가 있으면, 메서드의실행시간, 특정한패키지에 있는 특정한 메서드의 실행시간, 전 후로 작업하고 싶은 부분들
#### 일괄적으로 특정한 요청에 대해서 request정보를 남김
#### 코드에 개별적으로 하는게 아니라, 일괄적으로 특정패키지에 있는 모든 메서드들 전, 후 에 있는 기능을 넣을수 있는것<br></br>
### 1. AopBrowser 클래스 생성
```java
package com.company.design.aop;

import com.company.design.proxy.Html;
import com.company.design.proxy.IBrowser;

public class AopBrowser implements IBrowser {

    private String url;
    private Html html;
    private Runnable before;
    private Runnable after;

    public AopBrowser(String url, Runnable before, Runnable after) {
        this.url = url;
        this.before = before;
        this.after = after;
    }
    public Html show() {
        before.run();

        if(html == null) {
            this.html = new Html(url);
            System.out.println("AOPBrowser html loading from : "+url);
            try {
                Thread.sleep(1500);
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }

        }
        after.run();
        System.out.println("AopBrowser html cache : " +url);
        return html;
    }
}
```

### 2.main 클래스생성
```java
package com.company.design;

import com.company.design.aop.AopBrowser;
import com.company.design.proxy.Browser;
import com.company.design.proxy.BrowserProxy;
import com.company.design.proxy.IBrowser;

import java.util.concurrent.atomic.AtomicLong;

public class Main {
    public static void main(String[] args) {


        //시간체크
        //동시성문제로 인해 AtomicLong사용
        AtomicLong start = new AtomicLong();
        AtomicLong end = new AtomicLong();

        IBrowser aopBrowser = new AopBrowser("www.naver.com",
                ()->{
                    System.out.println("before");
                    start.set(System.currentTimeMillis());

                },
                ()-> {
                    long now = System.currentTimeMillis();
                    //현재시간 - 이전시간 = 끝난시간 -> end시간에는 총 몇초 걸렸는지 들어감
                    end.set(now - start.get());
                }

        );
        aopBrowser.show();
        System.out.println("loading time : " +end.get());

        aopBrowser.show();
        System.out.println("loading time : " +end.get());


    }

}
```
# 결론
#### AOP패턴은 프록시패턴을 활용하고있다 -> 특정한메서드(기능) 앞,뒤로 원하는기능 또는 앞,뒤로 넘어가는 argument에대해서 조작
#### 여러가지 기능 -> 흩어진공통된기능을 하나로 묶어줌

