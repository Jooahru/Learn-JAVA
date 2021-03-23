## Overloading

```java
class A{
    int add(int i, int j){return i+j;}
    String add(String i, String j){return i+j}
    void add(double i, double j){}
    void add(Object o1,Object o2){o1.toString()+o2.toString();}
    void add(Object o1){o1.toString();}
   //잘못된 오버로딩 void add(int a,int b){a+b;} 첫번째 줄과 중복
    void add(){}
   //잘못된 오버로딩 int add(){return 0;} 윗줄과 리턴타입 달라도 중복
}===> 메소드 overloading
    1개 클래스/ 같은 이름 메소드 여러개/ 매개변수(갯수나 타입이나 순서) 다르게 정의/
    리턴타입이나 modifier 상관없다
```

### 비정형 매개변수

```java
main
a1.add(정수 타입 정하고/ 갯수 정하지 않고)
    ====> 비정형 매개변수 형태
    
    class A{
        add(int... numbers){
            numbers==> int[]
        }
    }
```

### Sigleton dao dto

* DAO = data Access Object 클래스
  * 데이터직접 접근 객체 = 파일 입출력/DB입출력
* DTO = Data Transfer Object 클래스
* VO = Value Object 클래스
* DO = Data Object 클래스
  * EmployeeDTO=EmployeeVO=EmployeeDO 임시저장소

 사원등록 --> 등록 필요한 데이터 입력 -->Controller-->ManagerDAO

--->ManagerVO ---> 저장



#### 주아루 짱짱맨

* Jooah!