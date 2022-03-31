# C언어 재귀함수
### factorial 문제

```c

#include <stdio.h>
#include <string.h>

int factorial(int n);


void main()
{
	int num = 0;
	int result = 0;

	printf("정수를 입력하세요 : ");
	scanf_s("%d", &num);

	result = factorial(num);
	printf("%d의 결과는 : %d 입니다\n",num,result);
}

int factorial(int n);
{
	if (n == 1)
	{
		return 1;
	}
	return (n * factorial(n - 1));
}
```

### 카운트 다운 문제
```c

#include <stdio.h>
#include <string.h>
#include <Windows.h>

int countdown(int n);


void main()
{
	int num = 0;
	int result = 0;

	printf("정수를 입력하세요 : ");
	scanf_s("%d", &num);

	
	printf("카운트 다운 시작\n");
	countdown(num);
}

int countdown(int n)
{
	if (n < 1)
	{
		printf("발사\n");
		return 0;
	}
	else
	{
		printf("%d\n", n);
		Sleep(1000);
		countdown(n - 1);

	}
		
	
	
}
```
