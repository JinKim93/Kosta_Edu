# C언어_알고리즘

### 검색
- 순차 검색
  - 모든 알고리즘 중 가장 기본적이면서 상식적인 검색 방법
  - 테이블의 처음부터 끝까지 순서대로 읽으면서 키 비교
  - 알고리즘 간단 -> 검색효율 좋지않음
```c
#include <stdio.h>

int LinearSearch(int* ar, unsigned num, int key)
{
	unsigned i;

	for (i=0; i <num; i++)
	{
		if (ar[i] == key)
		{
			return i;
		}

	}
	return -1;
}

void main()
{
	int ar[] = { 23,47,19,63,57,26,75,73,82,89,47,11 };
	unsigned num;
	int key;
	int idx;

	printf("찾을 값을 입력하세요\n");
	scanf_s("%d", &key);
	num = sizeof(ar) / sizeof(ar[0]); //배열 나오면 사이즈는 왠만하면 계산 해놓자
	idx = LinearSearch(ar, num, key);

	if (idx == -1)
	{
		puts("찾는 값이 없습니다.");
	}
	else
	{
		printf("찾는 값은 %d번째에 있습니다.\n", idx+1);
	}
}
```

### 이분 검색
  - 중간값과 키값의 대소를 구분하여 테이블을 절반씩 나눠가며 비교하는 방식
  - 한 번 비교할 때 마다 테이블의 길이가 절반씩 줄어들기 떄문에 검색 효율은 상당히 좋다
  - 테이블이 커도 속도가 느려지지 않는다
  - 일반적으로 영한사전을 검색할 때 이분 검색을 사용한다
  - 이분 검색이 가능하려면 테이블의 모든 자료가 오름차순으로 정렬 되어 있어야 한다
```c
#include <stdio.h>

int BinarySearch(int* ar, unsigned num, int key)
{
	unsigned Upper, Lower, Mid;
	Lower = 0;
	Upper = num - 1;

	for (;;)
	{
		Mid = (Upper + Lower) / 2;
		if (ar[Mid] == key)
		{
			return Mid;
		}
		if (ar[Mid] > key)
		{
			Upper = Mid - 1;
		}
		else
		{
			Lower = Mid + 1;
		}
		if (Upper < Lower)
		{
			return -1;
		}
	}
}

void main()
{

	int ar[] = {2,6,13,19,21,21,23,29,35,48,62,89,90,95,99,102,109,208,629};
	unsigned num;
	int key;
	int idx;

	printf("찾을 값을 입력하세요\n");
	scanf_s("%d", &key);
	num = sizeof(ar) / sizeof(ar[0]); //배열 나오면 사이즈는 왠만하면 계산 해놓자
	idx = BinarySearch(ar, num, key);

	if (idx == -1)
	{
		puts("찾는 값이 없습니다.");
	}
	else
	{
		printf("찾는 값은 %d번째에 있습니다.\n", idx + 1); //출력할때 인덱스라서 +1 해줌
	}
}
```

### unsigned
- 양수의 인수만 사용하고 싶을때 쓰인다.
```c
unsigned char b
```
### 해시
![image](https://user-images.githubusercontent.com/82345970/160525766-970896b6-716b-4960-be02-c03696b0939f.png)

### 해시 테이블
- 2차원배열

![image](https://user-images.githubusercontent.com/82345970/160526328-6883470d-1993-4764-9764-02c27c65b30a.png)

### 해시 함수

![image](https://user-images.githubusercontent.com/82345970/160526665-226839ab-6634-4391-8da0-a6c5552b8c89.png)
