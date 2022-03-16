# switch ~ case문 
## 91점이상 100점이하 A 학점 / 81점이상 90점이하 B학점 / 71점이상 80점이하 C학점 / 61점이상 70점이하 D학점
```
#include <stdio.h>

int main(void)
{	//91 ~ 100 A학점 , 81 ~ 90 B학점
	int score = 0;
	printf("점수를 입력하시오\n");
	scanf_s("%d", &score);
	
	score = (score-1) / 10;
	switch (score)
	{
	case 9:
		printf("A학점입니다\n");
		break;
	case 8:
		printf("B학점 입니다\n");
		break;
	case 7:
		printf("C학점 입니다\n");
		break;
	case 6:
		printf("D학점 입니다\n");
		break;
	case 5:
	case 4:
	case 3:
	case 2:
	case 1:
	case 0:
		printf("범위에 없습니다\n");
		break;
	}

	return 0;
}
```
