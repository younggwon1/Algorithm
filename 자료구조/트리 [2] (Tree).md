# 트리 [2] (Tree)

### 5.5. 이진 탐색 트리 삭제 코드 구현과 분석

#### 5.5.1 삭제할 Node 탐색

- 삭제할 Node가 없는 경우도 처리해야 함

- 이를 위해 삭제할 Node가 없는 경우는 False를 리턴하고, 함수를 종료 시킴

````java
    public boolean delete(int value) {
        boolean searched = false;
        
        // 삭제할 노드의 부모 노드
        Node currParentNode = this.head;
        // 삭제할 노드
        Node currNode = this.head;
        
        // 예외 케이스1: Node가 하나도 없을 때
        if (this.head == null) {
            return false;
        } else {
            // 예외 케이스2: Node가 단지 하나만 있고, 해당 Node 가 삭제할 Node 일 때
            if (this.head.value == value && this.head.left == null && this.head.right == null) {
                this.head = null;
                return true;
            }
            
            while (currNode != null) {
                if (currNode.value == value) {
                    searched = true;
                    break;
                } else if (value < currNode.value) {
                    currParentNode = currNode;
                    currNode = currNode.left;
                } else {
                    currParentNode = currNode;
                    currNode = currNode.right;                    
                }
            }
            
            if (searched == false) {
                return false;
            }
        }

        // 여기까지 실행되면,
        // currNode에는 해당 데이터를 가지고 있는 Node(삭제할 노드),
        // currParentNode 에는 해당 데이터를 가지고 있는 Node(삭제할 노드)의 부모 Node 
        
    }
````



#### 5.5.2. Case1: 삭제할 Node가 Leaf Node인 경우

<img src="https://user-images.githubusercontent.com/42603919/143226525-efe48424-f420-48c6-bbde-f99c37306a34.PNG" alt="캡처" style="zoom:67%;" />

