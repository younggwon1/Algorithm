# 힙 (heap)

### 1. 힙 (Heap) 이란?

- **Heap**: **데이터에서 <u>최대값과 최소값을 빠르게 찾기 위해</u> 고안된 <u>완전 이진 트리</u>**(Complete Binary Tree)

- **완전 이진 트리** : **노드를 삽입할 때 최하단 왼쪽 노드부터 차례대로 삽입하는 트리**

  - 즉, 완전 이진 트리는 이진 트리에서 두 가지 조건을 더 만족해야한다.

    1. 마지막 레벨을 제외한 모든 노드가 채워져있어야함

    2. 모든 노드들은 왼쪽부터 채워져있어야함 

<img src="https://user-images.githubusercontent.com/42603919/143730023-61a4d180-9248-4513-8bf2-70b18f3a9e8a.PNG" alt="캡처" style="zoom:67%;" />



- **Heap**을 사용하는 이유
  - 배열에 데이터를 넣고, 최대값과 최소값을 찾으려면 O(n) 이 걸림
  - 이에 반해, **Heap**에 데이터를 넣고, **최대값과 최소값을 찾으면, <u>O(log n)</u>** 이 걸림
  - 우선순위 큐와 같이 **최대값 또는 최소값을 빠르게 찾아야 하는 자료구조 및 알고리즘 구현 등에 활용**됨
    -  **'우선순위 큐'가 바로 힙 자료구조를 이용하여 구현되기 때문**



### 2. 힙 (Heap) 구조

- **Heap**은 최대값을 구하기 위한 구조 (최대 힙, Max Heap) 와, 최소값을 구하기 위한 구조 (최소 힙, Min Heap) 로 분류할 수 있음

- **Heap**은 다음과 같이 두 가지 조건을 가지고 있는 자료구조임

  1. 형태

     - **최대 힙 ( Max Heap )**
       - 각 노드의 값은 해당 노드의 자식 노드가 가진 값보다 크거나 같음
       - 부모 노드의 값(key 값) ≥ 자식 노드의 값(key 값)

     - **최소 힙 ( Min Heap )**
       - 각 노드의 값은 해당 노드의 자식 노드가 가진 값보다 작거나 같음
       - 부모 노드의 값(key 값) ≤ 자식 노드의 값(key 값)

  2. 완전 이진 트리 형태를 가짐



#### 힙과 이진 탐색 트리의 공통점과 차이점

- 공통점: 힙과 이진 탐색 트리는 모두 **이진 트리**임

- 차이점: 

  - **힙**은 그냥 **왼쪽부터 노드를 추가( 크기에 상관 없이 )하는 것**이고,
  - **이진 탐색 트리**는 **왼쪽 노드에는 부모 노드 값보다 작은 노드가 추가되고 오른쪽에는 부모 노드 값보다 큰 노드가 추가**된다.

  - 힙은 각 노드의 값이 자식 노드보다 크거나 같음(Max Heap의 경우)
  - 이진 탐색 트리는 왼쪽 자식 노드의 값이 가장 작고, 그 다음 부모 노드, 그 다음 오른쪽 자식 노드 값이 가장 큼
  - 힙은 이진 탐색 트리의 조건인 자식 노드에서 작은 값은 왼쪽, 큰 값은 오른쪽이라는 조건은 없음
    - 힙의 왼쪽 및 오른쪽 자식 노드의 값은 오른쪽이 클 수도 있고, 왼쪽이 클 수도 있음

- **이진 탐색 트리는 탐색을 위한 구조, 힙은 최대/최소값 검색을 위한 구조 중 하나로 이해하면 됨**  

<img src="https://user-images.githubusercontent.com/42603919/143730056-70d107b5-4f5a-4165-9a49-ad71de833749.PNG" alt="캡처" style="zoom:67%;" />





### 3. 힙 (Heap) 동작

- 데이터를 힙 구조에 삽입, 삭제하는 과정을 그림을 통해 선명하게 이해하기



