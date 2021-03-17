# 2021.03.10 Day3

## EmployeeTest (클래스 생성)

* ```java
  package day3;
  
  //.java 파일 안에 여러개 클래스 가능
  // public 선언클래스명, main 메소드 가진 클래스명 으로 .java저장
  
  
  class Employee{//회사원 객체클래스
  	//사번 이름 직급 부서 변수
  	String id ;
  	String name ;
  	String title ;
  	String dept ;
  	
  	String work(){
  		System.out.println(name + "사원이 "+ dept + "부서에서 일한다.");
  		return "이달의 급여처리 업무 완료";
  	}
  	
  	
  }
	
  public class EmployeeTest {
  
  	public static void main(String[] args) {
  		//실행 문장 main 작성
  		Employee e1 = new Employee();
  	//   클래스명    변수명 = new 클래스명();
  		e1.id="100";
  		e1.name="박대리";
  		e1.title ="대리";
  		e1.dept= "인사부";
  		System.out.println(e1.id + ":" + e1.name + ":" + e1.title +":" + e1.dept);
  		
  		String result = e1.work();
  		System.out.println(result);
  		
  		Employee e2 = new Employee();
  		e2.id="200";
  		e2.name="최사원";
  		e2.title ="신입사원";
  		e2.dept= "it 개발부";
  		System.out.println(e2.id + ":" + e2.name + ":" + e2.title +":" + e2.dept);
  		e2.work();
  	}
  
  }
  ```
  
  ## ReturnTypeTest
  
  ```java
  package day3;
  
  class Test{
  	 int ma(){//메소드 정의
  		int i = 10;
  		return i*i; //ma() 실행후에 i*i의 결과 되돌려줌
  	}
  	 String mb(){
  		 String s = "java";
  		 return s.toUpperCase();
  	 }
  	 int[] mc(){
  		 int [] i = new int[3];
  		 i[0]=100;
  		 i[1]=200;
  		 i[2]=300;
  		 return i;
  	 }
  	void md(){
  		 int i =10;
  		 System.out.println(i*i);
  	 }
  	void me() {
  		int i=0;
  		System.out.println("me메소드시작");
  		if(i==0) {
  			return;
  		}
  		System.out.println("me메소드종료");
  	}
  }
  public class ReturnTypeTest {
  
  	public static void main(String[] args) {
  		Test t = new Test();
  		int r1 = t.ma();//메소드 호출 실행
  		System.out.println(r1);
  		String r2 = t.mb();
  		System.out.println(r2);
  		int[] r3 = t.mc();
  		for(int one:r3) {
  			System.out.println(one);
  		}
  		t.md();
  		t.me();
  		System.out.println("main 종료");
  	}
  
  }
  
  ```
  
  

