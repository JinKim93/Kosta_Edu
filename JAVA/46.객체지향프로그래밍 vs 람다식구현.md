# 객제지향프로그래밍과 람다식 비교
### 문자열 두개를 연결하여 출력하는 예제를 두 가지 방식으로 구현

## 객체지향프로그래밍으로 구현
### 1. StringConcat 인터페이스 생성
```java
package ch04;

public interface StringConcat {
	
	public void makeString(String s1, String s2);

}
```

### 2. StringConcatImpl 클래스 생성
```java
package ch04;

public class StringConcatImpl implements StringConcat{

	@Override
	public void makeString(String s1, String s2) {

		System.out.println(s1 + "," + s2);
	}

}
```

### 3. StringConcatTest 클래스 생성 -> 호출 및 출력
```java
package ch04;

public class StringConcatTest {

	public static void main(String[] args) {

		StringConcatImpl strImpl = new StringConcatImpl();
		strImpl.makeString("Hello", "World ");
	}

}
```

## 람다식으로 표현
### 1. StringConcat 인터페이스생성 -> 함수형인터페이스
```java
package ch04;

@FunctionalInterface
public interface StringConcat {
	
	public void makeString(String s1, String s2);

}
```

### 2. StringConcatTest 클래스 생성 -> 람다식 구현 및 호출 
```java
package ch04;

public class StringConcatTest {

	public static void main(String[] args) {
		
		String s1 = "Hello";
		String s2 = "World";

		StringConcatImpl strImpl = new StringConcatImpl();
		strImpl.makeString(s1, s2);
		
		StringConcat concat = (s,v) -> System.out.println(s + "," + v);
		concat.makeString(s1, s2);
		
		//클래스 없이 람다식을 쓸수있는게 아니라, 내부적으로 익명클래스가 만들어짐
		StringConcat concat2 = new StringConcat() {
			
			@Override
			public void makeString(String s1, String s2) {
				
				//StringConcat concat = (s,v) -> System.out.println(s + "," + v); 이부분이 
				//익명클래스로 만들어짐
				System.out.println(s1 + "....." + s2);
				
			}
		};
		concat2.makeString(s1, s2);

	}

}
```