#### 힙에 데이터 삽입하기 - 기본 동작

- Heap은 완전 이진 트리이므로, 삽입할 노드는 기본적으로 **왼쪽 최하단부 노드부터 채워지는 형태로 삽입**

<img src="https://user-images.githubusercontent.com/42603919/143730329-dda4ca4a-1af9-4fa7-8135-f71fa67b12a8.PNG" alt="캡처" style="zoom:50%;" />



#### 힙에 데이터 삽입하기 - 삽입할 데이터가 힙의 데이터보다 클 경우 (<u>Max Heap</u> 의 예)

- 먼저 삽입된 데이터는 완전 이진 트리 구조에 맞추어, 최하단부 왼쪽 노드부터 채워짐

- 채워진 노드 위치에서, 부모 노드보다 값이 클 경우, 부모 노드와 위치를 바꿔주는 작업을 반복함 (swap)

<img src="https://user-images.githubusercontent.com/42603919/143730342-b1c51b1b-cc6b-40c7-9287-eb067f062549.PNG" alt="캡처" style="zoom:50%;" />



#### 힙의 데이터 삭제하기 (<u>Max Heap</u> 의 예)

- **보통 삭제는 최상단 노드 (root 노드)를 삭제하는 것이 일반적임**
  - 힙의 용도는 최대값 또는 최소값을 root 노드에 놓아서, 최대값과 최소값을 바로 꺼내 쓸 수 있도록 하는 것임

- 상단의 데이터 삭제시, 가장 최하단부 왼쪽에 위치한 노드 (일반적으로 가장 마지막에 추가한 노드) 를 root 노드로 이동

- root 노드의 값이 child node 보다 작을 경우, root 노드의 child node 중 가장 큰 값을 가진 노드와 root 노드 위치를 바꿔주는 작업을 반복함 (swap)



<img src="https://user-images.githubusercontent.com/42603919/143730348-b6b051aa-e581-4f6f-93d2-75eb5d232ca5.PNG" alt="캡처" style="zoom:50%;" />





### 4. 힙 구현

#### 힙과 배열

- 일반적으로 **힙 구현시 배열 자료구조를 활용**함

- 배열은 인덱스가 0번부터 시작하지만, **힙 구현의 편의를 위해, root 노드 인덱스 번호를 1로 지정하면, 구현이 좀더 수월함**

  - 0 인덱스의 값은 null로 둔다.

  - 부모 노드 인덱스 번호 (parent node's index) = 자식 노드 인덱스 번호 (child node's index) / 2
    - JAVA 에서는 / 연산자로 **몫**을 구할 수 있음 

- 왼쪽 자식 노드 인덱스 번호 (left child node's index) = 부모 노드 인덱스 번호 (parent node's index) * 2

- 오른쪽 자식 노드 인덱스 번호 (right child node's index) = 부모 노드 인덱스 번호 (parent node's index) * 2 + 1

<img src="https://user-images.githubusercontent.com/42603919/143730744-987b9fcf-4691-4e52-a074-e5821e786ee1.PNG" alt="캡처" style="zoom:50%;" />



#### 힙에 데이터 삽입 구현 (Max Heap 예)

##### 힙 클래스 구현1

- **import java.util.ArrayList** 를 활용해서 구현

  ````java
  import java.util.ArrayList;
  
  public class Heap {
      public ArrayList<Integer> heapArray = null;
      
      public Heap (Integer data) {
          heapArray = new ArrayList<Integer>();
          
          // 0 인덱스 번호는 null로 설정
          heapArray.add(null);
          heapArray.add(data);
      }
  }
  ````

  ````java
  Heap heapTest = new Heap(1);
  System.out.println(heapTest.heapArray);
  
  => [null, 1]
  ````



##### 힙 클래스 구현2 - insert1

- **인덱스 번호는 1번부터 시작**하도록 변경

