#  [깊이/너비 우선 탐색(DFS/BFS)] 네트워크

[네트워크](https://programmers.co.kr/learn/courses/30/lessons/43162)

###### 문제 설명

네트워크란 컴퓨터 상호 간에 정보를 교환할 수 있도록 연결된 형태를 의미합니다. 예를 들어, 컴퓨터 A와 컴퓨터 B가 직접적으로 연결되어있고, 컴퓨터 B와 컴퓨터 C가 직접적으로 연결되어 있을 때 컴퓨터 A와 컴퓨터 C도 간접적으로 연결되어 정보를 교환할 수 있습니다. 따라서 컴퓨터 A, B, C는 모두 같은 네트워크 상에 있다고 할 수 있습니다.

컴퓨터의 개수 n, 연결에 대한 정보가 담긴 2차원 배열 computers가 매개변수로 주어질 때, 네트워크의 개수를 return 하도록 solution 함수를 작성하시오.

##### 제한사항

- 컴퓨터의 개수 n은 1 이상 200 이하인 자연수입니다.
- 각 컴퓨터는 0부터 `n-1`인 정수로 표현합니다.
- i번 컴퓨터와 j번 컴퓨터가 연결되어 있으면 computers[i][j]를 1로 표현합니다.
- computer[i][i]는 항상 1입니다.

##### 입출력 예

| n    | computers                         | return |
| ---- | --------------------------------- | ------ |
| 3    | [[1, 1, 0], [1, 1, 0], [0, 0, 1]] | 2      |
| 3    | [[1, 1, 0], [1, 1, 1], [0, 1, 1]] | 1      |

##### 입출력 예 설명

예제 #1
아래와 같이 2개의 네트워크가 있습니다.

<img src="https://user-images.githubusercontent.com/42603919/162473557-7ada2693-3451-41ef-9aef-8f25487f172b.PNG" alt="캡처" style="zoom:50%;" />



예제 #2
아래와 같이 1개의 네트워크가 있습니다.

<img src="https://user-images.githubusercontent.com/42603919/162473639-80aa6086-b609-4334-8e91-c853645211f6.PNG" alt="캡처" style="zoom:50%;" />



### **해설**

#### 깊이 우선 탐색(DFS, Depth-First Search)

**깊이 우선 탐색이란**
루트 노드(혹은 다른 임의의 노드)에서 시작해서 다음 분기(branch)로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방법

- 미로를 탐색할 때 한 방향으로 갈 수 있을 때까지 계속 가다가 더 이상 갈 수 없게 되면 다시 가장 가까운 갈림길로 돌아와서 이곳으로부터 다른 방향으로 다시 탐색을 진행하는 방법과 유사하다.
- 즉, 넓게(wide) 탐색하기 전에 깊게(deep) 탐색하는 것이다.
- 사용하는 경우: 모든 노드를 방문 하고자 하는 경우에 이 방법을 선택한다.
- 깊이 우선 탐색(DFS)이 너비 우선 탐색(BFS)보다 좀 더 간단하다.
- 단순 검색 속도 자체는 너비 우선 탐색(BFS)에 비해서 느리다.

**깊이 우선 탐색(DFS)의 특징**

- 자기 자신을 호출하는 **순환 알고리즘**의 형태 를 가지고 있다.
- 전위 순회(Pre-Order Traversals)를 포함한 다른 형태의 트리 순회는 모두 DFS의 한 종류이다.
- 이 알고리즘을 구현할 때 가장 큰 차이점은, 그래프 탐색의 경우 **어떤 노드를 방문했었는지 여부를 반드시 검사**해야 한다는 것이다.
  - 이를 검사하지 않을 경우 무한루프에 빠질 위험이 있다.

[출처 : 절차대로 생각하고 객체로 코딩하기](https://codevang.tistory.com/303)

````java
class Solution {
    private int count;
	public int solution(int n, int[][] computers) {
		boolean[] visit = new boolean[n];
		// 전체 컴퓨터 방문
		for (int i = 0; i < n; i++) {
			// 이미 방문 도장이 찍혀있으면 가지 않음 
			if (!visit[i]) {
				// 첫 노드부터 재귀함수 시작
				dfs(n, i, computers, visit);
				count++;
			}
		}
		return count;
	}

	private void dfs(int n, int index, int[][] computers, boolean[] visit) {
		// 방문확인
		visit[index] = true;
		// 노드 방문
		for (int i = 0; i < n; i++) {
			// 연결된 노드, 자신 제외, 아직 방문기록이 없는 노드
			if (computers[index][i] == 1 && i != index && !visit[i]) {
				dfs(n, i, computers, visit);
			}
		}
	}
}
````

