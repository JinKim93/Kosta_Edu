# Decorator Pattern
#### 데코레이터 패턴은 기존클래슨느 유지하되, 이후 필요한 형탤 꾸밀 때 사용함
#### 확장이 필요한 경우 상속의 대안으로도 활용
#### SOLID중에서 개방폐쇄원칙(OCP) 의존역전원칙(DIP)를 따름

# Decorator Pattern 실습
### 1. ICar인터페이스 생성
```java
package com.company.design.decorator2;

public interface ICar {

    int getPrice();
    void showPrice();
}
```
#### 2. Audi클래스생성 -> 기본뼈대
```java
package com.company.design.decorator2;

public class Audi implements ICar{

    private int price;

    public Audi(int price) {
        this.price =price;
    }
    @Override
    public int getPrice() {
        return price;
    }

    @Override
    public void showPrice() {
        System.out.println("audi의 가격은 " +this.price + "원입니다");

    }
}
```

### 3. AudiDecorator클래스생성 -> 아우디의 등급을 올리기위한 데코레이트클래스
```java
package com.company.design.decorator2;

public class AudiDecorator implements ICar{

    protected ICar audi;
    protected String modelName;
    protected int modelPrice;

    public AudiDecorator(ICar audi,String modelName, int modelPrice) {
        this.audi = audi;
        this.modelName = modelName;
        this.modelPrice = modelPrice;
    }

    @Override
    public int getPrice() {
        return audi.getPrice() + modelPrice;
    }

    @Override
    public void showPrice() {
        System.out.println(modelName + "의 가격은" + getPrice() + "원 입니다");

    }
}
```

### 4. A3, A4, A5클래스 생성
```java
package com.company.design.decorator2;

public class A3 extends AudiDecorator{
    public A3(ICar audi, String modelName) {
        super(audi, modelName, 1000);
    }
}
```
```java
package com.company.design.decorator2;

public class A4 extends AudiDecorator{
    public A4(ICar audi, String modelName) {
        super(audi, modelName, 2000);
    }
}
```

### 5. main클래스 생성
```java
package com.company.design;

import com.company.design.decorator2.*;

public class Main {
    public static void main(String[] args) {

        ICar audi = new Audi(1000);
        audi.showPrice();

        //a3 등급올리기
        ICar audi3 = new A3(audi,"A3");
        audi3.showPrice();

        //a4
        ICar audi4 = new A4(audi,"A4");
        audi4.showPrice();

        //a5
        ICar audi5 = new A5(audi,"A5");
        audi5.showPrice();






    }

}
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/188341624-948cadc9-3b4e-44b8-8b4f-e065ef2dd8cf.png)

# 결론
#### 기본베이스를 두고, 등급이 올라갈때마다 가격이 올라가게끔, 데코레이팅을 함
#### 기본뼈대는 건들지 않고, 부가적인 첨가를 하면서, 속성을 변하시키는것 -> 데코레이터패턴


