# C언어 함수

### 함수의 정의
- 나누어서 처리하기 위한 목적
- 중복방지
- 코드 가독성

### 함수의 종류

- 사용자 정의 함수
  - 표준함수의 기능에는 한계
  - 사용자가 자신이 원하는 기능을 직접 만들 수 있는데, 바로 사용자 정의 함수
  - 정형화된 장난감과 레고와 같은 가변적인 장난감의 차이
  
- 표준함수
  - scanf_s, printf 등

### 함수의 구성

자료형 함수이름(인수목록)
{
    함수의 내용
}
- 자료형
  - 함수가 리턴하는 값의 자료형(void, int, double 등)
```c
#include <stdio.h>

int main()
{

	
	return 0; // 의미없는값을 리턴 할때는 0
	return 100; //의미가있는 값 리턴 할때 1,100, -1 등등 	

}
```
### 함수(call by value)
 값에 의한 복사
```c
#include <stdio.h>
//call by value -> 값에 의한 복사
int Add(int a, int b)
{
	int c = 0;
	c = a + b;
	return c;

}

void main()
{
	int i, j, hap;
	printf("두 개의 정수를 입력하세요\n");
	scanf_s("%d %d", &i, &j);
	hap = Add(i, j);
	printf("두 정수의 합은 %d\n", hap);

	return;
}
```

### C언어 함수 형태
```c
#include <stdio.h>

int Add(int a, int b); //함수의 원형

void main() 
{
	int i, j, hap;
	printf("두 개의 정수를 입력하세요\n");
	scanf_s("%d %d", &i, &j);
	hap = Add(i, j);  // 함수의 호출
	printf("두 정수의 합은 %d\n", hap);

	return;
}

int Add(int a, int b) //함수의 정의
{
	int c = 0;
	c = a + b;
	return c;

}
```


### C언어 함수 연습문제
```c
#include <stdio.h>


int Add(int i, int j);

void print_Start()
{
	printf("=======Programming Start ========\n");
	printf("두 개의 정수를 입력하시오 : ");
}

void print_Hap(int result)
{
	printf("두 수의 합은 %d 입니다\n", result);
	printf("Programming End\n");
}

int main(void)
{
	int a;
	int b;
	int hap;
	print_Start();
	scanf_s("%d %d", &a, &b);
	hap = Add(a, b);
	print_Hap(hap);
	return 0;

}

int Add(int i, int j)
{

	return i + j;
}
```

```c
#include <stdio.h>

int mut(int a);

void main()
{
	int num;
	int result;
	printf("한개 정수를 입력하세요\n");
	scanf_s("%d", &num);
	result = mut(num);
	printf("결과는 %d 입니다\n",result);
}

int mut(int a)
{

	return a * 2;
}
```

### 원의 넓이를 구하시오(함수사용)

```c
#include <stdio.h>

void Circle(int radian);

int main()
{
	int r;
	
	printf("반지름을 입력하시오:");
	scanf_s("%d", &r);
	Circle(r);
	return 0;
}

void Circle(int radian)
{

	printf("원의 넓이는 %.2f\n", radian * radian * 3.14);

}
```

### 사각형의 넓이를 구하시오(함수사용)

```c
#include <stdio.h>

void Rect(int width, int height);

int main()
{
	int w, h;
	
	printf("두 정수를 입력하시오:");
	scanf_s("%d %d", &w, &h);
	Rect(w, h);
	return 0;
}

void Rect(int width, int height)
{

	printf("사각형의 넓이는 %d\n", width * height);

}
```

### 두 정수를 입력해서, 합, 차, 곱, 나누기 함수를 만드시오
```c
#include <stdio.h>

int Plus(int n1, int n2);
int Minus(int n1, int n2);
int Mutiple(int n1, int n2);
int Divide(int n1, int n2);

int main()
{
	int num, num2;
	int result;
	printf("두 정수를 입력하시오\n");
	scanf_s("%d %d", &num, &num2);
	result = Plus(num, num2);
	printf("두정수의 합은 %d 입니다.\n", result);
	result = Minus(num, num2);
	printf("두정수의 차는 %d 입니다.\n", result);
	result = Mutiple(num, num2);
	printf("두정수의 곱은 %d 입니다.\n", result);
	result = Divide(num, num2);
	printf("두정수의 나누기는 %d 입니다.\n", result);
		

	return 0;
}

int Plus(int n1, int n2)
{

	return n1 + n2;

}

int Minus(int n1, int n2)
{

	return n1 - n2;

}

int Mutiple(int n1, int n2)
{

	return n1 * n2;

}


int Divide(int n1, int n2)
{

	return n1 / n2;
}
```

### 두 수를 입력 받아, 두수를 비교하여 최대값,최소값을 구하는 함수를 정의하시오

```c
#include <stdio.h>
// 두 수를 입력받아 최대값, 최소값을 구하는 함수를 정의 하시오
void MinMax(int a,int b);

int main(void)

{
	int num1, num2;
	printf("두 정수를 입력하시오\n");
	scanf_s("%d %d", &num1, &num2);
	MinMax(num1,num2);
	return 0;
}

void MinMax(int a, int b)
{
	if (a > b)
	{
		printf("최대값은 %d, 최소값은 %d입니다\n", a,b);
	}
	else
	{
		printf("최대값은 %d, 최소값은 %d입니다\n", b, a);
	}
}
```




