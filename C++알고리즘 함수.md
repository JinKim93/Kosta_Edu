# find 알고리즘 함수

- 백터,리스트에서 둘다 사용 가능

```c
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>
using namespace std;

void main()
{			
	int arr[] = { 10,20,30,40,50 };
	vector<int> vec1(&arr[0], &arr[5]);
	vector<int>::iterator it;

	if (find(vec1.begin(), vec1.end(), 30) != vec1.end()) //find함수 처음부터 끝 다음까지 30숫자 찾아라
	{
		cout << "검색성공" << endl;
	}
	else
	{
		cout << "검색실패" << endl;
	}

}
```

# sort 알고리즘 함수

```c
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>
using namespace std;

void main()
{			
	int arr[] = { 49,26,19,77,34,52,84,34,92,69 };
	vector<int> vi(&arr[0], &arr[10]);
	vector<int>::iterator it;
	for (it = vi.begin(); it != vi.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;

	sort(vi.begin(), vi.end());
	for (it = vi.begin(); it != vi.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}
```
 