<img src="https://user-images.githubusercontent.com/42603919/143730920-650b42dc-185e-4946-8d7c-b4ea84969043.PNG" alt="캡처" style="zoom:50%;" />

````java
import java.util.ArrayList;

public class Heap {
    public ArrayList<Integer> heapArray = null;
    
    public Heap (Integer data) {
        heapArray = new ArrayList<Integer>();
        
        // 0 인덱스 번호는 null로 설정
        heapArray.add(null);
        heapArray.add(data);
    }
    
    public boolean insert(Integer data) {
        if(heapArray == null) {
            heapArray = new ArrayList<Integer>();
        
        	// 0 인덱스 번호는 null로 설정
        	heapArray.add(null);
        	heapArray.add(data);
        } else {
            heapArray.add(data);
        }
        return true;
    }
}
````

````java
Heap heapTest = new Heap(1);
heapTest.insert(2);
heapTest.insert(3);
heapTest.insert(4);
heapTest.insert(5);

System.out.println(heapTest.heapArray);

=> [null, 1 , 2 , 3 , 4 , 5]
````



##### 힙 클래스 구현3 - insert2

- 삽입한 노드가 부모 노드의 값보다 클 경우, 부모 노드와 삽입한 노드 위치를 바꿈

- 삽입한 노드가 루트 노드가 되거나, 부모 노드보다 값이 작거나 같을 경우까지 반복



##### 특정 노드의 관련 노드 위치 알아내기

- 부모 노드 인덱스 번호 (parent node's index) = 자식 노드 인덱스 번호 (child node's index) / 2

- 왼쪽 자식 노드 인덱스 번호 (left child node's index) = 부모 노드 인덱스 번호 (parent node's index) * 2

- 오른쪽 자식 노드 인덱스 번호 (right child node's index) = 부모 노드 인덱스 번호 (parent node's index) * 2 + 1

<img src="https://user-images.githubusercontent.com/42603919/143730947-f4d5b507-6c43-4b9d-b251-d14abac7044a.PNG" alt="캡처" style="zoom:50%;" />



##### 힙 구현에 사용된 Collections.swap() 메서드 사용법 이해하기

- swap (스왑) 이란, 두 데이터의 위치를 맞바꾸는 것을 의미함

- swap 함수를 별도로 구현할 수도 있지만, JAVA 에서는 Collections 패키지에서 swap() 메서드를 제공해주고 있음
  - 하나의 배열 안에 있는 두 데이터의 위치를 서로 맞바꾸고 싶을 때 사용 가능

````java
import  java.util.Collections;

Collections.swap(List list, int a, int b)
````

- list : 스왑할 데이터들이 들어 있는 배열 변수

- a : 스왑할 데이터 인덱스 번호

- b : 스왑할 데이터 인덱스 번호

````java
import java.util.Collections;

ArrayList<Integer> heapArray = new ArrayList<Integer>();
heapArray.add(1);
heapArray.add(2);
System.out.println(heapArray);

Collections.swap(heapArray, 0, 1);
System.out.println(heapArray);

=> [1, 2]
   [2, 1]
````



````java
import java.util.ArrayList;

public class Heap {
    public ArrayList<Integer> heapArray = null;
    
    public Heap (Integer data) {
        heapArray = new ArrayList<Integer>();
        
        heapArray.add(null);
        heapArray.add(data);
    }
    
    public boolean move_up(Integer inserted_idx) {
        if (inserted_idx <= 1) {
            // 해당 if문은 루트 노드일 때 타고 들어오는 것
            return false;
        }
        Integer parent_idx = inserted_idx / 2;
        if (this.heapArray.get(inserted_idx) > this.heapArray.get(parent_idx)) {
            return true;
        } else {
            return false;
        }
    }
    
