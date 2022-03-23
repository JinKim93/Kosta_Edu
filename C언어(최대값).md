# C언어_최대값_연습문제
- 길이가 5인 정수형 배열 {3,5,2,11,10} 요소 중에서 가장 큰 값을 구하시오

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
