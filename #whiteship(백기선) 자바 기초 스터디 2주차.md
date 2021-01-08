

<h1>#whiteship(백기선) 자바 기초 스터디 2주차</h1>



- 자바의 데이터 타입
  - 프리미티브 타입 ( Primitive type )
  - 레퍼런스 타입 ( Reference type )



<h2>프리미티브 타입 종류와 값의 범위, 기본 값</h2>



|        | 타입             | 할당되는 메모리 크기 | 기본 값  |                    데이터 표현 범위                    |
| ------ | ---------------- | :------------------: | -------- | :----------------------------------------------------: |
| 논리형 | boolean          |    1 byte (8bit)     | false    |                      true, false                       |
| 정수형 | byte             |        1 byte        | 0        |                       -128 ~ 127                       |
| ""     | short            |        2 byte        | 0        |                    -32,768 ~ 32,767                    |
| ""     | **int(기본)**    |      **4 byte**      | 0        |             -2,147,483,648 ~ 2,147,483,647             |
| ""     | long             |        8 byte        | 0L       | -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807 |
| 실수형 | float            |        4 byte        | 0.0F     |         (3.4 X 10-38) ~ (3.4 X 1038) 의 근사값         |
| ""     | **double(기본)** |      **8 byte**      | 0.0      |        (1.7 X 10-308) ~ (1.7 X 10308) 의 근사값        |
| 문자형 | char             |  2 byte (유니코드)   | '\u0000' |                       0 ~ 65,535                       |



<h2>레퍼런스 타입 종류와 값의 범위, 기본 값</h2>

- 기본형 타입을 제외한 모든 타입
- 빈 객체를 의미하는 Null이 존재
- 값이 저장되어 있는 곳의 **주소값**을 저장하는 공간으로 **힙(Heap)** 메모리에 저장
- 문법상 에러가 없지만 실행시켰을 때 에러가 나는 런타임 에러가 발생



| 타입                  | 예시                                                       | 기본 값 | 할당되는 메모리 크기    |
| --------------------- | ---------------------------------------------------------- | ------- | ----------------------- |
| 배열(Array)           | int[] arr = new int[5];                                    | Null    | 4 byte (객체의 주소 값) |
| 열거(Enumeration)     |                                                            | Null    | 4 byte (객체의 주소 값) |
| 클래스(Class)         | String str = "test";<br />Student yunhwan = new Student(); | Null    | 4 byte (객체의 주소 값) |
| 인터페이스(Interface) |                                                            | Null    | 4 byte (객체의 주소 값) |



<h2>리터럴</h2>

- 컴퓨터 과학 분야에서 리터럴이란, 소스 코드의 고정된 값을 대표하는 용어

- 고정된 값은 숫자, 문자, 함수 등 더이상 나눌 수 없는 명확한 데이터 표현 값

- ```java
  // 정수
  int v1 = 0b10	// 0b -> 2진수
  int v2 = 010	// 0 -> 8진수
  int v3 = 10
  int v4 = 0x10	// 0x-> 16진수
  long long_v1 = 10L	// l또는 L -> long 타입 리터럴 
  
  // 실수
  float float_v1 = 1.234F;	//f또는 F 선언
  double v1 = 1.234;
  double v2 = 1.234d;	//d또는 D 선언 해주어도 되고 안해주어도 됨
  double v3 = 1234E-3d;
  
  // 문자
  char v1 = 'C';
  char v2 = '민';
  char v3 = '\u1234'	// 백슬러시 u다음 4자리 16진수 유니코드
      
  // 부울
  boolean v1 = true;
  boolean v2 = 12 > 34;
  
  //문자열
  String v1 = "hello";
  ```



<h2>변수 선언 및 초기화</h2>

- 변수의 타입(자료형) 다음에 변수의 이름을 작성

- ```java
  public class test{
      public static void main(String[] args){
          int value1;
          int value2, value3;
  
          // 초기화
          int value = 10;
          int value2;
          value2 = 20;
      }
  }
  ```



<h2>변수의 스코프와 라이프타임</h2>

