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

### 문자열 표현 방식
```c
#include <stdio.h>

int main(void)
{

	char str[] = "love";
	const char *pstr = "you"; //상수화 권장(const)

	str[0] = 'r';

	printf("str의 출력 : %s\n,str");
	printf("pStr의 출력 : %s\n,pstr");



	return 0;
}

```

### 포인터 배열 (포인터의 특성을 가지고 있는 배열)
- 배열의 목적은 여러 개의 변수를 사용 하기 위함
- 포인터 배열은 포인터 변수를 여러 개 사용하기 위함

```c
#include <stdio.h>

int main(void)
{
	const char* pArr[] = { "C언어","자바","베이직" };
	int i;

	for (i = 0 ; i < 3; i++)
	{
		printf("%s\n", pArr[i]);
	}


	return 0;
}
```

### 2차원 배열
```c
int arr[2][3]; //행,열
```
- arr[0][0] arr[0][1] arr[0][2]
- arr[1][0] arr[1][1] arr[1][2]

```c
#include <stdio.h>

int main(void)
{

	int i, j;
	int arr[2][3];
	arr[0][0] = 1;
	arr[0][1] = 2;
	arr[0][2] = 3;
	arr[1][0] = 4;
	arr[1][1] = 5;
	arr[1][2] = 6;

	printf("2차원 배열 값의 출력 결과\n");

	for (i = 0 ; i < 2; i++)
	{
		
		for (j = 0; j < 3; j++)
		{
			printf("%d ", arr[i][j]);
		}
		printf("\n");
	}

	return 0;
}
```

## 함수와 포인터
- 배열형의 인자는 포인터형으로 받는다

```c
#include <stdio.h>

//배열형의 인자는 포인터형으로 받는다

void func(int* pArr);
int main(void)
{
	int arr[] = { 1,2,3,4,5 };
	int i;

	func(arr);
	for (i = 0; i < 5; i++)
	{
		printf("배열의 요소 출력 : %d\n", arr[i]);

	}
	

	return 0;
}

void func(int* pArr)
{
	int i;
	for (i = 0; i < 5; i++)
	{
		printf("함수 안에서 배열의 요소* 출력 : %d\n", *(pArr + i));
	}
}
```
```c
#include <stdio.h>

// func의 기능 - >  배열의 모든 요소의 합을 리턴
int func(int* pArr,int size);
int main(void)
{
	int arr[] = { 1,2,3,4,5 };
	int sumArr, sizeArr;

	sizeArr = sizeof(arr) / sizeof(int);
	sumArr = func(arr, sizeArr);
	printf("배열의 총 합은 : %d\n", sumArr);
	

	return 0;
}

int func(int* pArr,int size)
{
	int i, sum = 0;
	for (i = 0; i < size; i++)
	{
		sum += *(pArr + i);
	}
	return sum;
}
```
	
### 값 호출 방식(Call by Value)
- 값 호출 방식이란  실인수으 ㅣ값이 형식 인수로 전달되는 방식
- 실인수의 메모리와 형식인수의 메모리가 별도로 관리
- 실인수의 값이 형식인수로 복사되는 형태


```c
#include <stdio.h>

void callValue(int b);

int main(void)
{
	
	int a = 1;
	callValue(a);
	printf("실인수 a의 출력 : %d\n", a);

	return 0;
}

void callValue(int b)
{

	b = b + 3;
	printf("형식인수 b의 출력 : %d\n", b);
}

```

