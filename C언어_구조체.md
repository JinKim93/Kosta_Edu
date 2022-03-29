# 구조체
- 하나 이상의 서로 다른 종류의 변수들을 묶어서 새로운 자료형을 정의하는것
- 구조체도 자료형이다.

```c
#include <stdio.h>
#include <string.h>

struct student {
	char name[10];
	int age;
	int height;
}st1;

int main(void)
{

	strcpy_s(st1.name, "JinKim");
	st1.age = 25;
	st1.height = 178;
	printf("이름 = %s, 나이 = %d, 키 = %d\n", st1.name, st1.age, st1.height);
	return 0;
}
```
