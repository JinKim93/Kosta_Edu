# static 멤버를 가지는 클래스의 선언 및 구조
- 실제 은행 예금 계좌를 나타내느 클래스를 작성

```c
#include <iostream>

using namespace std;
class Deposit
{
public:
		Deposit() //전달인자 없이 default 생성자 -> 오버로딩
		{
	

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

};

double Deposit::dInterestRate = 0.05;


void main()
{
	
	cout << "변경된 이자전 : " << Deposit::GetInterestRate() << endl;
	Deposit::SetInterestRate(0.03); //클래스 이름으로 접근하는거는 static 변수이다.('공통변수'라고 생각하자)
	cout << "변경된 이자율 : " << Deposit::GetInterestRate() << endl;
}
```
