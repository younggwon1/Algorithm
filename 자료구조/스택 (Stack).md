# 스택 (Stack)

- 데이터를 제한적으로 접근할 수 있는 구조

  - 한쪽 끝에서만 자료를 넣거나 뺄 수 있는 구조

- 가장 나중에 쌓은 데이터를 가장 먼저 빼낼 수 있는 데이터 구조

  - 즉, 상자에 물건을 쌓아 올리듯이 데이터를 쌓는 자료구조이다.

  - 큐 : FIFO 정책
  - 스택 : LIFO 정책

- 그래프의 깊이 우선 탐색(DFS)에서 사용

- 재귀적 함수를 호출할 때 사용



![캡처](https://user-images.githubusercontent.com/42603919/139832665-cd23db09-2dbc-4b0e-9707-4c4424d97b36.PNG)



---



### 1. 스택 구조

- **스택은 LIFO(Last In , First Out)** 또는 FILO(First In Last Out) 데이터 관리 방식을 따른다.
- 대표적인 스택의 활용
  - 컴퓨터 내부의 프로세스 구조의 함수 동작 방식
- 주요 기능
  - **push()** 
    - 데이터를 스택에 넣기
  - **pop()**
    - 데이터를 스택에서 꺼내기



### 2. 자료구조 스택의 장단점

- 장점
  - 구조가 단순해서, 구현하기 쉽다.
  - 데이터 저장/읽기 속도가 빠르다.
- 단점(일반적인 스택 구현시)
  - 데이터 최대 갯수를 미리 정해야한다.
  - 저장 공간의 낭비가 발생할 수 있다.
    - 미리 최대 갯수만큼 저장 공간을 확보해야함

> => 스택은 단순하고 빠른 성능을 위해 사용되므로, 보통 배열 구조를 활용해서 구현하는 것이 일반적이다. 이 경우, 위에서 언급한 단점이 있을 수 있다.





### 3. JAVA 에서의 스택 자료구조 사용하기

- JAVA Stack 클래스
  - java.util 패키지에서 Stack 클래스 제공
    - push(item) 메서드
      - item을 Stack에 추가
    - pop() 메서드
      - Stack에서 마지막에 넣은 item을 리턴하고, 해당 아이템은 Stack에서 삭제
    - peek() 메서드
      - stack의 가장 상단의 값 출력



````java
// java.util Stack 클래서 import
import java.util.Stack

// 자료형 매개변수를 넣어서, 스택에 들어갈 데이터의 타입을 지정해야함
Stack<integer> stack_int = new Stack<integer>(); // INT형 스택 선언
Stack<String> stack_int = new Stack<String>(); // String형 스택 선언
````



- push()

````java
stack_int.push(1);
stack_int.push(2);
stack_int.push(3);
````



- pop()

````java
stack_int.pop();

=> 3
    
stack_int.pop();

=> 2
    
stack_int.pop();

=> 1
````





### 4. 프로그래밍 연습

![캡처](https://user-images.githubusercontent.com/42603919/139829511-6e464ba7-9cfb-47c1-a6d2-f85851b9efed.PNG)



````java
package AIngang;

import java.util.ArrayList;

public class MyStack<T> {
	private ArrayList<T> stack = new ArrayList<T>();
	
	public void push(T item) {
		stack.add(item);
	}
	
	public T pop() {
		if(stack.isEmpty()) {
            return null;
        }
		return stack.remove(stack.size()-1);
	}
	
    public boolean isEmpty() {
        return stack.isEmpty();
    }
	
	public static void main(String[] args) {
		MyStack<Integer> ms = new MyStack<Integer>();
		ms.push(1);
		ms.push(2);
		ms.push(3);
		
		System.out.println(ms.pop());
		System.out.println(ms.pop());
		System.out.println(ms.pop());
	}
}
````



[Java 스택(Stack) 클래스 정리](https://velog.io/@lshjh4848/Java-%EC%8A%A4%ED%83%9DStack-%ED%81%B4%EB%9E%98%EC%8A%A4-%EC%A0%95%EB%A6%AC)



