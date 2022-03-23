# C언어_최대값_연습문제
### 길이가 5인 정수형 배열 {3,5,2,11,10} 요소 중에서 가장 큰 값을 구하시오

```c
#include <stdio.h>

int main(void)
{
	int a[] = { 3,5,2,11,10};
	int i = 0;
	int imax = a[0];

	for (i = 0; i< 5; i++)
	{
		if (imax < a[i])
		{
			imax = a[i];
		}
				
	}
	printf("최대값은%d\n", imax);


	return 0;
} 

```
### 5개의 값을 입력 받은 후, 입력 받은 수 중에서 가장 큰수를 출력하시오
```c
#include <stdio.h>

int main(void)
{

	int a[5] = {0,}; //5개 배열을 0으로 전부다 초기화
	int i = 0;
	int imax = 0;
	printf("정수를 입력하시오\n");
	
	for (i = 0; i< 5; i++)
	{
		scanf_s("%d", &a[i]);
		if (imax < a[i])
		{
			imax = a[i];
		}
				
	}
	printf("최대값은%d\n", imax);


	return 0;
} 
```
