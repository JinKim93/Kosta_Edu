# 동적배열
- 신축성 있는 배열이 필요
- 실행 중에 필요한 만큼 늘렸다, 줄였다 할 수 있는 배열을 동적배열이라고 한다
- 기존 할당된 메모리를 재할당 하는 realloc함수를 사용하면 됨

### 배열의 한계(동적배열 구성 전)
```c
#include <stdio.h>
#include <string.h>

char ar[16] = "abcdef";
void Insert(int idx, char ch)
{

	memmove(ar + idx + 1, ar + idx, strlen(ar) - idx + 1);
	ar[idx] = ch;
}

void Delete(int idx)
{
	memmove(ar + idx, ar + idx + 1, strlen(ar) - idx);
}

void Append(char ch)
{
	Insert(strlen(ar), ch);
}

void main()
{

	printf("최초 : %s\n", ar);
	Insert(3, 't');
	printf("t삽입 : %s\n", ar);
	Delete(1);
	printf("b삭제 : %s\n", ar);
	Append('s');
	printf("s추가 : %s\n", ar);

}
```

### 배열의 한계 극복(동적배열로 구성)
```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

#define ELETYPE int
ELETYPE* ar;
unsigned size;
unsigned num;
unsigned growby;

void InitArray(unsigned asize, unsigned agrowby)
{
	size = asize;
	growby = agrowby;
	num = 0;
	ar = (ELETYPE*)malloc(size * sizeof(ELETYPE));
}

void Insert(int idx, ELETYPE value)
{

	unsigned need;
	need = num + 1;
	if (need > size)
	{
		size = need + growby;
		ar = (ELETYPE*)realloc(ar, size * sizeof(ELETYPE));
	}
	memmove(ar + idx + 1, ar + idx, (num - idx) * sizeof(ELETYPE));
	ar[idx] = value;
	num++;
	
}

void Delete(int idx)
{
	memmove(ar + idx, ar + idx + 1, (num - idx) * sizeof(ELETYPE));
	num--;
}

void Append(ELETYPE value)
{
	Insert(num,value);
}

void UnInitArray()
{
	free(ar);
}

void DumpArray(const char* sMark)
{
	unsigned i;
	printf("%16s => 크기=%02d,개수=%02d : ", sMark, size, num);
	for (i = 0 ; i < num; i++)
	{
		printf("%2d", ar[i]);
	}
	printf("\n");
}


void main()
{
	
	
	int i;
	InitArray(10, 5);
	DumpArray("최초");
	for (i = 1; i <= 8; i++)
	{
		Append(i);
	}
	DumpArray("8개 추가");
	Insert(3,10); 
	DumpArray("10 삽입");
	Insert(3,11);
	DumpArray("11 삽입");
	Insert(3,12); 
	DumpArray("12 삽입");
	Delete(7); 
	DumpArray("요소 7 삭제");
	UnInitArray();
	
}
```

### 주소록 저장 프로그램
```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <conio.h>

typedef struct _NameCard
{
	char name[10];
	char tel[15];
	char addr[32];
}ELETYPE;

ELETYPE* ar;
unsigned size;
unsigned num;
unsigned growby;

void InitArray(unsigned asize, unsigned agrowby)
{
	size = asize;
	growby = agrowby;
	num = 0;
	ar = (ELETYPE*)malloc(size*sizeof(ELETYPE));
}

void Insert(int idx, ELETYPE value)
{

	unsigned need;
	need = num + 1;
	if (need > size)
	{
		size = need + growby;
		ar = (ELETYPE*)realloc(ar,size*sizeof(ELETYPE));
	}
	memmove(ar + idx + 1, ar + idx, (num - idx)*sizeof(ELETYPE));
	ar[idx] = value;
	num++;

}

void Delete(int idx)
{
	memmove(ar + idx, ar + idx + 1, (num - idx) * sizeof(ELETYPE));
	num--;
}

void Append(ELETYPE value)
{
	Insert(num, value);
}

void UnInitArray()
{
	free(ar);
}

void DumpArray(const char* sMark)
{
	unsigned i;
	printf("%16s => 크기=%02d,개수=%02d : ", sMark, size, num);
	for (i = 0; i < num; i++)
	{
		printf("%2d", ar[i]);
	}
	printf("\n");
}


void main()
{

	char ch;
	unsigned i;
	ELETYPE Temp;

	InitArray(10, 5);
	for (;;) {
		printf("명령을 입력하세요(1:보기, 2:추가 3:삭제, Q:종료) > ");
		ch = _getch();
		printf("\n");
		if (ch == 'Q' || ch == 'q')	{
			break;
		}
	
		switch (ch)
		{
		case '1':
			if (num == 0)
			{
				printf("등록된 내용이 없습니다\n");

			}
			else
			{
				for (i = 0; i < num; i++)
				{
					printf("%d, 이름:%s, 전화:%s, 주소:%s\n", i, ar[i].name, ar[i].tel, ar[i].addr);
				}
			}
			break;

		case '2':
			printf("이름을 입력하세요(9자) : ");
			fgets(Temp.name, 9, stdin);
			printf("전화번호를 입력하세요(14자) : ");
			fgets(Temp.tel, 14, stdin);
			printf("주소를 입력하세요(31자) : ");
			fgets(Temp.addr, 31, stdin);
			Append(Temp);
			break;

		case '3':
			printf("삭제할 번호를 입력하세요 :");
			scanf_s("%d", &i);
			if (i < num)
			{
				Delete(i);
			}
			else
			{
				printf("등록되지 않은 번호입니다\n");
			}
			break;
		}

	}
	UnInitArray();
}
```
                           
                         