```c
#include <stdio.h>

void Swap(int a, int b);

int main(void)
{
	int x = 10, y = 20;
	printf("초기값 x = %d, y = %d\n", x, y);
	Swap(x, y);
	printf("함수 밖에서 변경 후 x = %d, y = %d\n", x, y);
	return 0;

}

void Swap(int a, int b)
{
	int temp;
	temp = a;
	a = b;
	b = temp;
	printf("함수 안에서 변경 후 a = %d , b = %d\n",a,b);

}
```
![image](https://user-images.githubusercontent.com/82345970/159834774-638cab63-bf3c-4322-bf97-3aa6d4d86616.png)
- 메모리를 공유 하지 않으므로 변경이 안된다
- 값 만 복사한것이다

### Call by reference(참조 호출 방식)
- 함수 호출 시 전달인자로 메모리 접근에 사용되는 주소값을 전달

```c
#include <stdio.h>


void callReference(int* b);

int main(void)
{
	int a = 1;
	callReference(&a);
	printf("실인수 a의 출력 : %d\n", a);
	
	return 0;

}
void callReference(int* b) //선언 -> 주소값 전달하는 변수
{ 
	*b = *b + 3; // b가 가리키고있는 실제값
	printf("형식인수 *b의 출력 : %d\n", *b); //b가 가리키고있는 실제값
}
```

```c
#include <stdio.h>

void Swap(int *a, int *b);

int main(void)
{
	int x = 10, y = 20;
	printf("초기값 x = %d, y = %d\n", x, y);
	Swap(&x, &y);
	printf("함수 밖에서 변경 후 x = %d, y = %d\n", x, y);
	return 0;

}

void Swap(int *a, int *b)
{
	int temp;
	temp = *a; //*a가 가르키고 있는 실제 데이터 int x = 10
	*a = *b;
	*b = temp;
	printf("함수 안에서 변경 후 a = %d , b = %d\n", a, b);

}
```
![image](https://user-images.githubusercontent.com/82345970/159843057-a28c3baf-d614-467b-8520-d6890542732c.png)


### 사용자로 부터 두 수를 입력 받아 두 수의 합과 곱을 구하시오(call-by-reference)
```c
#include <stdio.h>

void Sum_Mutiple(int a, int b, int* pSum, int* pMul);

int main(void)
{
	int x;
	int y;
	int hap = 0; 
	int gob = 0;
	printf("두 수를 입력하시오\n");
	scanf_s("%d %d", &x, &y);
	Sum_Mutiple(x, y,&hap,&gob);
	printf("합 : %d\n곱 : %d\n", hap, gob);

	return 0;

}

void Sum_Mutiple(int a, int b,int *pSum,int *pMul)
{

	*pSum = a + b;
	*pMul = a * b;
	
}

```

### 팩토리얼 문제
- ex) 3! = 3 * 2 * 1
```c
#include <stdio.h>

void Factorial(int a,int* pRet);

void main()
{
	
	int i = 5;
	int result = 1;
	printf("정수를 입력하세요\n");
	scanf_s("%d", &i);
	Factorial(i, &result);
	printf("%d! = %d\n",i,result);


}

void Factorial(int a, int* pRet)
{
	for (int i = 1; i < a +1; i++)
	{
		*pRet = *pRet * i;
	}
	
	
}
```

### 함수 포인터의 선언
- 자료형(*함수 포인터 이름)(인자목록)
- int (*func)(int a);
- 함수 포인터도 포인터이므로 주소값을 저장한다.

```c
#include <stdio.h>

int Add(int a, int b);
int Min(int a, int b);

int main(void)
{
	int a, b, sel, result;
	int (*fPtr)(int a, int b) = 0;

	while (1)
	{
		printf("다음 중 선택하시오 (1.덧셈 2.뺄셈 3.종료) : ");
		scanf_s("%d", &sel);

		switch (sel)
		{
		case 1:
			fPtr = Add;
			break;
		case 2:
			fPtr = Min;
			break;
		case 3 :
			return 0;
		default:
			break;

		}
		printf("두 정수를 입력하시오 : ");
		scanf_s("%d %d", &a, &b);
		result = fPtr(a,b);
		printf("결과 : %d\n", result);
	}
	return 0;
}
int Add(int a, int b)
{
	return a + b;

}

int Min(int a, int b)
{
	return a - b;
}
```

### 함수 포인터 사용 이유
- 직접 함수 호출하면 되지 왜 복잡하게 함수 포인터를 사용하나 ?
- 컴파일 타임 또는 런타임에 메모리 크기 및 위치가 결정된다
- 컴파일 타임 -> 정적 바인딩, 런타임 -> 동적 바인딩
- 함수 포인터의 사용은 프로그램의 확정성과 유용성을 위함이다.
- VScode 사용시, 파이썬을 플러그인으로 설치를 한 이후, VScode(편집기)는 그대로 있고, 파이썬 처럼 플러그인으로 설치 할수 있는건 확장이 된다(동적 바인딩)

### NULL 포인터
- NULL 포인터란 아무것도 가리키지 않는 포인터
- 아무것도 가리키지 않는다는 의미는 포인터 변수에 아무런 주소값도 저장되어 있지 않다는 의미이다.
- 실전에서는 함수의 동작 에러 체크 용도로 사용한다
```c
char *p = Func();
if(p == NULL)
{
	//에러 처리
}
else
{
	//수행처리
}
```
### 포인터를 리턴하는 함수를 NULL 체크 해주는 문제
```c
#include <stdio.h>
#include <string.h>

int main(void)
{

	char str[] = "Love";
	char* p;

	p = strchr(str, 'v');

	if (p != NULL)
	{
		*p = 'b';
		printf("변경 결과 : %s\n", str);
	}
	else
	{
		printf("NULL을 리턴하였습니다.\n");
	}
	return 0;
}
```
