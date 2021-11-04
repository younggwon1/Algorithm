# 링크드리스트1 (Linked List)

### 1. 링크드 리스트 (Linked List) 구조

- **연결 리스트**라고도 함
- **배열**은 순차적으로 연결된 공간에 데이터를 나열하는 데이터 구조
- **링크드 리스트**는 떨어진 곳에 존재하는 데이터를 화살표로 연결해서 관리하는 데이터 구조

- 링크드 리스트 기본 구조와 용어
  - **노드(Node)** : 데이터 저장 단위 ( **데이터 값 , 포인터** )로 구성
  - **포인터(Pointer)** : 각 노드 안에서, 다음이나 이전의 노드와의 **연결 정보**를 가지고 있는 공간
    - 특정 메모리 공간, 주소를 가리킴
- 일반적인 링크드 리스트 형태

![캡처](https://user-images.githubusercontent.com/42603919/140297529-ae912b25-e2ba-4d13-958d-e8b1efba01b9.PNG)![캡처](https://user-images.githubusercontent.com/42603919/140296854-6de58c88-9403-403d-aa4f-2d7fe97b478f.PNG)

### 2. 링크드 리스트의 장단점

- 장점
  - **리스트의 길이가 가변적** , 미리 데이터 공간을 할당하지 않아도 된다. ( 배열은 미리 공간을 할당해야함. )
- 단점
  - 연결을 위한 별도 데이터 공간이 필요하므로, **저장 공간 효율이 높지 않음**
  - 연결 정보를 찾는 시간이 필요하므로 **접근 속도가 느림**
  - 중간 데이터 삭제시, 앞 뒤 데이터의 연결을 재구성해야하는 **부가적인 작업 필요**



### 3. 간단한 링크드 리스트 예

#### 3.1 Node 클래스 구현

````java
public class Node<T> {
    // 데이터
	T data;
    // 포인터 (다음 데이터 주소)
	Node<T> next = null;
	
	public Node(T data) {
		this.data = data;
	}
}
````



#### 3.2 Node와 Node 연결하기 : Node 인스턴스간 연결

````java
Node<Integer> node1 = new Node<Integer>(1);
Node<Integer> node2 = new Node<Integer>(2);
````

````java
node1.next = node2;

// 맨 앞의 노드를 나타내는 변수 선언
Node head = node1;
````



#### 3.3 링크드 리스트에 데이터 추가하기

````java
public class SingleLinkedList<T> {
    // head 선언
    public Node<T> head = null;
    
    public class Node<T> {
        T data;
        Node<T> next = null;
        
        public Node(T data) {
            this.data = data;
        }
    }
    
    // 노드를 추가하는 메서드 생성
    public void addNode(T data) {
        // head == null -> 추가되는 노드가 첫 노드가 됨
        if(head == null) { 
            head = new Node<T>(data)
        } else {
            // head가 존재한다 (노드가 존재한다)
            Node<T> node = this.head;
            // 끝 노드까지 진행
            while (node.next != null) {
                node = node.next;
            }
            // 맨 끝에 있는 노드에 포인터를 추가하는 데이터를 가진 노드로 연결
            node.next = new Node<T>(data);
        }
    }
}
````



#### 3.4 링크드 리스트 데이터 출력하기 (검색하기)

````java
SingleLinkedList<Integer> MyLinkedList = new SingleLinkedList<Integer>();

MyLinkedList.addNode(1);

MyLinkedList.head.data
=> 1
    
MyLinkedList.addNode(2);

MyLinkedList.head.next.data
=> 2
````



#### 3.5 링크드 리스트 데이터 모두 출력

```java
public class SingleLinkedList<T> {
    public Node<T> head = null;
    
    public class Node<T> {
        T data;
        Node<T> next = null;
        
        public Node(T data) {
            this.data = data;
        }
    }
    
    public void addNode(T data) {
        if(head == null) {
            head = new Node<T>(data)
        } else {
            Node<T> node = this.head;
            while (node.next != null) {
                node = node.next;
            }
            node.next = new Node<T>(data);
        }
    }
    
    // 모두 출력
    public void printAll() {
    	if(head != null) {
    		Node<T> node = this.head;
    		System.out.println(node.data);
    		
    		while (node.next != null) {
    			node = node.next;
    			System.out.println(node.data);
    		}
    	}
    }
}
```

```java
SingleLinkedList<Integer> MyLinkedList = new SingleLinkedList<Integer>();

MyLinkedList.addNode(1);
MyLinkedList.addNode(2);
MyLinkedList.addNode(3);

MyLinkedList.printAll();
=> 1 2 3
```



### 4. 링크드 리스트의 복잡한 기능1 ( 링크드 리스트 데이터 사이에 데이터를 추가 )

![캡처](https://user-images.githubusercontent.com/42603919/140301925-b4e43f92-ef84-41c7-8670-e892563091ab.PNG)



````java
public class SingleLinkedList<T> {
    public Node<T> head = null;
    
    public class Node<T> {
        T data;
        Node<T> next = null;
        
        public Node(T data) {
            this.data = data;
        }
    }
    
    public void addNode(T data) {
        if(head == null) {
            head = new Node<T>(data)
        } else {
            Node<T> node = this.head;
            while (node.next != null) {
                node = node.next;
            }
            node.next = new Node<T>(data);
        }
    }
    
    // 모두 출력
    public void printAll() {
    	if(head != null) {
    		Node<T> node = this.head;
    		System.out.println(node.data);
    		
    		while (node.next != null) {
    			node = node.next;
    			System.out.println(node.data);
    		}
    	}
    }
    
    public Node<T> search(T data) {
        if(this.head == null) {
    		return null;        
        } else {
            Node<T> node = this.head;
            while(node != null) {
                if(node.data == data) {
                    return node;
                } else {
                    node = node.next;
                }
            }
            return null;
        }
    }
    
    // 링크드 리스트 데이터 사이에 데이터 추가!!!
    // T data : 내가 가지는 데이터 (newData), T isData : 추가될 데이터(newData) 앞에 있는 데이터(node)
    public void addNodeInside(T data, T isData) {
        Node<T> searchedNode = this.search(isData);
        
        if(searchedNode == null) {
            this.addNode(data);
        } else {
            Node<T> nextNode = searchedNode.next;
            searchedNode.next = new Node<T>(data);
            searchedNode.next.next = nextNode;
            
        }
    }
}
````



- 링크드 리스트 생성하고 1, 2, 3, 데이터 넣기

```java
SingleLinkedList<Integer> MyLinkedList = new SingleLinkedList<Integer>();

MyLinkedList.addNode(1);
MyLinkedList.addNode(2);
MyLinkedList.addNode(3);

MyLinkedList.printAll();
=> 1 2 3
```



- 1 데이터 뒤에 5 넣어보기

```java
MyLinkedList.addNodeInside(5,1);

MyLinkedList.printAll();
=> 1 5 2 3
```



- 3 데이터 뒤에 6 데이터 넣기

````
MyLinkedList.addNodeInside(6,3);

MyLinkedList.printAll();
=> 1 5 2 3 6
````



- 없는 데이터를 찾도록 해서, 맨 마지막에 데이터 넣기

````
MyLinkedList.addNodeInside(7,20);

MyLinkedList.printAll();
=> 1 5 2 3 6 7
````





### 5. 링크드 리스트의 복잡한 기능2 ( 특정 노드를 삭제 )

````java
public class SingleLinkedList<T> {
    public Node<T> head = null;
    
    public class Node<T> {
        T data;
        Node<T> next = null;
        
        public Node(T data) {
            this.data = data;
        }
    }
    
    public void addNode(T data) {
        if(head == null) {
            head = new Node<T>(data)
        } else {
            Node<T> node = this.head;
            while (node.next != null) {
                node = node.next;
            }
            node.next = new Node<T>(data);
        }
    }
    
    // 모두 출력
    public void printAll() {
    	if(head != null) {
    		Node<T> node = this.head;
    		System.out.println(node.data);
    		
    		while (node.next != null) {
    			node = node.next;
    			System.out.println(node.data);
    		}
    	}
    }
    
    public Node<T> search(T data) {
        if(this.head == null) {
    		return null;        
        } else {
            Node<T> node = this.head;
            while(node != null) {
                if(node.data == data) {
                    return node;
                } else {
                    node = node.next;
                }
            }
            return null;
        }
    }
    
    // 링크드 리스트 데이터 사이에 데이터 추가!!!
    // T data : 내가 가지는 데이터 (newData), T isData : 추가될 데이터(newData) 앞에 있는 데이터(node)
    public void addNodeInside(T data, T isData) {
        Node<T> searchedNode = this.search(isData);
        
        if(searchedNode == null) {
            this.addNode(data);
        } else {
            Node<T> nextNode = searchedNode.next;
            searchedNode.next = new Node<T>(data);
            searchedNode.next.next = nextNode;
            
        }
    }
    
    // 특정 노드 삭제
    public boolean delNode(T isData) {
        if(this.head == null) {
            return false;
        } else {
            Node<T> node = this.head;
            if(node.data == this.isData) {
                this.head = this.head.next;
                return true;
            } else {
                while(node.next != null) {
                    if(node.next.data == isData) {
                        node.next = node.next.next;
                        return true;
                    }
                    node = node.next;
                }
                return false;
            }
        }
    }
}
````



- 테스트1 : 5개의 노드 생성

````java
SingleLinkedList<Integer> MyLinkedList = new SingleLinkedList<Integer>();

MyLinkedList.addNode(1);
MyLinkedList.addNode(2);
MyLinkedList.addNode(3);
MyLinkedList.addNode(4);
MyLinkedList.addNode(5);

MyLinkedList.printAll();
=> 1 2 3 4 5
````



- 테스트2 : 중간 노드 삭제

````java
MyLinkedList.delNode(3);

=> true
    
MyLinkedList.printAll();
=> 1 2 4 5
````



- 테스트3 : 맨 앞의 노드(헤드) 삭제

````java
MyLinkedList.delNode(1);

=> true
    
MyLinkedList.printAll();
=> 2 4 5
````



- 테스트4: 맨 마지막 노드 삭제

````java
MyLinkedList.delNode(5);

=> true
    
MyLinkedList.printAll();
=> 2 4
````



- 테스트5 : 없는 노드 삭제

````java
MyLinkedList.delNode(20);

=> false
````







