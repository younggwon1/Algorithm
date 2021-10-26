# 큐 (Queue)

<img src="https://user-images.githubusercontent.com/42603919/138870661-b7c8538f-0904-4ff5-a799-0d3898aaac61.PNG" alt="캡처" style="zoom:50%;" />

### 1. 큐 구조

- 줄을 서는 행위와 유사
- **가장 먼저 넣은 데이터를 가장 먼저 꺼낼 수 있는 구조**
  - 음식점에서 가장 먼저 줄은 선 사람이 가장 먼저 음식점에 입장하는 것과 동일
  - 선입선출 , FIFO (First In , First Out) 또는 LILO (Last In , Last Out) 방식으로 스택과 꺼내는 순서가 반대이다.
- 큐를 그럼 어디에 활용할까?
  - 시간 순으로 어떤 작업 또는 데이터를 처리할 필요가 있는 것들은 큐의 성질을 갖고 있다고 보면 된다. 또한 대표적으로 알고리즘에서는 BFS(너비 우선 탐색)에 사용된다.



### 2. 알아야할 용어

- Enqueue
  - 큐에 데이터를 넣는 기능
- Dequeue
  - 큐에서 데이터를 꺼내는 기능



### 3. JAVA에서의 큐 자료구조 사용하기

- 자바에서 제공하고 있는 큐는 정확히 말하자면 인터페이스에 불과하고, 큐를 구현하는 클래스는 크게 **PriorityQueue(우선순위 큐)**, **ArrayDeque(배열 양방향 큐)**, **LinkedList(연결리스트)** 이렇게 3가지가 있다.

- JAVA에서는 기본적으로 java.util 패키지에 Queue 클래스를 제공하고 있음
  - Enqueue에 해당하는 기능
    - Queue 클래스에서는 add(value) 또는 offer(value) 메서드를 제공함
  - Dequeue
    - Queue 클래스에서는 poll(value) 또는 remove(value) 메서드를 제공함
  - 아쉽게도, Queue 클래스에 데이터 생성을 위해서는 java.util 패키지에 있는 LinkedList 클래스를 사용해야한다.
    - LinkedList 클래스는 자료구조의 링크드리스트와 연관이 있다.

````java
// Queue를 사용하기 위해 LinkedList 클래스를 사용한다.
import java.util.LinkedList;
import java.util.Queue;

// 자료형 매개변수를 넣어서, 큐에 들어갈 데이터의 타입을 지정해야함.
Queue<Integer> queue_int = new LinkedList<Integer>();
Queue<String> queue_str = new LinkedList<String>();
````

https://st-lab.tistory.com/181?category=856997

<img src="https://user-images.githubusercontent.com/42603919/138870045-b56c1b7c-50e7-4393-bca1-d3b50021ef8d.PNG" alt="캡처" style="zoom: 50%;" />

> offer() 의 경우 리스트에서의 add() 와 비슷한 역할이고, poll() 의 경우는 remove() 와 비슷한 역할이며, peek() 은 element() 와 비슷한 역할이다.
>
>  
>
> 다만 차이점은 add(), remove(), element()는 내부적으로 예외를 처리하고 있다. 예로들어 index 밖을 넘어가거나, 삭제할 요소가 없거나 등등 이러한 예외적 경우에 대해 예외를 던졌다.
>
>  
>
> 하지만 offer(), peek(), element()의 경우 예외를 던지는 것이 아닌 특별한 값을 던지는데, 일반적으로 null 또는 false를 던진다고 생각하면 된다.



- 데이터 추가는 add(value) 또는 offer(value)를 사용

````java
// 데이터 추가는 add(value) 또는 offer(value)를 사용
queue_int.add(1);
queue_int.offer(2);

// => 출력에 true라고 출력되는 부분은 offer(value) 메서드가 리턴한 값(성공)으로 , 셀의 맨 마지막에 함수를 넣을 경우, 변수가 변수값이 출력되는 것 처럼 함수는 함수 리턴값이 출력되는 것이다.
````



- Queue 인스턴스를 출력하면, 해당 큐에 들어있는 아이템 리스트가 출력됨

````java
// Queue 인스턴스를 출력하면, 해당 큐에 들어있는 아이템 리스트가 출력됨
System.out.println(queue_int);

=> [1,2]
````



- poll() , remove()는 큐의 첫번째 값 반환, 해당 값은 큐에서 삭제

````java
// poll()은 큐의 첫번째 값 반환, 해당 값은 큐에서 삭제

queue_int.poll();
=> 1
 
    
// 큐의 아이템을 확인해보면, poll()을 통해 반환된 값은 삭제되었음을 알 수 있다.
queue_int
=> [2]
    
// poll()과 마찬가지로 반환된 값은 삭제되었음을 알 수 있다.
queue_int.remove();
=> 2
    
// 큐의 아이템을 확인해보면, remove()을 통해 반환된 값은 삭제되었음을 알 수 있다.
queue_int
=> []
````



### 4. 프로그래밍 연습

![캡처](https://user-images.githubusercontent.com/42603919/138868262-2c9b9885-ff06-44f8-bfbb-250ec50396f9.PNG)

```java
package AIngang;

import java.util.ArrayList;
import java.util.Scanner;

public class MyQueue<T> {
    private ArrayList<T> queue = new ArrayList<T>();

    public void enqueue(T item) {
        queue.add(item);
    }

    public T dequeue() {
        if(queue.isEmpty()) {
            return null;
        }
        return queue.remove(0);
    }

    public boolean isEmpty() {
        return queue.isEmpty();
    }

    public static void main(String[] args) {
        MyQueue<Integer> mq = new MyQueue<Integer>();
        mq.enqueue(1);
        mq.enqueue(2);
        mq.enqueue(3);
        System.out.println(mq.dequeue());
        System.out.println(mq.dequeue());
        System.out.println(mq.dequeue());
    }
}
```