## C언어_함수_연습문제

### 책 읽기 마라톤 기능을 가진 프로그램</br>읽은책페이지: 30</br>최종누적페이지: 30</br>읽은책페이지: 20</br>최종누적페이지: 20</br>읽은책페이지: -1</br>더 분발하세요. 출력하시오 

### 함수 쓰기 전 코드
```c
#include <stdio.h>

int main(void)
{
	int page = 0;
	int sum = 0;
	do {
		printf("페이지 수를 입력하세요 : ");
		scanf_s("%d", &page);
		if (page == -1)
		{
			printf("더 분발하세요\n");
			break;
		}
		sum = sum + page;
		printf("최종 누적 페이지 : %d\n", sum);
	} while (page != -1);



	return 0;
}
```


### 함수 사용 코드(변수활용 static)

```c
#include <stdio.h>

void Add(int cnt)
{
	static int sum = 0; //static을 사용 안하면 sum이 0으로 계속 초기화 되서 누적이 안 된다.
	if (cnt == -1)
	{
		printf("더 분발하세요 \n");
		
	}
	else
	{
		sum = sum + cnt;
		printf("최종 누적 페이지 : %d\n", sum);
	}
}
int main(void)
{

	int page = 0;

	do {
		printf("페이지 수를 입력하세요 : ");
		scanf_s("%d", &page);
		Add(page);
	} while (page != -1);
	return 0;
}
```



