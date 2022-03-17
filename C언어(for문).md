# C언어 for문(구구단)

```c
#include <stdio.h>

int main()
{
	
	for (int dan =2; dan < 10; dan++)
	{
		
		for(int b = 1; b < 10; b++)
		{ 
			printf("%d * %d = %d\n", dan, b, dan * b);

		}
		printf("\n");
	
	}


	return 0;
}
```

# C언어 for문(별찍기)

![캡쳐](https://user-images.githubusercontent.com/82345970/158724015-eb2fd5a7-16ba-405a-af3f-0224698586b6.PNG)

```c
#include <stdio.h>

int main()
{
	for (int i = 1; i <= 5; i++)
	{
		for (int j = 0; j < i; j++)
		{
			printf("*");
		}
		printf("\n");
	}

	return 0;
}
