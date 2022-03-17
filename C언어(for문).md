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
