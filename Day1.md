# 2021.03.08 Day1

## Timeconversion

* ```java
  package day1;
  
  public class TimeConversion {
  
  	public static void main(String[] args) {
  		int time = 10000;// 초단위시간
  		//시분초단위 변경 출력
  		// 10000초는 xx 시간 xx분 xx초입니다.
  		
  		int a = time/3600;
  		int b = time%3600/60;
  		int c = time%3600%60;
  		
  		System.out.println(time + "초는" +a+"시간"+ b+"분" +c+"초입니다");
          String result = a>24?"만 1일 경과했습니다":"1일 이내입니다";
          System.out.println(result);
          	
  	}
  }
  ```

* VariableTest

  ```java
  package day1;
  
  public class VariableTest {
  
  	public static void main(String[] args) {
  		//int 최대값
  		//-2^31~2^31-1
          /*System.out.println(Integer.MAX_VALUE);//자바내장메소드
          System.out.println(Integer.MIN_VALUE);
          System.out.println(Byte.MAX_VALUE);//자바내장메소드
          System.out.println(Byte.MIN_VALUE);
  	*/
  		boolean b1 = true;
  		System.out.println("b1의 값은" + b1);
  		boolean b2 = 10 < 5;
  		System.out.println("b2의 값은" + b2);
  		char c1 = 'a';
  		System.out.println(c1);
  		char c2 = '9';
  		System.out.println(c2);
  		
  	}
  
  }
  ```

  

