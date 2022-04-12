# continue문

## continue문 사용 하는 경우
- 특정 조건에서 수행문을 생략하는 경우 사용

## continue문 연습문제
```c
#include <stdio.h>

int main()
{
	int a = 0;
	
	while (a<100)
	{
		
		a++;
		if (a > 80 && a< 90)
		{
			continue;
		}
		printf("a의 값은 %d이다.\n",a);
	}
	
	return 0;

}
```
## 코드 결과
![캡쳐](https://user-images.githubusercontent.com/82345970/158748121-48ec6d43-09a5-4a73-a0a6-836f1e597e6b.PNG)

- 81 ~ 89 예외 되어 있음

## 구구단을 출력하시오.<br>(짝수단 만 출력)

```c
#include <stdio.h>

int main()
{
	int a;
	int b;
	
	for (a = 2; a < 10; a++)
	{
		if ((a % 2) != 0)
		{
			continue;
		}

		for (b = 1; b < 10; b++)
		{
			
			printf("%d * %d = %d\n", a, b, a * b);
		
		}
		printf("\n");
	}

	return 0;

}
```