- 그 변수에 접근할 수 있는 범위

- 자바 언어는 블록 스코프를 사용 ( 중괄호 {} )

- ```java
  public class test{
      static int temp = 10;
      public static void main(String[] args){
          System.out.println(temp); //10
      }
  }
  ```

- ```java
  public class test{
      static int temp = 10;
      public static void main(String[] args){
          int temp = 20;
          System.out.println(temp); //20
      }
  }
  ```

- 레퍼런스 타입의 변수의 라이프 타임은 쓰레기 수집기(GC : Garbage Collector)와 관련이 있다.

- GC는 가비지 컬렉션 힙 영역에 존재하는 참조 타입 변수의 객체에 대해 동작

- 힙 영역의 메모리가 부족할 경우 GC가 이 영역을 스캔하고, 참조 되고 있지 않은 객체를 제거

- ```java
  public class test{
      public static void main(String[] args){
          // 런타임 스택 영역에 mt변수가 생성, 
          // 그 값은 가비지 컬렉션 힙 영역에 생성 된 new MyTest()로 만들어진 주소값을 가지고 있다.
          MyTest mt = new MyTest(); 
          
          //null을 할당하면, 더 이상 아무도 참조하지 않아 GC의 대상이 된다.
  		mt = null
      }
  }
  class MyTest{..}
  ```

- 런타임 스택 영역에 생성된 변수의 라이프 타임은 블록 스코프에 의존적 즉, 블록 내에서 선언된 변수는 블록이 종료될 때 런타임 스택 영역에서 함께 소멸



<h2>타입 변환, 캐스팅 그리고 타입 프로모션</h2>

1. 자신의 표현 범위를 모두 포함한 데이터 타입으로의 변환 (**타입 프로모션**)
2. 자신의 표현 범위를 모두 포함하지 못한 데이터 타입으로의 변환 (**타입 캐스팅**)

```java
public class test{
    public static void main(String[] args){
        float f_V1 = 1.23f;
        long l_v1 = f_v1;
        //오류 : Type mismatch (타입 캐스팅 발생)
        
        float f_V1 = 1.23f;
        long l_v1 = (long)f_v1;
        //오류는 나지 않지만 데이터 손실
    }
}
```



<h2>1차, 2차 배열 선언</h2>

배열 : 동일한 자료형을 정해진 수만큼 저장하는 순서를 가진 레퍼런스 타입 자료형



- <h4>1차원 배열</h4>

```java
// 1. 선언 방법
public class test{
    public static void main(String[] args){
        int[] test1;
        int test2[];
        
        test1 = {10,20,30,40,50}; // 오류 : Array constants can only be used in initializers
    }
}

// 2. 값 할당 방법
public class test{
    public static void main(String[] args){
        int[] test1 = new int[5];
		int[] test2 = {10,20,30,40,50};
        int[] test3 = new int[]{10,20,30,40,50};
    }
}
```

- 선언한 배열 **변수**는 **JVM의 런타임 스택 영역**에 생성
- 레퍼런스 타입이기 때문에 **값**은 **가비지 컬렉션 힙 영역**에 객체가 생성



- <h4>2차원 배열</h4>

```java
// 1. 선언 방법
public class test{
    public static void main(String[] args){
        int[][] test1;
        int test2[][];
    }
}

// 2. 값 할당 방법
public class test{
    public static void main(String[] args){
        int[][] test1 = new int[2][3];
		int[][] test2 = {{1,2}, {3,4,5}};
        int[][] test3 = new int[][]{{1,2},{3,4,5}};
    }
}
```



<h2>타입 추론, var</h2>

- 값을 보고 컴파일러가 데이터 타입이 무엇인지 추론

- ex) javascript는 모든 변수를 var, let, const등을 사용해 선언

- 대표적으로 제네릭에서 볼 수 있음

- ```java
  public class test{
      public static void main(String[] args){
          HashMap<String, Integer> hm = new HashMap<>();
      }
  }
  ```

- var로 사용할 경우 제약 사항

  - 로컬 변수이면서, 선언과 동시에 값이 할당 되어야 함