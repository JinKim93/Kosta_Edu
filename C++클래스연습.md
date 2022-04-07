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
