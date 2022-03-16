# C언어(switch ~ case문)
```c
#include <stdio.h>

int main(void)
{
	//피처폰의 단축키 지정
	int shortcut;
	printf("단축키를 입력하시오 : ");
	scanf_s("%d", &shortcut);
	switch (shortcut)
	{
	case 1:
		printf("딸 : 010 ~~\n");
		break;
	case 2:
		printf("아들 : 010~~\n");
		break;
	case 3:
		printf("남편 : 010 ~~\n");
		break;
	case 4:
		printf("부인 : 010 ~~ \n");
		break;
	default:
		printf("해당 단축키가 없습니다\n");
		break;

	}
	
	return 0;
}
```