````java
// Case1: 삭제할 Node가 Leaf Node 인 경우
// 삭제할 노드의 왼쪽, 오른쪽이 모두 없을 경우가 Leaf Node이다.
if (currNode.left == null && currNode.right == null) {
   // 삭제할 노드의 값이 부모 노드의 값보다 작을 경우, 부모 노드의 왼쪽에 있으므로 왼쪽을 삭제한다.
   if (value < currParentNode.value) {
      currParentNode.left = null;
      currNode = null;
   // 삭제할 노드의 값이 부모 노드의 값보다 클 경우, 부모 노드의 오른쪽에 있으므로 오른쪽을 삭제한다.
   } else {
      currParentNode.right = null;
      currNode = null;
   }
return true;
````



#### 5.5.2. Case2: 삭제할 Node가 Child Node를 한 개 가지고 있을 경우

<img src="https://user-images.githubusercontent.com/42603919/143226823-5304105e-9fe9-4f19-93ba-f08c46f98067.PNG" alt="캡처" style="zoom:67%;" />

````java
// Case2-1: 삭제할 Node가 Child Node를 한 개 가지고 있을 경우 (왼쪽에 Child Node 가 있을 경우)
		// 조건절에서 삭제할 노드의 왼쪽에 node가 존재하고, 오른쪽에 node가 존재하지 않으면 다음 else if절을 탄다
        } else if (currNode.left != null && currNode.right == null) {
            if (value < currParentNode.value) {
                currParentNode.left = currNode.left;
                currNode = null;
            } else {
                currParentNode.right = currNode.left;
                currNode = null;
            }
            return true;
        // Case2-2: 삭제할 Node 가 Child Node를 한 개 가지고 있을 경우 (오른쪽에 Child Node 가 있을 경우)
        // 조건절에서 삭제할 노드의 오른쪽에 node가 존재하고, 왼쪽에 node가 존재하지 않으면 다음 else절을 탄다
        } else if (currNode.left == null && currNode.right != null) {
            // 삭제할 노드의 값이 부모 노드의 값보다 작은 경우 부모 노드의 왼쪽을 삭제할 노드의 왼쪽 노드로 한다.
            if (value < currParentNode.value) {
                currParentNode.left = currNode.right;
                currNode = null;
            } else {
                currParentNode.right = currNode.right;
                currNode = null;
            }
            return true;
````



#### 5.5.3. Case3-1: 삭제할 Node가 Child Node를 두 개 가지고 있을 경우 (삭제할 Node가 Parent Node 왼쪽에 있을 때)

* 기본 사용 가능 전략
  1. **삭제할 Node의 오른쪽 자식 중, 가장 작은 값을 삭제할 Node의 Parent Node가 가리키도록 한다.**
  2. 삭제할 Node의 왼쪽 자식 중, 가장 큰 값을 삭제할 Node의 Parent Node가 가리키도록 한다.

* 기본 사용 가능 전략 중, 1번 전략을 사용하여 코드를 구현하기로 함
  - 경우의 수가 또다시 두가지가 있음
    - Case3-1-1:삭제할 Node가 Parent Node의 왼쪽에 있고, 삭제할 Node의 오른쪽 자식 중, 가장 작은 값을 가진 Node의 Child Node가 없을 때
    - Case3-1-2:삭제할 Node가 Parent Node의 왼쪽에 있고, 삭제할 Node의 오른쪽 자식 중, 가장 작은 값을 가진 Node의 오른쪽에 Child Node가 있을 때
      - 가장 작은 값을 가진 Node의 Child Node가 왼쪽에 있을 경우는 없음, 왜냐하면 왼쪽 Node가 있다는 것은 해당 Node보다 더 작은 값을 가진 Node가 있다는 뜻이기 때문임



<img src="https://user-images.githubusercontent.com/42603919/143227261-768b9a10-b28e-445f-add0-f4c9d2ba0674.PNG" alt="캡처" style="zoom:67%;" />

```java
        // Case3-1: 삭제할 Node가 Child Node 를 두 개 가지고 있고, (삭제할 Node 가 부모 Node의 왼쪽에 있을 때)
        } else {
            
            // 삭제할 Node가 부모 Node 의 왼쪽에 있을 때
            if (value < currParentNode.value) {
                
                Node changeNode = currNode.right;
                Node changeParentNode = currNode.right;
                // changeNodedml 왼쪽에 노드가 존재한다면, 계속적으로 왼쪽으로 가는 로직. 계속 가다가 Node가 없으면 해당 Node가 가장 작은 값을 가진다.
                while (changeNode.left != null) {
                    changeParentNode = changeNode;
                    changeNode = changeNode.left;
                }
                // 여기까지 실행되면, changeNode에는 삭제할 Node의 오른쪽 Node 중에서, 가장 작은 값을 가진 Node가 들어있음
                
                // Case 3-1-2: changeNode(가장 작은 값을 가진 노드)의 오른쪽 Child Node 가 있을 때
                if (changeNode.right != null) {
                    changeParentNode.left = changeNode.right;
                } 
                // Case 3-1-1: changeNode 의 Child Node가 없을 때
                else {
                    changeParentNode.left = null;
                }
                
                // currParentNode의 왼쪽 Child Node에, 삭제할 Node의 오른쪽 자식 중, 가장 작은 값을 가진 changeNode 를 연결
                currParentNode.left = changeNode;
                
                // parentNode의 왼쪽 Child Node가 현재 changeNode 이고,
                // changeNode의 왼쪽/오른쪽 Child Node를 모두, 삭제할 currNode 의 기존 왼쪽/오른쪽 Node 로 변경
                changeNode.right = currNode.right;
                changeNode.left = currNode.left;
                
                currNode = null;
```





#### 5.5.4. Case3-2: 삭제할 Node가 Child Node를 두 개 가지고 있을 경우 (삭제할 Node가 Parent Node 오른쪽에 있을 때)

* 기본 사용 가능 전략

1. **삭제할 Node의 오른쪽 자식 중, 가장 작은 값을 삭제할 Node의 Parent Node가 가리키도록 한다.**

2. 삭제할 Node의 왼쪽 자식 중, 가장 큰 값을 삭제할 Node의 Parent Node가 가리키도록 한다.

* 기본 사용 가능 전략 중, 1번 전략을 사용하여 코드를 구현하기로 함
  - 경우의 수가 또다시 두가지가 있음
    - Case3-2-1: 삭제할 Node가 Parent Node의 오른쪽에 있고, 삭제할 Node의 오른쪽 자식 중, 가장 작은 값을 가진 Node의 Child Node가 없을 때
    - Case3-2-2: 삭제할 Node가 Parent Node의 오른쪽에 있고, 삭제할 Node의 오른쪽 자식 중, 가장 작은 값을 가진 Node의 오른쪽에 Child Node가 있을 때
      - 가장 작은 값을 가진 Node의 Child Node가 왼쪽에 있을 경우는 없음, 왜냐하면 왼쪽 Node가 있다는 것은 해당 Node보다 더 작은 값을 가진 Node가 있다는 뜻이기 때문임



<img src="https://user-images.githubusercontent.com/42603919/143229289-0cfa4d72-0d12-4c3d-b23b-4c7e98830c06.PNG" alt="캡처" style="zoom:67%;" />

````java
        // Case3-2: 삭제할 Node가 Child Node를 두 개 가지고 있고, (삭제할 Node 가 부모 Node의 오른쪽에 있을 때)
        } else {
                Node changeNode = currNode.right;
                Node changeParentNode = currNode.right;
                while (changeNode.left != null) {
                    changeParentNode = changeNode;
                    changeNode = changeNode.left;
                }
                // 여기까지 실행되면, changeNode에는 삭제할 Node의 오른쪽 Node 중에서, 가장 작은 값을 가진 Node 가 들어있음            
                
            	// Case 3-2-2: changeNode의 오른쪽 Child Node가 있을 때
                if (changeNode.right != null) {
                    changeParentNode.left = changeNode.right;
                }
            	// Case 3-2-1: changeNode의 Child Node가 없을 때
            	else {
                    changeParentNode.left = null;
                }

                // currParentNode의 오른쪽 Child Node에, 삭제할 Node의 오른쪽 자식 중, 가장 작은 값을 가진 changeNode를 연결
                currParentNode.right = changeNode;
                
                // parentNode 의 왼쪽 Child Node 가 현재, changeNode 이고, changeNode 의 왼쪽/오른쪽 Child Node 를 모두, 삭제할 currNode의 기존 왼쪽/오른쪽 Node 로 변경
                changeNode.right = currNode.right;
                changeNode.left = currNode.left;
                
                currNode = null;            
        }
        return true;
````

