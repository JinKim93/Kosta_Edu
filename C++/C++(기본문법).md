# C++(기본문법)
```c
#include <iostream> 


void main()
{
	std::cout << "Hello C++" << std::endl; // ::스코프연산자(영역결정연산자) -> 영역결정할떄 쓰인다
}
```
![image](https://user-images.githubusercontent.com/82345970/160737146-d10c7569-9921-4d3c-8724-6620cd9b53b8.png)

### 기본 자료형 출력
```c
#include <iostream> // 


void main()
{

	int a = 10;
	float b = 3.14f;
	char c = 'A';

	std::cout << a << std::endl;
	std::cout << b << std::endl;
	std::cout << c << std::endl;

}
```

### 출력 객체 cout
- namespace에 대하여
  - 특정 공간에 이름을 지정해 준다는 의미
  - 이름 공간 사용 유무에 따른 문제점과 해결점

### namespace을 사용하지 않은 경우 문제 코드(컴파일 안됨, 오류코드)
```c
#include <iostream> 

void func(void)
{
	std::cout << "A학급 주성" << std::endl;
}
void func(void)
{
	std::cout << "B학급 주성" << std::endl;
}


void main()
{

	
	func();


}
```
### namespace을 사용한 코드(정상)
```c
#include <iostream> 

namespace A
{
	void func(void)
	{
		std::cout << "A학급 주성" << std::endl;
	}
}

namespace B
{
	void func(void)
	{
		std::cout << "B학급 주성" << std::endl; //std라는 namespace안에 cout있다. endl = 개행
	}
}


void main()
{

	
	A::func(); //A라는 영역에 해당하는 func을 불러라(::스코프연산자 사용)


}

```

### std::cout 반복해서 안쓰는 방법
- using namespace std; 
```c
#include <iostream> 
using namespace std; //std라는 namespace존재해있고, 사용하겠다

void main()
{

	
	int a = 10;
	float b = 3.14f;
	char c = 'A';
	
	cout << a << endl;
	cout << b << endl;
	cout << c << endl;


}
```
### 값 입력 받게 해주는 cin객체

```c
#include <iostream> 
using namespace std; //std라는 namespace존재해있고, 사용하겠다




void main()
{

	int a;
	float b;
	char c;

	cin >> a;
	cout << "정수값 출력 :" << a << endl;
	cin >> b;
	cout << "실수값 출력 :" << b << endl;
	cin >> c;
	cout << "문자값 출력 :" << c << endl;

}
```

### C++ 언어에서 새로운 규칙
![image](https://user-images.githubusercontent.com/82345970/160743607-4568cb18-ac19-4629-a585-4709ae219709.png)

```c
#include <iostream> 
using namespace std;
void func(int a = 10, int b = 20);

void main()
{

	func(); // 전달인자 없음, 기본값 사용
	func(100); //첫번째 전달인자, 두번째 기본값 사용
	func(100, 200); //첫번째, 두번째 모두 전달 인자 사용

}

void func(int a, int b)
{
	cout << "두 전달인자 출력 : " << a << "  " << b << endl;
}
```

### C++ 언어에서 새로운 규칙(C언어에서는 지역변수가 전역변수보다 우선순위가 높다)
- C언어에서 작성한거랑, C++에서 작성한 코드 비교하기
```c
#include <stdio.h>

int nTemp = 10;
void main()
{
	{
		int nTemp = 20;
		printf("nTemp의값은 %d\n", nTemp);
	}
	printf("nTemp의값은 %d\n", nTemp);
}
```

```c
#include <iostream> 

using namespace std;


int nTemp = 10;
void main()
{
	{
		int nTemp = 20;
		cout << "nTemp = " << nTemp << endl; 
		cout << "::nTemp = " << ::nTemp << endl; // ::namespace가 있으면 전체를 나타냄 -> 전역변수 int nTemp = 10; 출력함
	}
	cout << "nTemp = " << nTemp << endl;
}

```
### C++에서 작성한 코드 결과 값
![image](https://user-images.githubusercontent.com/82345970/160754825-92a873d3-8c5f-458a-80ef-b97196ef89ba.png)


# 클래스
- 사용자가 정의한 추상적인 데이터형
 
### 클래스의 구성
![image](https://user-images.githubusercontent.com/82345970/160761582-3a766c9b-737a-404e-a2a5-daa05d4a7c60.png)

### 클래스의 정의
```c
#include <iostream> 
#include <stdio.h>
using namespace std;

class MousePoint
{
	private: //외부에서 다른 객체가 접근 못하게 함(접근지정자)
	int x;
	int y;

public: //외부에서 접근할수있게(접근지정자)
	void SetXY(int nX, int nY)
	{
		x = nX;
		y = nY;
	}

};


void main()
{
	

}
```
### C++에서 정석으로 사용하는 함수 구조
```c
#include <iostream> 
#include <stdio.h>
using namespace std;

class MousePoint
{
	private: //외부에서 다른 객체가 접근 못하게 함(접근지정자)
	int x;
	int y;

public: //외부에서 접근할수있게(접근지정자)

	void SetXY(int nX, int nY);
};

void MousePoint::SetXY(int nX, int nY)
{
	x = nX;
	y = nY;
}
void main()
{
	

}
```

### 접근지정자
![image](https://user-images.githubusercontent.com/82345970/160763917-445c1221-2aee-42fa-bb6e-2cbaa449ce19.png)

### 멤버접근(멤버변수 및 멤버함수)
```c
#include <iostream> 

using namespace std;

class MousePoint
{
	private: 
	int x;
	int y;

public: 

	void SetXY(int nX, int nY);
};

void MousePoint::SetXY(int nX, int nY) 
{
	x = nX;
	y = nY;
	cout << "x = " << x << endl;
	cout << "x = " << y << endl;
}
void main()
{
	MousePoint point;
	point.SetXY(10, 20);


}
```


