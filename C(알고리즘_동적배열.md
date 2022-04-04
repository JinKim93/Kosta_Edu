# 동적배열
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


                           
                         
