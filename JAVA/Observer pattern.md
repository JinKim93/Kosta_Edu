# Observer Pattern
### 변화가 일어났을때 미리 등록된 다른 클래스에 통보해주는 패턴
### event listener에서 해당패턴을 사용함

# Observer Pattern 예제
#### 1. IButtonListener 인터페이스생성
```java
package com.company.design.observer;

public interface IButtonListener {
    void clickEvent(String event);
}
```

#### 2. Button클래스 생성
```java
package com.company.design.observer;

public class Button {

    private  String name;
    private IButtonListener buttonListener;

    public Button(String name) {
        this.name = name;
    }

    public void click(String message) {
        buttonListener.clickEvent(message);
    }

    public void addListener(IButtonListener buttonListener) {
        this.buttonListener = buttonListener;
    }

}
```
#### 3. Main 클래스
```java
package com.company.design;

import com.company.design.observer.Button;
import com.company.design.observer.IButtonListener;

public class Main {
    public static void main(String[] args) {
        Button button = new Button("버튼");

        //익명클래스 생성
        button.addListener(new IButtonListener() {
            @Override
            public void clickEvent(String event) {
                System.out.println(event);
            }
        });
        button.click("메시지 전달 : click1");
        button.click("메시지 전달 : click2");
        button.click("메시지 전달 : click3");
        button.click("메시지 전달 : click4");




    }

}
```



# 결론
#### 리스너를 통해서, 옵저버패턴은 특정한이벤튼(버튼에대한클릭)이 일어났을때, 메시지를 리스너를통해서 이벤트를 전달해주는형태이다
#### 이벤트를 전달할일 있으면, 리스너를 전달해서, 객체리스너를 등록해두고, 이벤트를 전달해주는 패턴
