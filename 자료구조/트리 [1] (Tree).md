# 트리 [1] (Tree)

### 1. 트리 (Tree) 구조

- **트리(Tree)** : **Node**와 **Branch**를 이용해서, **사이클을 이루지 않도록 구성한 데이터 구조**
- root 노드는 0개 이상의 자식노드를 가지고 있다.
  - 그 자식 노드 또한 0개 이상의 자식 노드를 갖고 있고, 이는 반복적으로 정의된다.

- 실제로 어디에 많이 사용되나? 
  - 트리 중 **이진 트리 (Binary Tree)** 형태의 구조로, 탐색(검색) 알고리즘 구현을 위해 많이 사용된다.



### 2. 알아둘 용어

- 루트 노드(root node) : 부모가 없는 노드, 트리는 하나의 루트 노드만을 가진다.
- 단말 노드(leaf node) : 자식이 없는 노드, ‘말단 노드’ 또는 ‘잎 노드’라고도 부른다.
- 내부(internal) 노드 : 단말 노드가 아닌 노드
- 간선(edge) : 노드를 연결하는 선 (link, branch 라고도 부름)
- 형제(sibling) : 같은 부모를 가지는 노드
- 노드의 크기(size) : 자신을 포함한 모든 자손 노드의 개수
- 노드의 깊이(depth) : 루트에서 어떤 노드에 도달하기 위해 거쳐야 하는 간선의 수
- 노드의 레벨(level) : 트리의 특정 깊이를 가지는 노드의 집합
- 노드의 차수(degree) : 하위 트리 개수 / 간선 수 (degree) = 각 노드가 지닌 가지의 수
- 트리의 차수(degree of tree) : 트리의 최대 차수
- 트리의 높이(height) : 루트 노드에서 가장 깊숙히 있는 노드의 깊이
  

<img src="https://user-images.githubusercontent.com/42603919/143014109-ce01a00b-6a65-4c1b-9d51-df0fab4dbb9d.PNG" alt="1" style="zoom:67%;" />



### 2.1 트리 (Tree) 특징

- 그래프의 한 종류이다. ‘최소 연결 트리’ 라고도 불린다.
- 트리는 계층 모델 이다.
- 트리는 DAG(Directed Acyclic Graphs, 방향성이 있는 비순환 그래프)의 한 종류이다.
  - loop나 circuit이 없다. 당연히 self-loop도 없다.
  - 즉, 사이클이 없다.

- 노드가 N개인 트리는 항상 N-1개의 간선(edge)을 가진다.
  - 즉, 간선은 항상 (정점의 개수 - 1) 만큼을 가진다.

- 루트에서 어떤 노드로 가는 경로는 유일하다.
  - 임의의 두 노드 간의 경로도 유일하다. 즉, 두 개의 정점 사이에 반드시 1개의 경로만을 가진다.

- 한 개의 루트 노드만이 존재하며 모든 자식 노드는 한 개의 부모 노드만을 가진다.
  - 부모-자식 관계이므로 흐름은 top-bottom 아니면 bottom-top으로 이루어진다.

- 순회는 Pre-order, In-order 아니면 Post-order로 이루어진다. 이 3가지 모두 DFS/BFS 안에 있다.
- 트리는 이진 트리, 이진 탐색 트리, 균형 트리(AVL 트리, red-black 트리), 이진 힙(최대힙, 최소힙) 등이 있다.



### 3. 이진 트리와 이진 탐색 트리 (Binary Search Tree)

- **이진 트리** : 노드의 최대 Branch가 2인 트리

- **이진 탐색 트리** (Binary Search Tree, BST): 이진 트리에 다음과 같은 추가적인 조건이 있는 트리
  - **왼쪽 노드는 해당 노드보다 작은 값**, **오른쪽 노드는 해당 노드보다 큰 값**을 가지고 있다.

 

<img src="https://www.mathwarehouse.com/programming/images/binary-search-tree/binary-search-tree-insertion-animation.gif" />

