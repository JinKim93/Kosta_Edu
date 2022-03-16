# C언어 세개의 정수 입력 후 최소값을 출력
```c
#include <stdio.h>

int main(void)
{
	int num1 = 0;
	int num2 = 0;
	int num3 = 0;
	int min = 0;
	
	printf("세개의 정수를 입력하시오\n");
	scanf_s("%d %d %d", &num1, &num2, &num3);

	if(num1 < num2)
	{
		if (num1 < num3)
		{
			min = num1;
		}
		else
		{
			min = num3;
		}
	}
	else
	{
		if (num2 < num3)
		{
			min = num2;
		}
		else
		{
			min = num3;
		}
	}
	printf("최소값은 %d입니다\n", min);
}

```
