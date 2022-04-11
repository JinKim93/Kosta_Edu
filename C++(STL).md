# STL(Standard Templete Library)
- 표준 템플릿 라이브러리
- 템플릿의 철학은 누구나 공통적으로 사용하기 위한 일반화(Generic) 프로그래밍을 기반으로한다

### 컨테이너
- 배열처럼 동일한 요소들로 구성되어야 함
- 순차 컨테이너, 정렬 연관 컨테이너로 나눌 수 있다

### 순차 컨테이너
- 동일한 객체가 선형으로 구성된 집합으로 **백터,데크,리스트** 가 있다
- **벡터,리스트** 중요
- **벡터** : 구성요소게 임의 접근이 가능, 요소 끝에 삽입/삭제 빠름, 처음이나 중간 삽입/삭제는 요소 개수에 따라 처리속도가 비례
- **데크** : 벡터와 비슷, 차이점은 요소 양끝에 삽입/삭제가 가능하다는 점, 선능 또한 벡터와 같이 요소 개수에 따라 처리속도가 비례
- **리스트** : 구성 요소에 선형적으로 접근한다. 요소에 삽입과 삭제가 위치에 상관 없이 같은 속도로 처리

### 백터
- 필요한 크기만큼 메모리를 자동으로 재할당하여 늘릴 수 있음
- 배열인대, 메모리를 늘렸다, 줄였다 -> 즉 필요한만큼 쓸 수 있는 배열이라고 생각하자

### 벡터의 사용형태
- 백터의 형식으로 타입이 T형인 백터 객체를 선언한 형태
```c

vector<T> vec1;
```

- 타입이 int형인 벡터를 생성하려면?
```c
vector<int> vec1;
```

- 백터의 크기를 미리 지정할 수도 있다
```c
vector<int> vec1(5); //20byt 메모리할당 -> 내부적으로 동적할당 일어남
```
### 백터사용 예제
```c
#include <iostream>
#include <vector>
using namespace std;

void main()
{
	int i, num;
	cout << "배열의 크기 입력 : ";
	cin >> num;

	vector<int> arr(num);

	//sizeof(arr)/sizeof(int) -> 배열의크기 구할때 정의 했는대
	//백터를 사용하면 arr.size()로 표현 가능
	for (i = 0; i < arr.size(); i++)
	{
		arr[i] = i + 1;
	}
	for (i = 0; i < arr.size(); i++)
	{
		cout << "arr[" << i << "]=" << arr[i] << endl;

	}
}
```

### 벡터 push_back()
- 빈벡터를 생성한 후 루프를 통해 push_back() 함수로 백터의 뒤쪽에 5개의 요소를 추가함
- 백터는 요소를 인접한 메모리 위치에 연속적으로 저장하므로 요소에 빠르게 접근
- 중간에 요소를 삽입, 삭제 시에는 발생 기준 메모리에서 전체를 밀고 당겨야 하므로 상대적으로 속도가 느리다
```c
#include <iostream>
#include <vector>
using namespace std;

void main()
{
	int i;
	int num;
	cout << "배열의 크기 입력 : ";
	cin >> num;

	vector<int> arr;

	//sizeof(arr)/sizeof(int) -> 배열의크기 구할때 정의 했는대
	//백터를 사용하면 arr.size()로 표현 가능
	for (int i = 0; i < num; i++)
	{
		//arr[i] = i + 1;
		arr.push_back(i + 1);
	}
	for (int i = 0; i < arr.size(); i++)
	{
		cout << "arr[" << i << "]=" << arr[i] << endl;

	}
}
```

### 데크
- 데크는 양쪽 끝에서 데이터를 삽입 및 삭제할 수 있는 컨테이너
- 벡터와의 차이점은 데이터를 끝에서만 삽입, 삭제 하느냐 양쪽 끝에서 하느냐의 차이다

### 데크의 사용형태
```c
deque<T> dq;
```

### 데크 예제
```c
#include <iostream>
#include <vector>
#include <deque>
using namespace std;

void main()
{
	
	deque<int> num;
	num.push_back(5);
	num.push_back(6);
	num.push_front(2);
	num.push_front(1);

	for (int i = 0; i < num.size(); i++)
	{
		cout << num[i] << " ";
	}
	cout << endl;

	

}
```

### 리스트
- 이중 연결 리스트로 구현되어 있는 컨테이너
- 연결 리스트는 노드라는 것이 붙어 있어서 데이터가 물리적으로 인접해있지 않고, 논리적인 순서를 기억하므로 데이터 삽입, 삭제의 속도가 상대적 빠름

### 리스트 사용형태
```c
list<T> lst;
```

### 리스트 멤버함수
- push_front 가장 앞에 요소 삽입
- push_back 가장 뒤에 요소 삽입
- pop_front 가장 앞에 요소 삭제
- pop_back 가장 뒤에 요소 삭제

### 리스트 예제
```c
#include <iostream>
#include <vector>
#include <list>
using namespace std;

void main()
{
	list<int> lst;
	int i;
	for (i = 0; i<5; i++)
	{
		lst.push_back(i);
	}

	list<int>::iterator it; //iterater -> 반복자를 통해 포인터로 데이터 접근해야함
	for (it = lst.begin(); it != lst.end(); it++, i++)
	{
		cout << i << "번째 = " << *it << endl;

	}
}
```

### 정렬 연관 컨테이너
- **맵 중요**
- 키를 사용하여 데이터를 신속하게 찾아냄
- 실행 시 크기를동적으로 변경할 수 있다

### 반복자
- 컨테이너의 요소를 가리키는 객체, 컨테이너의 시작부터 끝까지 이동하면서 요소를 읽거나 쓰기 위해 사용
- 컴파일러의 내부 알고리즘은 컴파일러 제작 회사마다 다름



