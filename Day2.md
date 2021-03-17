# 2021.03.09 Day2

## ArrayTest

* ```java
  package day2;
  
  import java.text.DecimalFormat;
  
  public class ArrayTest {
  
  	public static void main(String[] args) {
  		//5명의 학생 시험점수
  		String names[] = new String[5];
  		int [][]scores;//배열선언
  		scores = new int[names.length][3]; //배열생성
  		//int []scores = new int[5]로해도 똑같다
  		double avg [] = new double[names.length];
  		names[0]= "홍미미";
  		names[1]= "이민정";
  		names[2]= "서형준";
  		names[3]= "김범근";
  		names[4]= "김우일";
  		
  		for(int i=0;i<scores.length;i++) {
			System.out.print(names[i]+"\t");
  			int sum=0;
  			for(int j=0;j<scores[i].length;j++)
  			{
  				scores[i][j] = (int)(Math.random()*100+1);
  				sum += scores[i][j];
  				System.out.print(  scores[i][j] + "\t");
  			}
  			avg[i] = (double)sum/ scores[i].length;
  			java.text.DecimalFormat dec = new DecimalFormat("##.00");
  			// 소수점 둘째짜리까지 보는 코드 (.00 붙이면 40.00 나옴 .##은 소수점 .00생략)
  			System.out.print( dec.format(avg[i]));
  			System.out.println();
  		}
             //names 배열 - 5명 학생이름 저장 상태
  		   //배열 10개로 증가하고싶을때
  		   String []names2 = new String[10];
  		   for(int i=0; i<names.length;i++)
  		   {
  			   names2[i] = names[i];
  		   }
  		   for(int i=0; i<names2.length;i++)
  		   {
  			   System.out.println(names2[i]);
  		   }
  		   //for 또다른 방법(jdk 1.5 추가)
  		   for(String n : names2) {
  			   System.out.println(n);
  		   }
  	}
  
  }
  ```
  
  ## ForTest
  
  ```java
  package day2;
  
  public class ForTest {
  
  	public static void main(String[] args) {
  		
  		int i=0;
  		int sum=0;
  		/*for(i=1;i<=10;i++)
  		{
  			System.out.println((int)(Math.random()*101));
  		}
  */
  		for(i=1; i<=10; i++)
  		{
  			if(i==5) {break;}
  			sum=sum+i;
  			System.out.println(i+"값까지의 정수 총합="+sum);
  		}
  	}
  }
  
  ```
  
  

