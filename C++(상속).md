# 상속

### 회사 인사시스템 예시

```c
#include <iostream>

using namespace std;

class Employee
{
public:
	Employee();
	~Employee();
	Employee(const char* pName, const char* pAddr);
	void Display();
private:
	char* strName;
	char* strAddr;
};

Employee::Employee()
{
	strName = NULL;
	strAddr = NULL;
	cout << "디폴트 생성자" << endl;
}

Employee::Employee(const char* pName, const char* pAddr)
{
	strName = new char[strlen(pName) + 1];//넘겨받은 메모리를 strName에 동적메모리로 할당 널값도 포함
	strAddr = new char[strlen(pAddr) + 1];
	strcpy_s(strName, strlen(pName) + 1, pName);//문자열 카피//안정적으로 사용하라고 중간에 길이까지 넣었다
	strcpy_s(strAddr, strlen(pAddr) + 1, pAddr);
	//상수화 된 포인터를 새로운 변수에 메모리를 넘겨받고 문자열을 카피하여 출력
	cout << "전달인자가 2개인 생성자" << endl;
}

Employee::~Employee()
{
	delete[] strName;
	delete[] strAddr;

	cout << "소멸자" << endl;
}

void Employee::Display()
{
	cout << "이름 : " << strName << endl;
	cout << "주소 : " << strAddr << endl;
}

void main()
{
	Employee kim("핸드폰", "권선구");
	kim.Display();
}
```

