# 객체 포인터
- 객체의 주소값을 저장하기 위한 변수
- 객체를 간접 참조하기 위해 사용

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
	int GetX() { return x; }
	int GetY() { return y; }
};

void MousePoint::SetXY(int nX, int nY) {
	x = nX;
	y = nY;
}
MousePoint::MousePoint() {
	x = 10;
	y = 20;
	cout << "생성자 호출~!!" << endl;
}
MousePoint::~MousePoint() {// 소멸자
	cout << "소멸자 호출~!!" << endl;
}
MousePoint::MousePoint(int nX, int nY) {
	x = nX;
	y = nY;
}

void main()
{
	MousePoint* pObj;
	MousePoint pt(10, 20);

	pObj = &pt;

	cout << pt.GetX() << endl; // 직접 참조 연산자
	cout << pt.GetY() << endl;

	cout << pObj->GetX() << endl; // 간접 참조 연산자
	cout << pObj->GetY() << endl;
}
```
