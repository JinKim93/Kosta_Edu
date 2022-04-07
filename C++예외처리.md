# 예외처리

### 정수를 0으로 나누는 경우(예외처리 전)

```c
#include <iostream>

using namespace std;



void main()
{
	int a, b;
	cout << "나누어질수 입력:";
	cin >> a;
	cout << "나누는수 입력:";
	cin >> b;
	cout << "나누기결과" << a / b << endl;
}
```

### 정수를 0으로 나누는 경우(예외처리 후)

```c
#include <iostream>

using namespace std;



void main()
{
	int a, b;
	cout << "나누어질수 입력:";
	cin >> a;
	cout << "나누는수 입력:";
	cin >> b;
	if (b > 0)
	{
		cout << "나누기 결과" << a / b << endl;
	}
	else
	{
		cout << "나눌수 없습니다" << endl;
	}

}
```


