# JAVA

## 객체지향 VS 절차지향
### 절차지향 
- 시간이나 사건의 흐름
- 일어난다 -> 씻는다

### 객체지향
- 학생 <-> 밥 먹는다
- 학생 <-> 학교 간다


## 멤버변수
### 학생클래스 

- 객체의속성 ->  멤버변수
- 역할 ->  메서드로 구현

![image](https://user-images.githubusercontent.com/82345970/182526037-5b2f463c-23e5-4846-a44c-f09c5ac045cd.png)

## 함수정의호출
```java
package ch03;

public class FunctionTest {
	
	//반환해줄 데이터타입 int
	//매개변수 int num1, int num2 -> 매개변수 2개 받음
	//함수이름 addNum 
	public static int addNum(int num1, int num2 ) {
		
		int result;
		result = num1 + num2;
		return result;
		
	}
	//반환해줄값없음 -> void
	//매개변수 String greeting
	//함수이름 sayHello
	
	public static void sayHello(String greeting) {
		
		System.out.println(greeting);
		
	}
	//반환해줄 데이터타입 int
	//배개변수 없음
	//함수이름 calcSum
	public static int calcSum() {
		
		int sum = 0;
		int i;
		for(i = 0; i <=100; i++) {
			
			sum+= i;
			
		}
		return sum;
		
		
	}

	public static void main(String[] args) {
		
		int n1 = 10;
		int n2 = 20;
		
		int total = addNum(n1, n2); //addNum함수는 반환해줄값 있어서 total로 받아줌
		System.out.println(total);
		
		sayHello("안녕하세요");
		
		total = calcSum();
		System.out.println(total);
		
	}
}
```

## 함수 vs 메서드(method)
- 함수: 어디 속해있는게 아님, 단독모듈, 호출해서 쓰는것
- 메서드: 클래스 안에 속해있음, 클래스 멤버변수를 활용해서 구현되는게 메서드

## 메서드
- 객체지향에서는 클래스 안에 있는게 메서드다
- c++에서는 멤버함수로 부르고, 자바에서는 메서드라고 부른다
- 메서드를 구현함으로써 객체의기능이 구현 됨

## 객체의속성은 멤버변수, 객체의기능은 메서드로 구현

### 1. Student class 구현
```java
package ch04;

public class Student {
	
	//멤버변수 구현
	public int studentID;
	public String studentName;
	public String address;
	
	//메서드 구현 -> 학생정보보여주는 메서드
	public void showStudentInfo() {

		System.out.println(studentID + "학번 학생의 이름은" + studentName + "이고, 주소는" + address + "입니다");
	}
	
	//studentName 가져가는 메서드(get)
	//이름반환해줄거라서 String
	//메서드이름: getstudentName
	//studentName을반환해줌
	public String getStudentName() {
		
		return studentName;
		
	}
	
	//어떤이름으로 지정 또는 바꿔주는 메서드(set)
	//반환값은 없음 : void
	//어떤이름으로 바꿀건지 메개변수 있어야함
	public void setStudentName(String name) {
		
		//studentName에 들어온 매개변수 넣어줌
		studentName = name;
	}
	
}
```

### 2. Student class를 사용하는(쓰는) 클래스 구현 -> main을포함한 StudentTest클래스 만듬
```java
package ch04;

//Student클래스를 사용하는 클래스임
public class StudentTest {

	public static void main(String[] args)
	{
		//Student클래스라는 데이터타입
		//new Student() -> 학생한명생성 -> 이렇게 생성되는 studentLee를 인스턴스라고함
		//new Student() -> 생성자 -> Student하나를 생성해라
		//클래스를 기반으로 여러개의 인스턴스가 생성됨
		Student studentLee = new Student();
		
		studentLee.studentID = 12345;
		studentLee.setStudentName("Lee");
		studentLee.address = "서울 강남구";
		
		studentLee.showStudentInfo();
		
		Student studentKim = new Student();
		
		studentKim.studentID = 54321;
		studentKim.studentName = "Kim";
		studentKim.address ="경기도 성남시";
		
		studentKim.showStudentInfo();
		
	}
	
	
	
}
```
