# switch ~ case문
### 휴대폰 단축키 지정
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

# 해당 월에 해당하는 계절을 출력하시오.
### switch ~ case문 작성할떄 break를 이용해서 문법 중복방지
```c
#include <stdio.h>

int main(void)
{
	
	int month = 0;
	printf("월을 입력하시오: ");
	scanf_s("%d", &month);
	switch (month)
	{
		
	
	case 3:
	case 4:
	case 5:
		printf("봄 입니다\n");
		break;
	case 6:
	case 7:
	case 8:
		printf("여름 입니다\n");
		break;
	case 9:
	case 10:
	case 11:
		printf("가을 입니다\n");
		break;
	case 1:
		printf("겨울 입니다\n");
		break;
	case 2:
		printf("겨울 입니다\n");
		break;
	case 12:
		printf("겨울 입니다\n");
		break;
	default:
		printf("해당 단축키가 없습니다\n");
		break;

	}
	
	return 0;
}
```