(출처: https://www.mathwarehouse.com/programming/gifs/binary-search-tree.php#binary-search-tree-insertion-node) 





### 4. 자료 구조 이진 탐색 트리의 장점과 주요 용도

- 주요 용도: 데이터 검색(탐색) 

- 장점: 탐색 속도를 개선할 수 있음



\> 단점은 이진 탐색 트리 알고리즘 이해 후에 살펴보기로 함



### 이진트리와 정렬된 배열간의 탐색 비교

<img src="https://www.mathwarehouse.com/programming/images/binary-search-tree/binary-search-tree-sorted-array-animation.gif" />

(출처: https://www.mathwarehouse.com/programming/gifs/binary-search-tree.php#binary-search-tree-insertion-node)



---



### 5.1 노드 클래스 만들기

````java
public class NodeMgmt {
    public class Node {
        Node left;
        Node right;
        int value;
        public Node (int data) {
            this.value = data;
            this.left = null;
            this.right = null;
        }
    }
}
````



### 5.2. 이진 탐색 트리에 데이터 넣기

* 이진 탐색 트리 조건에 부합하게 데이터를 넣어야 함

````java
public class NodeMgmt {
    Node head = null;
    
    public class Node {
        Node left;
        Node right;
        int value;
        public Node (int data) {
            this.value = data;
            this.left = null;
            this.right = null;
        }
    }
    
    public boolean insertNode(int data) {
        // Node가 하나도 없을 때
        if (this.head == null) {
            // Node 생성
            this.head = new Node(data);
        } else {
            // Node가 하나 이상 들어가 있을 때
            Node findNode = this.head;
            while (true) {
                // 현재 Node의 왼쪽에 Node 가 들어가야할 때
                if (data < findNode.value) {
                    if (findNode.left != null) {
                        findNode = findNode.left;
                    } else {
                        findNode.left = new Node(data);
                        break;
                    }
                // 현재 Node의 오른쪽에 Node 가 들어가야할 때                    
                } else {
                    if (findNode.right != null) {
                        findNode = findNode.right;
                    } else {
                        findNode.right = new Node(data);
                        break;
                    }
                }
            }
        }
        return true;        
    }
}
````



````java
NodeMgmt myTree = new NodeMgmt();
myTree.insertNode(2);
myTree.insertNode(3);
myTree.insertNode(4);
myTree.insertNode(6);

=> true
````



### 5.3. 이진 탐색 트리 탐색

````java
public class Node {
    Node left;
    Node right;
    int value;
    public Node (int data) {
        this.value = data;
        this.left = null;
        this.right = null;
    }
}

public class NodeMgmt {
    Node head = null;
    
    public boolean insertNode(int data) {
        // Node가 하나도 없을 때
        if (this.head == null) {
            this.head = new Node(data);
        } else {
            // Node가 하나 이상 들어가 있을 때
            Node findNode = this.head;
            while (true) {
                // 현재 Node의 왼쪽에 Node 가 들어가야할 때
                if (data < findNode.value) {
                    if (findNode.left != null) {
                        findNode = findNode.left;
                    } else {
                        findNode.left = new Node(data);
                        break;
                    }
                // 현재 Node의 오른쪽에 Node 가 들어가야할 때                    
                } else {
                    if (findNode.right != null) {
                        findNode = findNode.right;
                    } else {
                        findNode.right = new Node(data);
                        break;
                    }
                }
            }
        }
        return true;        
    }
    
    public Node search(int data) {
        // Node가 하나도 없을 때
        if (this.head == null) {
            return null;
        // Node가 하나 이상 있을 때            
        } else {
            Node findNode = this.head;
            while (findNode != null) {
                if (findNode.value == data) {
                    return findNode;
                } else if (data < findNode.value) {
                    findNode = findNode.left;
                } else {
                    findNode = findNode.right;
                }
            }
            return null;
        }
    }
}
````



````java
NodeMgmt myTree = new NodeMgmt();
myTree.insertNode(2);
myTree.insertNode(3);
myTree.insertNode(4);
myTree.insertNode(6);

=> true
````

````java
Node testNode = myTree.search(3);
testNode.right.value

=> 4
````



### 5.4. 이진 탐색 트리 삭제

#### 5.4.1. Leaf Node 삭제

* Leaf Node : Child Node 가 없는 Node

* **삭제할 Node의 Parent Node가 삭제할 Node를 가리키지 않도록 한다.** 

![2](https://user-images.githubusercontent.com/42603919/143014120-03f64ec2-dd91-4619-9d4a-5351b616d11c.PNG)



#### 5.4.2. Child Node 가 하나인 Node 삭제

* **삭제할 Node의 Parent Node가 삭제할 Node의 Child Node를 가리키도록 한다.**

![3](https://user-images.githubusercontent.com/42603919/143014079-1a52ca29-edb0-4476-b11d-7f53f680d8cd.PNG)



#### 5.4.3. Child Node 가 두 개인 Node 삭제

1. **삭제할 Node의 오른쪽 자식 중, 가장 작은 값을 삭제할 Node의 Parent Node가 가리키도록 한다.**

2. 삭제할 Node의 왼쪽 자식 중, 가장 큰 값을 삭제할 Node의 Parent Node가 가리키도록 한다.

![4](https://user-images.githubusercontent.com/42603919/143014126-a3e5a717-d8b6-47f5-aba1-81d7ab4dc018.PNG)



##### 5.4.3.1. 삭제할 Node의 오른쪽 자식중, 가장 작은 값을 삭제할 Node의 Parent Node가 가리키게 할 경우

- 삭제할 Node의 오른쪽 자식 선택

- 오른쪽 자식의 가장 왼쪽에 있는 Node를 선택

- 해당 Node를 삭제할 Node의 Parent Node의 왼쪽 Branch가 가리키게 함

- 해당 Node의 왼쪽 Branch가 삭제할 Node의 왼쪽 Child Node를 가리키게 함

- 해당 Node의 오른쪽 Branch가 삭제할 Node의 오른쪽 Child Node를 가리키게 함

- 만약 해당 Node가 오른쪽 Child Node를 가지고 있었을 경우에는, 해당 Node의 본래 Parent Node의 왼쪽 Branch가 해당 오른쪽 Child Node를 가리키게 함







참고

[[자료구조] 트리(Tree)란](https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html)