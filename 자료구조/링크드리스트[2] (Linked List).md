# 링크드리스트[2] (Linked List)

### 다양한 링크드 리스트 구조

참고 : https://yjg-lab.tistory.com/122

#### 1. 더블 링크드 리스트 ( Doubly Linked List )

![캡처](https://user-images.githubusercontent.com/42603919/141451169-4183837a-2473-4a2a-a5f8-a5a8c038b4bf.PNG)

- 기본 구조
  - 각 노드가 선행 노드와 후속 노드에 대한 링크를 가지는 리스트이다.
  - **이중 연결 리스트**라고도 함
  - 장점 : **양방향**으로 연결되어 있어서 **노드 탐색이 양쪽으로 모두 가능**



```java
public class DoubleLinkedList<T> {
	public Node<T> head = null; // 노드 head
	public Node<T> tail = null; // 노드 tail
	
	public class Node<T> {
		T data;
		Node<T> prev = null; // 앞에 있는 노드를 가리키는 포인터
		Node<T> next = null; // 뒤에 있는 노드를 가리키는 포인터
		
		public Node(T data) {
			this.data = data;
		}
	}
    
    // 데이터를 추가하는 메서드
    public void addNode(T data) {
        if(this.head == null) {
            this.head = new Node<T>(data);
            this.tail = this.head;
        } else {
            Node<T> node = this.head;
            while (node.next != null) {
                node = node.next;
            }
            node.next = new Node<T>(data);
            node.next.prev = node;
            this.tail = node.next;
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



````java
DoubleLinkedList<Integer> MyLinkedList = new DoubleLinkedList<Integer>();

MyLinkedList.addNode(1);
MyLinkedList.addNode(2);
MyLinkedList.addNode(3);
MyLinkedList.addNode(4);
MyLinkedList.addNode(5);

MyLinkedList.printAll();
=> 1 2 3 4 5
````





![캡처](https://user-images.githubusercontent.com/42603919/141453097-14b1a12c-34c3-422e-b529-e3dac677b995.PNG)

```java
public class DoubleLinkedList<T> {
	public Node<T> head = null; // 노드 head
	public Node<T> tail = null; // 노드 tail
	
	public class Node<T> {
		T data;
		Node<T> prev = null; // 앞에 있는 노드를 가리키는 포인터
		Node<T> next = null; // 뒤에 있는 노드를 가리키는 포인터
		
		public Node(T data) {
			this.data = data;
		}
	}
    
    // 데이터를 추가하는 메서드
    public void addNode(T data) {
        if(this.head == null) {
            this.head = new Node<T>(data);
            this.tail = this.head;
        } else {
            Node<T> node = this.head;
            while (node.next != null) {
                node = node.next;
            }
            node.next = new Node<T>(data);
            node.next.prev = node;
            this.tail = node.next;
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
    
    // head부터 특정 노드를 찾는 메서드 추가하기
    public T searchFromHead(T isData) {
        if(this.head == null) {
            return null;
        } else {
            Node<T> node = this.head;
            while(node != null) {
                if(node.data == isData) {
                    return node.data;
                } else {
                    node = node.next;
                }
            }
            return null;
        }
    }
    
    // tail부터 특정 노드를 찾는 메서드 추가하기
    public T searchFromTail(T isData) {
        if(this.head == null) {
            return null;
        } else {
            Node<T> node = this.tail;
            while(node != null) {
                if(node.data == isData) {
                    return node.data;
                } else {
                    node = node.prev;
                }
            }
            return null;
        }
    }
}
```



##### 연습문제

![캡처](https://user-images.githubusercontent.com/42603919/141454635-d5819262-3bc3-4210-92d2-186bcf90531c.PNG)

![캡처](https://user-images.githubusercontent.com/42603919/141456991-09e83d4e-39c3-4d81-8ec0-a80cedfc5c4e.PNG)

```java
public class DoubleLinkedList<T> {
		public Node<T> head = null; // 노드 head
		public Node<T> tail = null; // 노드 tail
		
		public class Node<T> {
			T data;
			Node<T> prev = null; // 앞에 있는 노드를 가리키는 포인터
			Node<T> next = null; // 뒤에 있는 노드를 가리키는 포인터
			
			public Node(T data) {
				this.data = data;
			}
		}
	    
	    // 데이터를 추가하는 메서드
	    public void addNode(T data) {
	        if(this.head == null) {
	            this.head = new Node<T>(data);
	            this.tail = this.head;
	        } else {
	            Node<T> node = this.head;
	            while (node.next != null) {
	                node = node.next;
	            }
	            node.next = new Node<T>(data);
	            node.next.prev = node;
	            this.tail = node.next;
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
	    
	    // head부터 특정 노드를 찾는 메서드 추가하기
	    public T searchFromHead(T isData) {
	        if(this.head == null) {
	            return null;
	        } else {
	            Node<T> node = this.head;
	            while(node != null) {
	                if(node.data == isData) {
	                    return node.data;
	                } else {
	                    node = node.next;
	                }
	            }
	            return null;
	        }
	    }
	    
	    // tail부터 특정 노드를 찾는 메서드 추가하기
	    public T searchFromTail(T isData) {
	        if(this.head == null) {
	            return null;
	        } else {
	            Node<T> node = this.tail;
	            while(node != null) {
	                if(node.data == isData) {
	                    return node.data;
	                } else {
	                    node = node.prev;
	                }
	            }
	            return null;
	        }
	    }
	    
	    // 데이터를 임의 노드 앞에 노드를 추가하는 메서드 추가하기
	    // 노드 추가에 성공 = true , 노드 추가에 실패 = false
	    public boolean insertToFront(T existedData, T addData) {
	    	if(this.head == null) {
	    		this.head = new Node<T>(addData);
	    		this.tail = this.head;
	    		return true;
	    	} else if(this.head.data == existedData) {
	    		Node<T> newHead = new Node<T>(addData);
	    		newHead.next = this.head;
	    		this.head = newHead;
	    		return true;
	    	} else {
	    		Node<T> node = this.head;
	    		while(node != null) {
	    			if(node.data == existedData) {
	    				Node<T> nodePrev = node.prev;
	    				
	    				nodePrev.next = new Node<T>(addData);
	    				nodePrev.next.next = node;
	    				
	    				nodePrev.next.prev = nodePrev;
	    				node.prev = nodePrev.next;
	    				
	    				return true;
	    			} else {
	    				node = node.next;
	    			}
	    		}
	    		return false;
	    	}
	    }
	}
```





#### 2. 