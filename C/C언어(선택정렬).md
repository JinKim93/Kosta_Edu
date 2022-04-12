# 선택정렬
- 선택정렬은 최소값을 찾아 앞쪽으로 이동하기를 배열 크기만큼 반복하는 정렬 방법
- 배열에서 가장 작은 값을 찾아 처음으로 일단 보낸다
- 첫 번째 요소는 제외하고 남은 요소들 중에 제일 작은 값을 찾아 선두로 보내기를 배열 끝까지 반복
- 작은 순서대로 계속 앞쪽으로 이동하므로 반복이 끝나면 모든 요소를 순서대로 정렬

```c
#include <iostream>
#include <stdio.h>
#include <string.h>
void swap(char* a, char* b)
{
	char t = 0;
	t = *a;
	*a = *b;
	*b = t;
}

void SelectionSort(char* ar, int num)
{
	int minidx;
	int i, j;
	for (i = 0; i < num -1; i++)
	{
		for (minidx = i, j = i +1; j < num; j++)
		{
			if (ar[minidx] > ar[j])
			{
				minidx = j;
			}
		}
		if (minidx != i)
		{
			swap(&ar[minidx], &ar[i]);
		}

	}
		
}

void main()
{
	char str[] = "winapi";
	printf("정렬 전의 문자열 : %s\n", str);
	SelectionSort(str, strlen(str));
	printf("정렬된 문자열 : %s\n", str);
}
```
