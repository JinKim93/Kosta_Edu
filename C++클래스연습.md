```c
#include <iostream>
using namespace std;

class Phone
{
private:
	int num;
	int shape;
	const char* sms;
public:
	Phone() {}
	Phone(const char* msg)
	{
		sms = msg;
	}
	~Phone() {}
	const char* Receive() const { return sms; }
	void Call() {}
	void Send(const char* msg)
	{
		sms = msg;
	}
};

void main()
{
	
	Phone ph("분리수거를 잘하자");
	Phone* pObj;
	pObj = &ph;
	std::cout << pObj->Receive();



	
}

```



```c
#include <iostream>
using namespace std;

class Phone
{
private:
	int num;
	int shape;
	const char* msg;
public:
	Phone() {}
	Phone(const char* msg)
	{
		this->msg = msg;
	}
	~Phone() {}
	const char* Receive() const { return this->msg; }
	void Call() {}
	void Send(const char* msg)
	{
		this->msg = msg;
	}
};

void main()
{
	
	Phone ph("분리수거를 잘하자");
	Phone* pObj;
	pObj = &ph;
	std::cout << pObj->Receive();



	
}
```

### 힙영역 메모리 할당

``c
#include <iostream>
using namespace std;
/*
new 연산자를 이용하여 메모리를 런타임에 동적으로 할당하도록 하자
(cin을 사용하여 사용자로부터 크기를 입력 받음)
메모리 타입은 int로 하고, 배열의 길이는 사용자로부터 입력 받자
*/


void main()
{
	
	int* pBuffer;
	int nLength;
	
	cin >> nLength;

	pBuffer = new int[nLength];
	



	delete[] pBuffer;


	
}
```

### 동적메모리 할당

```c
#include <iostream>
using namespace std;

void main()
{
	
	int* pBuffer;
	int nLength;
	
	cin >> nLength;
	pBuffer = new int[nLength];

	for (int i = 0; i < nLength; i++)
	{
		pBuffer[i] = i + 1;
	}

	for (int i = 0; i < nLength; i++)
	{
		cout << pBuffer[i] << " ";

	}
		
	delete[] pBuffer;


	
}
```
