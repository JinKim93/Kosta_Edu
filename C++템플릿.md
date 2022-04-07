# 템플릿

```c
void main()
{
  CStack<char> p; //<> 자바 등 언어에서 <>가보이면, 저문법은 '템플릿 구조구나' 인지하기
}
```

### 객체생성
- 클래스 템플릿이 정의되었으므로 객체를 생성할수 있다
- 멤버함수도 명확하게 호출될 때까지는 생성되지 않는다
- 클래스 템플릿의 객체가 생성될 때까지는 클래스 템플릿에 대한 어떠한 코드도 생성되지 않는다
```c
CStack<int> test(10);
```

### 값에 의한 복사(템플릿 작성)

```c
#include <iostream>

using namespace std;

template <class T> T Max(T a, T b)
{
	return (a > b) ? a : b;
}

void main()
{
	char ca = 'A', cb = 'B';
	int ia = 10, ib = 20;

	cout << Max(ca, cb) << endl;
	cout << Max(ia, ib) << endl;

}

```
















