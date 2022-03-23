# C언어 동적메모리 할당
### 메모리 영역
- 코드 영역 -> 실행 명령어 저장
- 스택 영역 -> 지역변수 및 매개변수 저장
- 힙 영역 -> 프로그래머가 직접할당
- 데이터 영역 -> 전역변수, static 변수 저장

### 동적 메모리 할당 함수의 원형
```c
void *malloc(size_t size)
```
- 전달인자 size는 byte 단위로 입력
- 메모리 할당이 되면 메모리의 주소값을 리턴
- 메모리 부족 시 NULL 포인터 리턴
- 리턴형 void* 인데, 타입이 지정되어 있지 않는 포인터를 리턴(난 당신이 원하는 메모리 크기만큼 할당해줄테니, 메모리는 당신이 원하는 형태로 정해서 사용해라)

### 동적 메모리 해제 함수의 원형
```c
void free(void* memblock);
```
- 메모리 사용 후 반드시 해제해주어야 한다.
- 전달인자로 메모리를 가리키는 포인터를 대입한다.

### 동적 메모리 할당_예제_1
```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
	
	int num;
	int* student;

	fputs("학생수를 입력하세요 : ", stdout);
	scanf_s("%d", &num);

	student = (int*)malloc(sizeof(int) * num); //동적메모리할당

	if (student == NULL) //널 포인터 검사 무조건 작성해야한다 
	{
		printf("메모리가 부족하여 메모리를 할당 할수 없습니다.\n");
		return 0;

	}
	printf("할당된 메모리의 크기는 %d 입니다\n", sizeof(int) * num);

	free(student); //동적메모리해제

		
	return 0;
} 
```
### 동적 메모리 할당_예제_2
```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
	int num, i, total = 0;
	int* student;
	fputs("학생수를 입력하세요 :", stdout);
	scanf_s("%d", &num);
	student = (int*)malloc(sizeof(int) * num);
	if (student == NULL)
	{
		printf("메모리가 부족하여 메모리를 할당할 수 없습니다\n");
		return 0;
	}
	for (i = 0; i < num; i++)
	{
		printf("%d번째 학생의 성적 입력 :", i + 1);
		scanf_s("%d", &student[i]);
	}
	for (i = 0; i < num; i++)
	{
		total += student[i];
	}
	printf("총점 : %d, 평균 : %d\n", total, total / num);
	free(student);

	return 0;
} 
```
