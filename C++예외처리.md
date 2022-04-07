# 예외처리

- C++ 예외 처리 키워드
- try 예외 가능성이 있는 코드 영역을 처리한다. 이 블록에서 예외가 발생하면 throw 명령으로 예외를 넘긴다
- catch 예외 발생 시 예외를 잡아서 처리 한다
- throw 이 키워드를 만나면 예외를 처리하는 구문으로 던진다 

### 예외처리 하기 전(나누어야 할 수가 0인 경우)

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
		cout << "나누기결과" << a / b << endl;
	}
	


}
```

### 예외처리 후

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
	try
	{
		if (b == 0)
		{
			throw b;
		}
		cout << "나누기 결과: " << a / b << endl;
	}
	catch (int exp)
	{
		cout << "b에" << exp << "이 입력 되었습니다" << endl;
	}

}
```




