# JAVA do-while문

### 입력한 수를 더하는 프로그램을 구하시오
- 0입력시 프로그램종료
- while문작성, do-while문 작성시 차이점 이해 하기
### while문으로 작성

```java
package ch18;

import java.util.Scanner; //Scanner scanner = new Scanner(System.in);


public class dowhileTest {
	
	public static void main(String[] args)
	{
		Scanner scanner = new Scanner(System.in);
		int input;
		int sum = 0;
		input = scanner.nextInt();
		
		while(input != 0)
		{
			sum+=input;
			input = scanner.nextInt();
		}
		System.out.println("sum의 값은" +sum);
	}

}
```

### do-while문으로 작성
```java
package ch18;

import java.util.Scanner; //Scanner scanner = new Scanner(System.in);


public class dowhileTest {
	
	public static void main(String[] args)
	{
		Scanner scanner = new Scanner(System.in);
		int input;
		int sum = 0;
		
		
		do
		{	System.out.println("수를 입력하세요");
			input = scanner.nextInt();
			sum+=input;
			
		}while(input != 0);
		
		System.out.println("sum의 값은" +sum);
	}

}
```
