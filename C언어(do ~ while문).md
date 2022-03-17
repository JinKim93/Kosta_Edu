# do ~ while문 쓰는 이유

- 조건에 해당하는 변수가 누군가로 부터 입력을 받아야 판별 해야 하는 경우

# do ~ while문 연습문제
- 사용자로부터 정수 입력

  0을 입력하면 반복문빠짐

  총합을 출력
 
```c
#include <stdio.h>

int main()
{
	int sum = 0;
	int input = 0;

	do
	{
		printf("정수를 입력하세요 : ");
		scanf_s("%d", &input);
		sum = sum + input;
		
		
	} while (input != 0);
	printf("총 합은 %d 입니다\n", sum);

	return 0;

}
```
# do ~ while문 사용 하지 않고 while문으로만 작성

```c
#include <stdio.h>

int main()
{
	int sum = 0;
	int input = 0;
	printf("정수를 입력하세요 : ");
	scanf_s("%d", &input);
	sum = sum + input;
	
	while (input !=0)
	{
		printf("정수를 입력하세요 : ");
		scanf_s("%d", &input);
		sum = sum + input;

	}
	printf("총 합은 %d 입니다\n", sum);

	return 0;

}
```

# 사용자로부터 하나의 정수를 입력 받아 1부터 입력받은 정수까지 <br>합 계산 (do ~ while문 사용)

```c
#include <stdio.h>

int main()
{
	int input = 0;
	int sum = 0;
	int i = 0;
	printf("정수를 입력하시오 : ");
	scanf_s("%d", &input);

	do
	{		
		i++;
		sum += i; //sum = sum + i;
		
	}while(i<input);
	printf("누적된 합은 %d입니다\n", sum);
	return 0;

}
```



