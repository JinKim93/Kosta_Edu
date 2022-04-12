# hash_map(unorded_map)
- STL에서 관련하여 hash_map을 지원함 -> 하지만 표준은 아님
- map과의 차이점은 hash라는 자료구조를 사용함으로써 검색 속도가 빠름

### 사용형태
- 헤더파일
```c
#include <hash_map>
```

- 변수,반복자 타입
```c
hash_map < key 자료형, value 자료형 > 변수
```

### hash_map(unorded_map) 간단예제
```c
#include <iostream>
#include <unordered_map>

using namespace std;
using namespace stdext;

void main()
{			
	
	vector<string> str;//hash_map안에 value값으로 쓸 백터
	unordered_map<string, int> test1; //키값 문자열, value 정수형
	unordered_map<string, vector<string>> test2; // value(data)값을 vector<string>(컨테이너)다

	test1["구현준"] = 123;
	test1["최성현"] = 789;
	
	unordered_map<string, int>::iterator it; // hash_map<string,int>타입에 소속되있는 iterator
	
	for (it = test1.begin(); it != test1.end(); it++)
	{	//first 키값, second value값
		cout << it->first << " : " << it->second << endl;
	}
	


}
```

### hash_map(unorded_map)
```c
#include <iostream>
#include <unordered_map>

using namespace std;
using namespace stdext;

void main()
{			
	
	vector<string> str;//hash_map안에 value값으로 쓸 백터
	unordered_map<string, int> test1; //키값 문자열, value 정수형
	unordered_map<string, vector<string>> test2; // value(data)값을 vector<string>(컨테이너)다

	test1["구현준"] = 123;
	test1["최성현"] = 789;
	
	unordered_map<string, int>::iterator it; // hash_map<string,int>타입에 소속되있는 iterator
	
	for (it = test1.begin(); it != test1.end(); it++)
	{	//first 키값, second value값
		cout << it->first << " : " << it->second << endl;
	}
	
	str.push_back("서울시 강남구"); // 데이터 백터에 넣어줌
	str.push_back("성남시 분당구");

	test2["주소1"] = str; // 주소1에는 서울시 강남구, 성남시 분당구가 들어감
	
	str.clear(); //clear함수를 쓰면 서울시 강남구, 성남시 분당구가 사라짐 -> 새로운 백터 생성하기 위해

	str.push_back("수원시 영통구");
	str.push_back("수원시 권선구");

	test2["주소2"] = str; //새로운 백터를 새로운 키값을 넣어좀
							
	unordered_map<string, vector<string>> ::iterator it2;
	vector < string>::iterator vit;

	for (it2 = test2.begin(); it2 != test2.end(); it2++)
	{
		for (vit = it2->second.begin(); vit != it2->second.end(); vit++)
		{
			cout << it2->first << endl; //키 값 출력 -> 주소1에 있는 백터의 값 str을 풀어해친게 하기 *vit이다
			cout << *vit << endl;
		}
		 
	}

}
```
