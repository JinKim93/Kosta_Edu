# friend
- 클래스의 멤버변수 접근 지정자는 privacte으로 외부로부터 접근 차단
- 오직 멤버함수를 통해서만 멤버변수에 접근이 가능
- 이러한 기본 규칙을 깨는 변칙적인 기능이 'friend'이다
- 프렌드라는 의미는 친구라는 의미로 '나에게로 접근을 허용하겠다'라는 의미

# new / delete 연산자 (동적메모리)
### 동적메모리의 필요성
- 동적메모리는 실행시간에 할당되어 사용되는 메모리 블록
- 동적메모리의 반댓말은 정적 메모리(스택)
- 동적 메모리는 프로그램 작성시 얼마만큼의 메모리가 필요하지 알지 못하는 경우에 사용 됨
- 동적 메모리 영역을 힙(heap)영역이라고 함
- 객체지향에서는 동적 메모리 생성 시 new, 소멸 시 delete(C++)연산자를 사용

### new연산자
- C++ 에서는 힙 메모리에 동적 메모리를 할당할 때 new 연산자를 이용
- 자신이 할당하는 객체의 데이터형을 알고 있다
- 데이터형의 포인터를 반환함

```c
#include <iostream>

using namespace std;


void main()
{
	
	int* pBuffer;
	int nLength;
	cout << "힙 영역에 할당할 메모리 수:";
	cin >> nLength;

	pBuffer = new int[nLength];

	for (int i = 0; i < nLength; i++)
	{
		pBuffer[i] = i + 1;
	}
	for (int i = 0; i < nLength; i++)
	{
		cout << pBuffer[i] << "";
		cout << endl;
		delete[] pBuffer;
	}

}
```

