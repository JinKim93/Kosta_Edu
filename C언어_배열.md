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

### 배열의 복사
- 배열은 배열끼리 복사 가능

```c
#include <stdio.h>

int main()
{

	int arr1[5] = { 1,2,3,4,5 };
	int arr2[5];
	int i = 0;
	for (i=0;i<sizeof(arr1)/sizeof(int); i++)
	{
		arr2[i] = arr1[i];
		printf("%d\n", arr2[i]);
	}


	

	return 0;
}
```
### 배열(문자열 변수)
- 배열을 통해 문자도 control 할 수 있는 문자열 변수 선언
```c
#include <stdio.h>

int main(void)
{

	
	char str[12] = "Hello World"; //문자열 변수
	printf("%s\n", str);
	
	return 0;
}

```
### 배열(문자열_null문자)
- 문자열의 끝에는 null 문자가 추가된다.

### null 문자의 필요성
```c
char str[100] = "ABC";
```
- 100바이트 할당됨,\0(null문자) 
- 컴퓨터는 문자열 데이터를 읽을때 \0까지만 읽고, \0이후 무시 약속
- 항상 문자열 할당할때 \0 공간도 확보 해야함

### 배열 연습문제
- 입력한 값을 배열요소로 출력하시오
- -1입력시 현재까지 입력한 배열요소를 출력하시오.
```c
#include <stdio.h>

int main(void)
{

	int arr[100];
	int i = 0;
	int cnt = 0;
	for (i = 0; i < 100; i++)
	{
		printf("출력할 배열요소 값을 입력하시오\n");
		scanf_s("%d", &arr[i]);
		if (arr[i] == -1)
		{
			cnt = i;
			break;
		}

		
	}
	for(int j = 0; j < cnt; j++)
	{
		printf("현재까지 입력한 배열 요소 : %d\n", arr[j]);
	}
	

	return 0;
}
```
### 배열 연습문제 
- 두 변수의 값을 서로 바꾸시오.
```c
#include <stdio.h>

int main(void)
{
	int a = 2;
	int b = 3;
	int temp = 0;

	temp = a;
	a = b;
	b = temp;

	printf("a:%d\nb:%d\n", a, b);

	

	return 0;
}

```
### 함수사용해서작성
```c
#include <stdio.h>

void Swap(int a, int b)
{
	int temp = a;
	a = b;
	b = temp;
	printf("a:%d\nb:%d", a, b);
}

int main(void)
{
	int a = 2;
	int b = 3;
	
	Swap(a, b);
		

	return 0;
}
```
