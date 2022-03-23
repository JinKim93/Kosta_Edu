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



