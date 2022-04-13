# 복사생성자
- 객체 생성 시 초기화를 하되, 생성되는 객체를 다른 객체로 초기화 시에 호출된다

```c
#include <iostream>
using namespace std;

class String
{
public:
	String(char ch, int nSize);
	~String();
	String(const String& s);

	void operator=(const String& s);
	void SetData();
private:
	int nLength;
	char* pBuffer;
};

String::String(char ch, int nSize)
{
	nLength = nSize;
	pBuffer = new char[nLength + 1];
	memset(pBuffer, ch, nLength);
	pBuffer[nLength] = '\0';
}

String::~String()
{
	delete pBuffer;

}

String::String(const String& s) //s = str1
{
	//str2 호출
	this->nLength = s.nLength;
	this->pBuffer = new char[this->nLength + 1];
	strcpy_s(this->pBuffer,nLength+1, s.pBuffer);
}

void String::operator=(const String& s)
{
	if (&s == this) //객체의 자기 자신 대입 시에 대한 처리
	{
		return;
	}
	delete this->pBuffer;
	this->nLength = s.nLength;
	this->pBuffer = new char[this->nLength + 1];
	strcpy_s(this->pBuffer, nLength + 1, s.pBuffer);
}

void String::SetData()
{
	cout << "pBuffer :" << this->pBuffer << endl;
	cout << "nLength :" << this->nLength << endl;

}

void main()
{

	String str1('A', 3);
	String str2 = str1; // String str2(str1);
	str1 = str1; //str2.operator=(str1);
	cout << "대입 후 str2";
	str2.SetData();

}
```
