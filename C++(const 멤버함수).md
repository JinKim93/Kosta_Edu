# const 멤버함수
- const 사용 목적은 객체의 멤버변수를 변경시킬 수 없도록 하기 위함
- get함수(받는거) -> const 무조건 쓴다.
- set함수(얻는거) -> 데이터를 줘야 하니까 const 쓰면 안됨

```c
#include <iostream>
using namespace std;

class MousePoint {
private:
	int x;
	int y;

public:
	void SetXY(int nX, int nY);
	MousePoint();//생성자
	MousePoint(int nX, int nY);
	~MousePoint();// 소멸자
	int GetX() const
	{ 
		return this -> x; 
	}
	int GetY() const
	{
		return this -> y; 
	}
};

void MousePoint::SetXY(int x, int y) 
{
	this -> x = x;
	this -> y = y;
}
MousePoint::MousePoint() //디폴트 생성자
{
	x = 10;
	y = 20;
	cout << "생성자 호출~!!" << endl;
}
MousePoint::~MousePoint() // 소멸자
{
	cout << "소멸자 호출~!!" << endl;
}
MousePoint::MousePoint(int nX, int nY) {
	x = nX;
	y = nY;
}

void SetRect(MousePoint pt1, MousePoint pt2)
{
	cout << "pt1.GetX : " << pt1.GetX() << endl;
	cout << "pt1.GetY : " << pt1.GetY() << endl;
	pt1.SetXY(1000, 2000);
	cout << "pt1.GetX : " << pt1.GetX() << endl;
	cout << "pt1.GetY : " << pt1.GetY() << endl;
}

MousePoint & CopyObject(MousePoint &pt1, MousePoint &pt2)
{
	pt1 = pt2;
	cout << "pt1.GetX : " << pt1.GetX() << endl;
	cout << "pt1.GetY : " << pt1.GetY() << endl;
	return pt1;

}
void main()
{
	
	MousePoint mp1(10, 20), mp2(100, 200);
	cout << "mp1.GetX : " << mp1.GetX() << endl;
	cout << "mp1.GetY : " << mp1.GetY() << endl;
	MousePoint ret = CopyObject(mp1, mp2);
	//SetRect(mp1, mp2);
	cout << "mp1.GetX : " << ret.GetX() << endl;
	cout << "mp1.GetY : " << ret.GetY() << endl;
}
```