    public boolean insert(Integer data) {
        Integer inserted_idx, parent_idx;
        
        if (heapArray == null) {
            heapArray = new ArrayList<Integer>();
            
            heapArray.add(null);
            heapArray.add(data);
            return true;
        }
        
        this.heapArray.add(data);
        inserted_idx = this.heapArray.size() - 1;
        
        while (this.move_up(inserted_idx)) {
            parent_idx = inserted_idx / 2;
            Collections.swap(this.heapArray, inserted_idx, parent_idx);
            inserted_idx = parent_idx;
        }
        return true;
    }
}
````



##### 그림과 같이 테스트해보기

<img src="https://user-images.githubusercontent.com/42603919/143730994-c6d38ccc-332b-4e86-aa2a-0ba470ef6f09.PNG" alt="캡처" style="zoom:50%;" />

````java
Heap heapTest = new Heap(15);
heapTest.insert(10);
heapTest.insert(8);
heapTest.insert(5);
heapTest.insert(4);
heapTest.insert(20);

System.out.println(heapTest.heapArray);

=> [null, 20, 10, 15, 5, 4, 8]
````



#### 힙에 데이터 삭제 구현 (Max Heap 예)

##### 힙 클래스 구현4 - delete1

- 보통 삭제는 최상단 노드 (root 노드)를 삭제하는 것이 일반적임
  - 힙의 용도는 최대값 또는 최소값을 root 노드에 놓아서, 최대값과 최소값을 바로 꺼내 쓸 수 있도록 하는 것임

````java
import java.util.ArrayList;

public class Heap {
    public ArrayList<Integer> heapArray = null;
    
    public Heap (Integer data) {
        heapArray = new ArrayList<Integer>();
        
        heapArray.add(null);
        heapArray.add(data);
    }
    
    public boolean move_up(Integer inserted_idx) {
        if (inserted_idx <= 1) {
            // 해당 if문은 루트 노드일 때 타고 들어오는 것
            return false;
        }
        Integer parent_idx = inserted_idx / 2;
        if (this.heapArray.get(inserted_idx) > this.heapArray.get(parent_idx)) {
            return true;
        } else {
            return false;
        }
    }
    
    public boolean insert(Integer data) {
        Integer inserted_idx, parent_idx;
        
        if (heapArray == null) {
            heapArray = new ArrayList<Integer>();
            
            heapArray.add(null);
            heapArray.add(data);
            return true;
        }
        
        this.heapArray.add(data);
        inserted_idx = this.heapArray.size() - 1;
        
        while (this.move_up(inserted_idx)) {
            parent_idx = inserted_idx / 2;
            Collections.swap(this.heapArray, inserted_idx, parent_idx);
            inserted_idx = parent_idx;
        }
        return true;
    }
    
    public Integer pop() {
        if(this.heapArray == nunll) {
            return null;
        } else {
            return this.heapArray.get(1);
        }
    }
}
````



##### 힙 클래스 구현4 - delete2

- 상단의 데이터 삭제시, 가장 최하단부 왼쪽에 위치한 노드 (일반적으로 **가장 마지막에 추가한 노드**) 를 **root 노드로 이동**
- root 노드의 값이 child node 보다 작을 경우, **root 노드의 child node 중 가장 큰 값을 가진 노드와 root 노드 위치를 바꿔주는 작업을 반복함** (swap)



##### 특정 노드의 관련 노드 위치 알아내기

- 부모 노드 인덱스 번호 (parent node's index) = 자식 노드 인덱스 번호 (child node's index) / 2

- 왼쪽 자식 노드 인덱스 번호 (left child node's index) = 부모 노드 인덱스 번호 (parent node's index) * 2

- 오른쪽 자식 노드 인덱스 번호 (right child node's index) = 부모 노드 인덱스 번호 (parent node's index) * 2 + 1

<img src="https://user-images.githubusercontent.com/42603919/143731804-897f28d5-9f82-44ae-9137-7ea34319f2f5.PNG" alt="캡처" style="zoom:50%;" />



##### 구현을 위한 move_down 메서드 작성하기

