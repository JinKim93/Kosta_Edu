# POJO(Plain Old Java Object)
### 순수한 자바 오브젝트 : 외부에 종속성이 없고, 순수하게 자바로 이루어진 클래스<br></br>

# POJO특징
### 1. 특정규약에 종속되지 않는다
#### 특정 Library, Module에서 정의된 클래스를 상속 받아서 구현하지 않아도 된다
#### POJO가 되기 위해서는 외부의 의존성을 두지 않고, 순수한 JAVA로 구성이 가능해야 한다
### 2. 특정환경에 종속되지 않는다
#### 비즈니스 로직을 처리하는 부분에 외부 종속적인 http request, session 등 POJO를 위배 한것으로 간주한다
#### @Annotation 기반으로 설정하는 부분도 엄연히는 POJO라고 볼수는 없다<br></br>

# POJO Framework
### 1. Spring, Hibernate
