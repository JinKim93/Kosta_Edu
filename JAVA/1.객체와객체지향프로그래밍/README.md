# 객체(Object)
### 학생,회원,주문,배송 등 -> 어떤 기능을 수행하는 데이터단위(명사)<br></br>

# 객체지향 vs 절차지향(c언어)
### ㅁ 절차지향 -> 시간이나 사건의 흐름에 따른 프로그래밍
### ex) 일어난다 -> 씻는다 -> 밥을 먹는다 -> 버스를탄다 -> 요금을지불한다 -> 학교도착
### ㅁ 객체지향

![image](https://user-images.githubusercontent.com/82345970/183837346-03052f29-60dc-4aa2-9fb1-9ba8d4420ea1.png)<br></br>

# 멤버변수
### Student클래스를 만들어 봄
### 1. 객체속성 -> 멤버변수 -> class 안에 선언한 변수
### 2. 객체의 속성은 멤버변수, 역할은 메서드로 구현
![image](https://user-images.githubusercontent.com/82345970/182526037-5b2f463c-23e5-4846-a44c-f09c5ac045cd.png)<br></br>

# 함수 vs 메서드(method)
### ㅁ 함수
### 1. 하나의 기능을 수행하는 일련코드
### 2. 어디 속해있지 않음 -> 단독모듈, 호출해서 씀<br></br>
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
### ㅁ 함수호출과 스택메모리

![image](https://user-images.githubusercontent.com/82345970/183844918-a3b7d701-b7ee-46ac-9d1c-617af82b90d1.png)<br></br>

### ㅁ 메서드
### 1. 객체의기능(역할)을 구현하기 위해 클래스 내부에 구현되는 함수
### 2. c++ : 멤버함수, 자바 : 메서드로 불림<br></br>

# 객체의속성은 멤버변수, 객체의기능은 메서드로 구현
```java
package ch04;

public class Student {
	
	//멤버변수 구현
	public int studentID;
	public String studentName;
	public String address;
	
	//메서드 구현 -> 학생정보 보여주는 메서드
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

### Student class를 사용하는(쓰는) 클래스 구현 -> main을포함한 StudentTest클래스 만듬
```java
package ch04;

//Student클래스를 사용하는 클래스임
public class StudentTest {

	public static void main(String[] args)
	{
		//Student클래스라는 데이터타입
		//new Student() -> 학생한명 생성 -> 이렇게 생성되는 studentLee를 인스턴스라고함
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

# 인스턴스생성과 힙 메모리
### 1. new 키워드 사용하여 인스턴스 생성
### 2. 클래스기반으로 생성된 객체(인스턴스)는 각각 다른 멤버 변수 값을 가지게 됨

![image](https://user-images.githubusercontent.com/82345970/183847518-8b3bd9c9-5293-477c-81de-a5c9d576bc8a.png)<br></br>

# 힙메모리

![image](https://user-images.githubusercontent.com/82345970/183847745-cd3c6336-caef-4de5-86b3-91264143cf6c.png)<br></br>

# 참조변수, 참조 값

![image](https://user-images.githubusercontent.com/82345970/183848877-ae5b5db8-a3c7-447d-b918-79a77902239b.png)<br></br>


# 용어정리
## ㅁ 객체
### 객체지향 프로그램의 대상, 생성된 인스턴스<br></br>

## ㅁ 클래스
### 객체를 프로그래밍 하기위해 코드로 정의해 놓은 상태<br></br>

## ㅁ 인스턴스
### new 키워드를 사용하여 클래스를 메모리에 생성한 상태
### 생성된 인스턴스는 동적메모리(힙 메모리)에 할당됨<br></br>

## ㅁ 멤버변수
### 클래스의 속성, 특성<br></br>

## ㅁ 메서드
### 멤버변수를 이용하여 클래스의 기능을 구현한 함수<br></br>

## ㅁ 참조변수
### 메모리에 생성된 인ㅅ느턴스를 가리키는 변수<br></br>

## ㅁ 참조 값
### 생성된 인스턴스의 메모리 주소 값<br></br>










