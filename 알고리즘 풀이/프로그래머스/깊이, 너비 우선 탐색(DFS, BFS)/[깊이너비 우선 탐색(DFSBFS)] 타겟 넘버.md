# [깊이/너비 우선 탐색(DFS/BFS)] 타겟 넘버

[타겟 넘버](https://programmers.co.kr/learn/courses/30/parts/12421)

###### 문제 설명

n개의 음이 아닌 정수들이 있습니다. 이 정수들을 순서를 바꾸지 않고 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.

```
-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3
```

사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
- 각 숫자는 1 이상 50 이하인 자연수입니다.
- 타겟 넘버는 1 이상 1000 이하인 자연수입니다.

##### 입출력 예

| numbers         | target | return |
| --------------- | ------ | ------ |
| [1, 1, 1, 1, 1] | 3      | 5      |
| [4, 1, 2, 1]    | 4      | 2      |

##### 입출력 예 설명

**입출력 예 #1**

문제 예시와 같습니다.

**입출력 예 #2**

```
+4+1-2+1 = 4
+4-1+2-1 = 4
```

- 총 2가지 방법이 있으므로, 2를 return 합니다.





### **해설**

[출처 : 시작의 반/ G_GI](https://tmdrl5779.tistory.com/200)

````java
class Solution {
    int count = 0;
    public int solution(int[] numbers, int target) {
        int answer = 0;
        dfs(numbers, 0, target, 0);
        answer = this.count;
        
        return answer;
    }
    
    public void dfs(int[] numbers, int depth, int target, int result){
        if (depth == numbers.length){
            if (target == result){
                this.count++;
            }
            return;
        }
        
        int add = result + numbers[depth];
        int sub = result - numbers[depth];
        
        dfs(numbers, depth+1, target, add);
        dfs(numbers, depth+1, target, sub);
        
    }
}
````