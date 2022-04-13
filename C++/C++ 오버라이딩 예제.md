```c
//Emplayee : 이름, 주소

#include<iostream>

using namespace std;
class Employee
{
public:
	Employee();
	~Employee();
	Employee(const char* pName, const char* pAddr);
	void Display();
	virtual double PayCheck() const = 0; //순수가상함수
protected:
	char* strName;
	char* strAddr;
};

class Regular : public Employee
{
public:
	Regular() {};
	~Regular() { cout << "Regular 소멸자호출" << endl; };
	Regular(const char* pName, const char* pAddr, double dSalary);
	double PayCheck() const;
private:
	double salary;
};

Regular::Regular(const char* pName, const char* pAddr, double dSalary) :Employee(pName, pAddr)
{
	//cout << "Regular 생성자"  << endl;
	/*strName = new char[strlen(pName) + 1];
	strAddr = new char[strlen(pAddr) + 1];
	strcpy_s(strName, strlen(pName) + 1, pName);
	strcpy_s(strAddr, strlen(pAddr) + 1, pAddr);*/
	salary = dSalary;
	//cout << "이름 : " << strName << endl;
	//cout << "주소 : " << strAddr << endl;
}

double Regular::PayCheck() const
{
	return salary;
}

class Temporary : public Employee
{
public:
	Temporary() {};
	~Temporary() { cout << "Temporary 소멸자호출" << endl; };
	Temporary(const char* pName, const char* pAddr, double dDailyPayCheck, int nDays);
	double PayCheck() const;
private:
	double dailyPayCheck;
	int days;
};

Temporary::Temporary(const char* pName, const char* pAddr, double dDailyPayCheck, int nDays)
	:Employee(pName, pAddr)
{
	//cout << "Temporary 생성자" << endl;
	/*strName = new char[strlen(pName) + 1];
	strAddr = new char[strlen(pAddr) + 1];
	strcpy_s(strName, strlen(pName) + 1, pName);
	strcpy_s(strAddr, strlen(pAddr) + 1, pAddr);*/
	dailyPayCheck = dDailyPayCheck;
	days = nDays;
	//cout << "이름 : " << strName << endl;
	//cout << "주소 : " << strAddr << endl;
}

double Temporary::PayCheck() const
{
	return dailyPayCheck * days;
}

Employee::Employee()
{
	strName = NULL;
	strAddr = NULL;
	//cout << "Employee 디폴트 생성자" << endl;
}
Employee::Employee(const char* pName, const char* pAddr)
{
	strName = new char[strlen(pName) + 1];
	strAddr = new char[strlen(pAddr) + 1];
	strcpy_s(strName, strlen(pName) + 1, pName);
	strcpy_s(strAddr, strlen(pAddr) + 1, pAddr);
	//cout << "Employee 전달인자가 2개인 생성자" << endl;
}

Employee::~Employee()
{
	delete[] strName;
	delete[] strAddr;
	//cout << "Employee 소멸자" << endl;
}

void Employee::Display()
{
	cout << "이름 : " << strName << endl;
	cout << "주소 : " << strAddr << endl;
}

class SalesMan : public Regular
{
public:
	SalesMan();
	~SalesMan();
	SalesMan(const char* pName, const char* pAddr, double dSalary, double dallowance);
	double PayCheck() const;
private:
	double allowance;
};

SalesMan::SalesMan()
{
	//cout << "SalesMan 디폴트 생성자" << endl;
}
SalesMan::~SalesMan()
{
	//cout << "SalesMan 소멸자" << endl;
}
SalesMan::SalesMan(const char* pName, const char* pAddr, double dSalary, double dallowance) :Regular(pName, pAddr, dSalary)
{
	allowance = dallowance;
	//cout << "SalesMan 전달인자 4개인 생성자" << endl;
}

double SalesMan::PayCheck() const
{
	return Regular::PayCheck() + allowance;
}

class Department {
public:
	Department() {
		count = 0;
	}
	~Department() {

	}
	void AddEmployee(Employee& emp)
	{
		employee[count] = &emp;
		count++;
	}
	void DepartDisplay() const
	{
		for (int i = 0; i < count; i++)
		{
			employee[i]->Display();
			cout << "급여 :" << employee[i]->PayCheck() << endl;
		}
	}
private:
	int count;
	Employee* employee[10];
};


void main()
{
	Regular kim("김범준", "강남구", 100);
	//cout << "급여 : " << kim.PayCheck() << endl;

	Temporary son("손유경", "분당구", 200, 10);
	//cout << "급여 : " << son.PayCheck() << endl;

	SalesMan slm("홍길동", "영통구", 100, 50);
	//cout << "급여 : " << slm.PayCheck() << endl;

	//int a = (int)3.14;
	//Employee* employee = (Employee*)&slm;
	//cout << employee->PayCheck() << endl;

	Department dept;
	dept.AddEmployee(kim);
	dept.AddEmployee(son);
	dept.AddEmployee(slm);
	dept.DepartDisplay();
}
```
