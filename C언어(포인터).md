# C언어_포인터

### 포인터(변수)
- 어느 특정 주소를 가리키거나 향하게 하고 있다
- 주소값을 가리킨다는 의미는 주소값을 가지고 있다라는 의미이다
- 메모리의 주소값을 가리키는 변수
- 포인터변수는 무조건 4byte이다
```c
#include <stdio.h>

int main(void)
{
	int b = 100;
	int *pB = &b;

	printf("b = %d\n", b);
	printf("&b = %x\n", &b);
	printf("*pB = %d\n", *pB); //*pB는 pB가 가리키는 메모리의 실제값을 나타냄
	printf("pB = %x\n", pB);

	return 0;
}
```

## 배열과포인터
- 배열의이름은 포인터상수
- 배열의이름 == 포인터
- 포인터를
```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
	
	int arr[] = { 1,2,3,4,5 };
	int i;

	printf("배열의 요소 출력 : "); //배열에 직접 접근
	for (i = 0; i < 5; i++)
	{
		printf("%d ", arr[i]);
	}
	printf("\n");

	printf("배열 이름을 이용한 배열 요소 출력 : "); // 배열을 포인터처럼 사용
	for (i = 0; i < 5; i++)
	{
		printf("배열의 값은 %d \n", *(arr + i));
		printf("배열의 주소값은 %d\n", arr + i);
	}
	printf("\n\n");
		
	return 0;
} 
} 
```

### 포인터를 배열의 이름처럼 사용

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
	
	int arr[] = { 1,2,3,4,5 };
	int* pTemp;
	int i;

	pTemp = arr; //배열의이름은포인터 
	printf("배열의 요소 출력 : ");   
	for(i = 0; i < 5; i++)
	{
		printf("%d ", pTemp[i]);
	}
	printf("\n");

		
	return 0;
} 
```
