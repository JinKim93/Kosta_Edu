# C언어 배열

### 배열

```c
#include <stdio.h>
//각 배열 요소의 합을 구하라
int main()
{
	int arr[3]; //12byte
	int sum = 0;
	
	for (int i = 0; i < sizeof(arr)/sizeof(int); i++) // for(int i =0; i < 3; i++
	{
		arr[i] = 10*(i+1);
		printf("%d\n", arr[i]);
		sum += arr[i];
		
	}
	printf("각 배열 요소의 합은 : %d \n", sum);
	printf("각 배열 요소의 평균은 : %d\n", sum / 3);


	return 0;
}
```
- sizeof 연산자를 이용해서 for문 조건식 능률적으로 변경함

