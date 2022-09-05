# Strategy pattern
#### 유사한 행위들을 캡슐화하여, 객체의 행위를 바꾸고 싶은 경우 직접 변경하는 것이 아닌 전략만 변경하여,
#### 유연하게 확장하는 패턴 SOLID중에서 개방폐쇄원칙(OCP), 의존역전원칙(DIP)를 따른다

# Strategy pattern 예제
### 1. EncodingStrategy인터페이스 생성
```java
package com.company.design.strategy;

public interface EncodingStrategy {
    String encode(String text);
}
```

### 2. 인코딩사용하는인터페이스 정해짐 -> 이런전략을 사용하는 NormalStrategy, Base64Strategy 클래스생성
```java
package com.company.design.strategy;

public class NormalStrategy implements EncodingStrategy{
    @Override
    public String encode(String text) {
        return text;
    }
}
```


```java
package com.company.design.strategy;

import java.util.Base64;

public class Base64Strategy implements EncodingStrategy {
    @Override
    public String encode(String text) {
        return Base64.getEncoder().encodeToString(text.getBytes());
    }
}
```


### 3. 전략을 사용하는 인코더 생성 -> Encoder클래스 생성
```java
package com.company.design.strategy;

public class Encoder {
    private EncodingStrategy encodingStrategy;

    public String getMessage(String message){
        return this.encodingStrategy.encode(message);
    }

    public void setEncodingStrategy(EncodingStrategy encodingStrategy) {
        this.encodingStrategy = encodingStrategy;
    }
}
```

### 4-1 AppendingStrategy 클래스 추가
```java
package com.company.design.strategy;

public class AppendingStrategy implements EncodingStrategy{
    @Override
    public String encode(String text) {
        return "ABCD" + text;
    }
}
```

### 4-2 main클래스
```java
package com.company.design;

import com.company.design.strategy.*;

public class Main {
    public static void main(String[] args) {

        Encoder encoder = new Encoder();

        //base64전략생성
        EncodingStrategy base64 = new Base64Strategy();

        //normal
        EncodingStrategy normal = new NormalStrategy();

        EncodingStrategy append = new AppendingStrategy();

        String message = "hello java";

        encoder.setEncodingStrategy(base64);
        String base64Result = encoder.getMessage(message);
        System.out.println(base64Result);

        encoder.setEncodingStrategy(normal);
        String normalResult = encoder.getMessage(message);
        System.out.println(normalResult);

        encoder.setEncodingStrategy(append);
        String appendResult = encoder.getMessage(message);
        System.out.println(appendResult);











    }

}
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/188348477-227d0697-f028-4dd2-ad7b-9ed0c6352de2.png)


# 결론
#### 실제사용하는 원본객체는 그대로두고 Encoder encoder, 전략만 수정을해서, 다른결과를 얻어냄

![image](https://user-images.githubusercontent.com/82345970/188348783-6716fb8c-e44e-46ad-98a8-e40a74f5e654.png)



