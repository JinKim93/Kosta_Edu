# C++ 객체 포인터 배열

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
	MousePoint();//디폴트 생성자
	MousePoint(int nX, int nY);
	~MousePoint();//소멸자
	int GetX() const
	{
		return this->x;
	}
	int GetY() const
	{
		return this->y;
	}
};

void MousePoint::SetXY(int x, int y)
{
	this->x = x;
	this->y = y;
}
MousePoint::MousePoint()//디폴트 생성자
{
	x = 10;
	y = 20;
	cout << "생성자 호출~!!" << endl;
}
MousePoint::~MousePoint()//소멸자
{
	cout << "소멸자 호출~!!" << endl;
}
MousePoint::MousePoint(int nX, int nY)
{
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

MousePoint& CopyObject(MousePoint& pt1, MousePoint& pt2)
{
	pt1 = pt2;
	cout << "pt1.GetX : " << pt1.GetX() << endl;
	cout << "pt1.GetY : " << pt1.GetY() << endl;
	return pt1;
}

void main()
{
	MousePoint* pt[3];

	pt[0] = new MousePoint(10, 20);
	pt[1] = new MousePoint(100, 200);
	pt[2] = new MousePoint(1000, 2000);

	for (int i = 0; i < 3; i++)
	{
		cout << "X좌표 : " << pt[i]->GetX() << endl;
		cout << "Y좌표 : " << pt[i]->GetY() << endl;
	}
	
	
	for (int i = 0 ; i < 3; i++ )
	{
		delete pt[i];
	}
	

}
```
