# Adapter pattern
#### Adapter는 실생활에서 110v를 220v로 변경해주거나, 그반대로 해주는 돼지코라고 불리느 변환기를 예를 들수 있음
#### 호환성이 없는 기존클래스의 인터페이스를 변환하여 재사용 할 수 있도록 한다 -> SOLID중에서 개방폐쇄원칙(OCP)를 따른다

# 110V만 사용가능한제품 -> 220v제품을 110v로 변환시켜주는 예제
### 1. Electronic110V 인터페이스 생성, Electronic220V 인터페이스 생성
```java
package com.company.design.adapter;

public interface Electronic110V {

    void powerOn();
}
```
```java
package com.company.design.adapter;

public interface Electronic220V {

    void connect2();
}
```

### 2. 110v를 상속받은 HairDryer클래스 생성, 220v를 상속받은 Cleaner클래스 생성
```java
package com.company.design.adapter;

public class HairDryer implements Electronic110V {
    @Override
    public void powerOn() {
        System.out.println("헤어 드라이기 110V on");
    }
}
```
```java
package com.company.design.adapter;

public class Cleaner implements Electronic220V{
    @Override
    public void connect2() {
        System.out.println("청소기 220v on");
    }
}
```
### 3. SocketAdapter 클래스 생성 -> 변환기역할 클래스
```java
package com.company.design.adapter;

//220v가 110v로 변환될 클래스이다
//기본적으로 110v을 상속받아야함
public class SocketAdapter implements Electronic110V {

    //자기자신이 연결시켜줘야할 220v를 가지고 있어야함
    private Electronic220V electronic220V;


    public SocketAdapter(Electronic220V electronic220V) {
        this.electronic220V = electronic220V;

    }
    @Override
    public void powerOn() {
        electronic220V.connect2();
    }
}
```

### 4. main 클래스 생성
```java
package com.company.design;

import com.company.design.adapter.Cleaner;
import com.company.design.adapter.Electronic110V;
import com.company.design.adapter.HairDryer;
import com.company.design.adapter.SocketAdapter;

public class Main {
    public static void main(String[] args) {
        //110v짜리
        HairDryer hairDryer = new HairDryer();
        connect(hairDryer);

        //220v짜리이다
        Cleaner cleaner = new Cleaner();
        Electronic110V adapter = new SocketAdapter(cleaner);
        connect(adapter);


    }
    //콘센트 -> main자체도 static이여서 static메서드로 만들어줘야함
    public static void connect(Electronic110V electronic110V) {
        electronic110V.powerOn();
    }
}
```


