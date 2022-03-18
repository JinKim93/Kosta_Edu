# 지역변수
- 메모리가 존재하는 시간

```c
#include <stdio.h>

void func1();
void func2();



void main(void)
{
	
	int val = 0;
	printf("첫 번째 메모리 할당 : val = 0\n");
	func1();
	printf("두  번째 메모리 소멸 : local = 10\n");
}
void func1()
{
	int local = 10;
	printf("두 번째 메모리 할당 : local = 10\n");
	func2();
	printf("세 번째 메모리 소멸 : local = 20\n");

}
void func2()
{
	int local = 20;
	printf("세 번째 메모리 할당 : local = 20\n");

}
```
- 매개 변수도 지역변수
- 함수의 매개 변수도 스택 메모리에 할당되는 지역변수


![메모리](https://user-images.githubusercontent.com/82345970/158953076-18c4a83a-e54c-4bff-ad67-b04d0ab4833a.PNG)

```c
#include <stdio.h>

int func(int a, int b) // 매개 변수(int a, int b)도 지역변수
{
	int result = 0;
	a = a + 1;
	b = b + 1;
	result = a + b;
	return result;

}
```

# 전역변수
- 전역 변수의 선언
  - main 바깥쪽에 선언
- 전역 변수가 메모리에 존재하는 시간
- 전역변수는 프포그램 시작하자 마자 메모리 상에 올라가서 프로그램이 종료 될때 메모리 상에서 소멸
![변수](https://user-images.githubusercontent.com/82345970/158953407-1adeed0a-72e0-458e-91c6-549d6b468773.PNG)

```c
#include <stdio.h>

int global; //전역변수 선언
void Add(int i, int j);
int main(void)
{
	int a;
	int b;
	printf("두 개의 정수를 입력하시오 : ");
	scanf_s("%d %d", &a, &b);
	Add(a, b);
	printf("두 정수의 합은 : %d 입니다.\n", global);
	return 0;
}
void Add(int i, int j)
{
	global = i + j;
}
```

### 메모리영역
- Stack(스택)
  - 지역변수
- Heap(힙)
  - 전역변수,static
- 데이터영역
