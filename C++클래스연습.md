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
