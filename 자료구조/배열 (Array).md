# 배열 (Array)

### 1. 배열은 왜 필요할까?

- 같은 종류(동일한 자료형)의 데이터를 효율적으로 관리하기 위해 사용
- 같은 종류의 데이터를 순차적으로 저장
- 장점
  - 빠른 접근 가능
    - 첫 데이터의 위치에서 상대적인 위치로 데이터 접근(**인덱스 번호로 접근**)
- 단점
  - 데이터 추가/삭제의 어려움
    - 미리 최대 길이를 지정해야함 (배열은 길이가 정해져있다.)

---

#### 참고 : Primitive 자료형과 Wrapper 클래스

[자바 자료형 정리(Java Data Type)](https://jdm.kr/blog/213)

[래퍼 클래스란(Wrapper Class)?](https://coding-factory.tistory.com/547)

<img src="https://user-images.githubusercontent.com/42603919/138682769-9566ad14-10e6-4289-9d08-52239a088be2.PNG" alt="캡처" style="zoom:50%;" />

- Java에서는 int와 Integer 같이, Primitive 자료형과 Wrapper 클래스가 있음
- **주로 Wrapper 클래스 사용할 것이다!!** (필요시에만 Primitive 자료형 사용)
  - null을 용이하게 처리할 수 있다.
  - ArrayList등 객체만을 핸들링 하는 기능을 사용할 수 있다.

---



### 2. Java와 배열

- Java에서는 기본문법으로 배열 지원
  - 1차원 배열은 [] 를 통해 선언할 수 있다.
  - 각 아이템은 {} 내에 콤마로 작성



##### new 키워드를 사용해서, 배열을 미리 선언하고, 데이터를 넣을 수 있음

<img src="https://user-images.githubusercontent.com/42603919/138689261-5ce39435-bd1f-4332-a374-ead264f9b19b.PNG" alt="캡처" style="zoom:67%;" />

````java
Integer[] data_list = new Integer[10];

data_list[0] = 1;
data_list[1] = 2;
````



##### 직접 배열 데이터 선언시 넣을 수 있음

- 데이터들의 값을 알고 있을 때 사용하면 편리

<img src="https://user-images.githubusercontent.com/42603919/138689104-8c40f097-9f16-4e7b-91c1-41db355aae44.PNG" alt="캡처" style="zoom:67%;" />

````java
Integer data_list1[] = {5,4,3,2,1};
Integer[] data_list2 = {1,2,3,4,5};
````

 

#### Java에서 배열을 보다 손쉽게 다루기 위한 *클래스*등을 제공

- 예 : **Arrays 클래스를 활용**하여, 전체 데이터 출력하기

**단순 배열 변수를 출력**하면 메모리 주소값이 출력된다.

````java
Integer[] data_list2 = {1,2,3,4,5};
System.out.println(data_list2); // ??

=> [I@762efe5d : 메모리 주소값이 출력된다.
````



따라서 **배열을 출력**하기 위해서는 **반복문을 사용하거나, 메소드를 사용**해야한다.

1. 반복문

````java
import java.util.Arrays;

Integer[] data_list2 = {1,2,3,4,5};

for (int i = 0; i < data_list2.length; i++) {
	System.out.println(data_list2[i]);
}

=> 
1
2
3
4
5
````



2. 메소드 사용

배열에 정의된 값들을 문자열 형태로 만들어서 리턴해준다.

````java
import java.util.Arrays;

// 배열의 내용을 출력하려면, Arrays.toString(배열변수) 메서드를 사용하면 된다.
System.out.println(Arrays.toString(data_list2));
[1,2,3,4,5]
````



#### Java에서 배열을 보다 손쉽게 다루기 위한 ArrayList 클래스 예

- 배열은 고정된 크기를 가지고있다 -> 따라서 얼마든지 **배열의 크기를 가변적**으로 다룰 수 있는 기능을 제공하는 것 => **ArrayList** 라고한다.!!



---

#### 참고 : List와 ArrayList

[Java 리스트(List) 컬렉션 종류 ArrayList, Vector, LinkedList](https://lelecoder.com/78)

- List , ArrayList 선언의 차이점

  - 하기 내용에 대해서 둘 다 가능

  ````
  List<Integer> list1 = new ArrayList<Integer>();
  ArrayList<Integer> list2 = new ArrayList<Integer>();
  ````

- List는 인터페이스이고, ArrayList는 클래스이다.

---



##### add() , get()

- add() : 배열에 아이템 추가시 add(아이템) 메서드를 사용
- get() : 배열에 특정 아이템을 읽을 시 get(인덱스 번호) 메서드 사용

````java
import java.util.ArrayList;

// int형 데이터를 담을 수 있는 가변 길이의 배열을 선언
ArrayList<Integer> list1 = new ArrayList<Integer>();

list1.add(1); //배열에 아이템 추가시 add(아이템) 메서드를 사용
list1.add(2);
list1.get(0); // 배열에 특정 아이템을 읽을 시 get(인덱스 번호) 메서드 사용 (굳이 System.out.println()을 사용하지 않아도 된다.)

=> 1
````



##### set()

- set() : 특정 인덱스에 해당하는 아이템 변경 시, set(인덱스 번호, 변경할 값) 메서드 사용 

````java
list1.set(0, 5); // 특정 인덱스에 해당하는 아이템 변경 시, set(인덱스 번호, 변경할 값) 메서드 사용 

list1.get(0);

=> 5
````



##### remove()

- remove() : 특정 인덱스에 해당하는 아이템 삭제 시, remove(인덱스 번호) 메서드 사용

````java
list1.remove(0); // 특정 인덱스에 해당하는 아이템 삭제 시, remove(인덱스 번호) 메서드 사용

list1.get(0);

=> 2
````



##### size()

- size() : 배열의 길이 확인하기

````java
list1.size();

=> 1
````



#### 다차원 배열

https://m.blog.naver.com/heartflow89/220950845259

````java
// 2차원 배열
Integer data_list2[][] = {{1,2,3} , {4,5,6}}

// 3차원 배열
Integer data_list3[][] = {
							{
								{1,2,3}, 
								{4,5,6}
							},
							{
								{7,8,9}, 
								{10,11,12}
							}
						  }
````



---

#### 참고

- **배열.length** : 배열에 들어있는 아이템 개수
- **문자열.indexOf(String key)** : 문자 key가 해당 문자열에 있으면 해당 문자의 위치 index 값을 리턴하고, 없으면 -1을 리턴한다.

---