# 객체(Object)
### 학생,회원,주문,배송 등 -> 어떤 기능을 수행하는 데이터단위(명사)

# 객체지향 vs 절차지향(c언어)
### ㅁ 절차지향 -> 시간이나 사건의 흐름에 따른 프로그래밍
### ex) 일어난다 -> 씻는다 -> 밥을 먹는다 -> 버스를탄다 -> 요금을지불한다 -> 학교도착
### ㅁ 객체지향

![image](https://user-images.githubusercontent.com/82345970/183837346-03052f29-60dc-4aa2-9fb1-9ba8d4420ea1.png)

# 멤버변수
### Student클래스를 만들어 봄
### 1. 객체속성 -> 멤버변수 -> class 안에 선언한 변수
### 2. 객체의 속성은 멤버변수, 역할은 메서드로 구현
![image](https://user-images.githubusercontent.com/82345970/182526037-5b2f463c-23e5-4846-a44c-f09c5ac045cd.png)


# 객체의속성은 멤버변수, 객체의기능은 메서드로 구현
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

### Student class를 사용하는(쓰는) 클래스 구현 -> main을포함한 StudentTest클래스 만듬
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

# 함수 vs 메서드(method)
### ㅁ 함수
### 1. 하나의 기능을 수행하는 일련코드
### 2. 어디 속해있지 않음 -> 단독모듈, 호출해서 씀<br></br>
### ㅁ 메서드
### 1. 클래스안에 속해있음, 클래스 멤버변수를 활요해서 구현하는게 메서드
### 2. 클래스 안에 있는게 메서드
### 3. 메서드를 구현함으로써 객체의기능(역할)구현됨
### 4. c++ : 멤버함수, 자바 : 메서드로 불림






