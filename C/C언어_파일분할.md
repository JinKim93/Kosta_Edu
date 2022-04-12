# C언어_파일분할

### 파일 분할의 필요성
- 지금까지의 코드
  - 코드 양도 작고, 기능도 간단
  - 하나의 파일에서 코드를 작성
  - 코드 양과 라인이 많아지면 하나의 파일에서 관리하기 힘들어짐
  - 파일을 나누어 관리하는 이유는 효율성을 극대화 시키기 위함
 
 - 어떻게 나눌것인가?
    - 작게는 기능 단위, 크게는 모듈 단위로 나눈다
    - 객체지향기반에서는 클래스 단위로 나눈다

### 파일 분할 예제
- **파일 분할 전**
 
![image](https://user-images.githubusercontent.com/82345970/160514139-da081784-85ae-4545-a013-50500311e0e1.png)

- **파일 분할 후(main함수, Add 함수로 분할)**
 
![image](https://user-images.githubusercontent.com/82345970/160514500-163181a2-7e4e-4630-bc2c-a72a76bd87c3.png)

![image](https://user-images.githubusercontent.com/82345970/160514649-1c33cdfd-83b6-472e-9f64-23b5b562294a.png)

# 헤더 파일

![image](https://user-images.githubusercontent.com/82345970/160515530-9fa1a9f8-941e-40ae-933a-b59b839771cf.png)

### 헤더파일 예제

![image](https://user-images.githubusercontent.com/82345970/160517528-82fc1b65-9e5e-437c-b10c-e3805c0545eb.png)

- **함수의 선언부 헤더파일로 빼놓는다**
 
![image](https://user-images.githubusercontent.com/82345970/160517619-eadcf31d-78e8-4bae-b465-10fa1aebe125.png)

# 조건부 컴파일
- 조건에 따라 컴파일을 할 것인지 말 것인지 결정하는것
- 소스코드 내에서 특정 영역을 지정하여 컴파일 유무를 결정
- 이기종 간의 두 개의 플랫폼 상에서 같은 소스를 동작시킬 경우

```c
#include <stdio.h>
#define DEBUG 1

int main(void)
{

	#if DEBUG
	printf("디버그 모드로 동작합니다\n");
	#else
	printf("릴리즈 모드로 동작합니다\n");
	#endif
	return 0;
}
```
- DEBUG가 1인 경우에는 디버그 모드로 동작하고, 0인 경우는 릴리즈 모드로 동작 함

### 내장 매크로

![image](https://user-images.githubusercontent.com/82345970/160522312-532d7417-47fe-4e5d-95b8-8b5e69fe702f.png)

-내장 매크로는 **코드 디버깅** 에 유용
```c
#include <stdio.h>


int main(void)
{
	
	printf("현재 날짜는 %s 입니다\n", __DATE__);
	printf("현재 시간은 %s 입니다\n", __TIME__);
	printf("소스 파일는 %s 입니다\n", __FILE__);
	printf("현재 라인 번호는 %d 입니다\n", __LINE__);
	return 0;
	
}
```
