# static 멤버함수
### 객체 상태 정보 관리
- static 멤버는 클래스 내에서 단 한번 생성하고 초기화 된다.
- static 멤버를 사용하여 객체의 상태 정보 관리에 사용 가능

```c
#include <iostream>

using namespace std;
class Deposit
{
public:
		Deposit() //전달인자 없이 default 생성자 -> 오버로딩
		{
			nCount++;
			cout << "객체 생성 개수 : " << nCount << endl;

		}
		~Deposit() // 소멸자
		{
			nCount--;
			cout << "객체 생성 개수 : " << nCount << endl;

		}
		Deposit(char* name, double balance) //전달인자 2개 생성자 -> 오버로딩
		{
			strName = name;
			dBalance = balance;

		}
		void BankBalance() //멤버함수 (현재잔액 알아보는 함수)
		{
			dBalance = dBalance + (dBalance * dInterestRate); // 원금에 이자율을 더한값
		}

		static void SetInterestRate(double dNewRate)
		{

			dInterestRate = dNewRate;

		}
		static double GetInterestRate()
		{

			return dInterestRate;

		}

private:

	char* strName;
	double dBalance; // 원금
	static double dInterestRate; // 이자율
	static int nCount;

};

double Deposit::dInterestRate = 0.05; //초기화
int Deposit::nCount = 0;


void main()
{
	
	Deposit custom1;
	Deposit custom2;
	Deposit custom3;
	Deposit custom4;

}
```
