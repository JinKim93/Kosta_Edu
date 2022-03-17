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

