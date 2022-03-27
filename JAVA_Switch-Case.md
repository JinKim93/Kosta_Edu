# JAVA switch-case 문

### 한 달이 며칠인지 알려주는 프로그램을 구현하시오
```java
package ch16;

import java.util.Scanner;

public class SwitchCaseTest {

	public static void main(String[] args) {

		Scanner scanner = new Scanner(System.in);
		int month = scanner.nextInt();
		int day;
		switch(month) {

				case 1: case 3: case 5: case 7: case 8: case 10: case 12:
					day = 31;
					break;
				case 2: 
					day = 28;
					break;
				
				case 4: 
					day = 30;
					break;
				
				case 6: 
					day = 31;
					break;
				
				
				case 9: 
					day = 30;
					break;
				
				case 11: 
					day = 20;
					break;
				
					default:
						System.out.println("존재하지 않는 달입니다.\n");
						day = -1;
				
				
		}
		System.out.println(month + "월은" + day + "일 입니다.");
		
	}

}
```

## JAVA 14부터 지원 되는 Switch 문법
- 간단하게 쉼표(,)로 조건 구분
- 식으로 표현하여 반환 값을 받을수 있음, 리턴 값이 없는 경우 오류 생김
- yield 키워드 사용

```java
package ch16;

public class SwitchCaseUpTest {

	public static void main(String[] args) {
		
		int month = 3;
		
		int day = switch (month) {
	    	case 1, 3, 5, 7, 8, 10,12 -> {
	    		System.out.println("한 달은 31일입니다."); 
	    		yield 31;
	    	}
	    	case 4,6,9,11 -> {
	    		System.out.println("한 달은 30일입니다."); 
	    		yield 30;
	    	}
	    	case 2 ->{
	    		System.out.println("한 달은 28일입니다.");
	    		yield 28;
	    	}
	    	default->{
	    		System.out.println("존재하지 않는 달 입니다."); 
	    		yield 0;
	    	}
		};
		System.out.println(month + "월은 " + day + "일입니다.");
	}
}


```