````java
    public boolean move_down(Integer popped_idx) {
        Integer left_child_popped_idx, right_child_popped_idx;
        
        left_child_popped_idx = popped_idx * 2;
        right_child_popped_idx = popped_idx * 2 + 1;
        
        // CASE1 : 왼쪽 자식 노드도 없을 때 (자식 노드가 하나도 없을 때)
        if (left_child_popped_idx >= this.heapArray.size()) {
            return false;
        // CASE2 : 오른쪽 자식 노드만 없을 때 (왼쪽 노드는 있을 때)
        } else if (right_child_popped_idx >= this.heapArray.size()) {
            if (this.heapArray.get(popped_idx) < this.heapArray.get(left_child_popped_idx)) {
                return true;
            } else {
                return false;
            }
        // CASE3 : 왼쪽/오른쪽 자식 노드가 모두 있을 때
        } else {
            if (this.heapArray.get(left_child_popped_idx) > this.heapArray.get(right_child_popped_idx)) {
                if (this.heapArray.get(popped_idx) < this.heapArray.get(left_child_popped_idx)) {
                    return true;
                } else {
                    return false;
                }
            } else {
                if (this.heapArray.get(popped_idx) < this.heapArray.get(right_child_popped_idx)) {
                    return true;
                } else {
                    return false;
                }
            }
        }
    }
````



##### 구현을 위한 pop 메서드 작성하기

````java
    public Integer pop() {
        Integer returned_data, popped_idx, left_child_popped_idx, right_child_popped_idx; 
        
        if (this.heapArray == null) {
            return null;
        } else {
            returned_data = this.heapArray.get(1);
            this.heapArray.set(1, this.heapArray.get(this.heapArray.size() - 1));
            this.heapArray.remove(this.heapArray.size() - 1);
            popped_idx = 1;
            
            while (this.move_down(popped_idx)) {
                left_child_popped_idx = popped_idx * 2;
                right_child_popped_idx = popped_idx * 2 + 1;

                // CASE2: 오른쪽 자식 노드만 없을 때
                if (right_child_popped_idx >= this.heapArray.size()) {
                    if (this.heapArray.get(popped_idx) < this.heapArray.get(left_child_popped_idx)) {
                        Collections.swap(this.heapArray, popped_idx, left_child_popped_idx);
                        popped_idx = left_child_popped_idx;
                    }
                // CASE3: 왼쪽/오른쪽 자식 노드가 모두 있을 때                    
                } else {
                    if (this.heapArray.get(left_child_popped_idx) > this.heapArray.get(right_child_popped_idx)) {
                        if (this.heapArray.get(popped_idx) < this.heapArray.get(left_child_popped_idx)) {
                            Collections.swap(this.heapArray, popped_idx, left_child_popped_idx);
                            popped_idx = left_child_popped_idx;
                        } 
                    } else {
                        if (this.heapArray.get(popped_idx) < this.heapArray.get(right_child_popped_idx)) {
                            Collections.swap(this.heapArray, popped_idx, right_child_popped_idx);
                            popped_idx = right_child_popped_idx;
                        } 
                    }
                }
            }
            
            return returned_data;
        }
    }
````



#### 5. 힙 (Heap) 시간 복잡도

- depth (트리의 높이) 를 h라고 표기한다면,

- n개의 노드를 가지는 heap 에 데이터 삽입 또는 삭제시, 최악의 경우 root 노드에서 leaf 노드까지 비교해야 하므로 h = log_2{n}에 가까우므로, 시간 복잡도는 O(log{n})
  - 참고: 빅오 표기법에서 log{n}에서의 log의 밑은 10이 아니라, 2이다.
  - 한번 실행시마다, 50%의 실행할 수도 있는 명령을 제거한다는 의미. 즉 50%의 실행시간을 단축시킬 수 있다는 것을 의미함



참고

[자바 [JAVA] - 배열을 이용한 Heap (힙) 구현하기](https://st-lab.tistory.com/205)
