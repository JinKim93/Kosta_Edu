# 정렬
- 임의의 자료 집합을 일정한 기준에 따라 나열하는 것
- 가장 간단한 정렬 알고리즘이 버블 정렬이다

# 정렬의 원리
- 레코드의 키들을 비교해보고 순서를 바꿀 필요가 있는 레코드를 정렬이 완료될 때까지 반복한다

# 버블정렬
- 레코드의 선두부터 인접 요소를 비교하여 큰 값을 뒤로 보내는 방식으로 정렬

![image](https://user-images.githubusercontent.com/82345970/160957901-810b3f98-8320-484a-a61e-d0fe3f03f192.png)

### 버블정렬
```c
#include <string.h>
#include <stdio.h>


void Swap(char* a, char* b)
{
	char t = 0;
	t = *a;
	*a = *b;
	*b = t;
}

void BubbleSort(char* ar, int num)
{
	int i, j;
	for (i = 0; i < num - 1; i++)
	{
		for (j = 1; j < num -i; j++)
		{
			if (ar[j - 1] > ar[j])
			{
				Swap(&ar[j - 1], &ar[j]);
			}
		}

	}


}

void main()
{
	char str[] = "winapi";

	printf("정렬 전의 문자열 : %s\n", str);
	BubbleSort(str, strlen(str));
	printf("정렬 된 문자열 : %s\n", str);

}
```
