# [힙(Heap)] 더 맵게

[더 맵게](https://programmers.co.kr/learn/courses/30/lessons/42626)

###### 문제 설명

매운 것을 좋아하는 Leo는 모든 음식의 스코빌 지수를 K 이상으로 만들고 싶습니다. 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 Leo는 스코빌 지수가 가장 낮은 두 개의 음식을 아래와 같이 특별한 방법으로 섞어 새로운 음식을 만듭니다.

```
섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)
```

Leo는 모든 음식의 스코빌 지수가 K 이상이 될 때까지 반복하여 섞습니다.
Leo가 가진 음식의 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수 K가 주어질 때, 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞어야 하는 최소 횟수를 return 하도록 solution 함수를 작성해주세요.

##### 제한 사항

- scoville의 길이는 2 이상 1,000,000 이하입니다.
- K는 0 이상 1,000,000,000 이하입니다.
- scoville의 원소는 각각 0 이상 1,000,000 이하입니다.
- 모든 음식의 스코빌 지수를 K 이상으로 만들 수 없는 경우에는 -1을 return 합니다.

##### 입출력 예

| scoville             | K    | return |
| -------------------- | ---- | ------ |
| [1, 2, 3, 9, 10, 12] | 7    | 2      |

##### 입출력 예 설명

1. 스코빌 지수가 1인 음식과 2인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.
   새로운 음식의 스코빌 지수 = 1 + (2 * 2) = 5
   가진 음식의 스코빌 지수 = [5, 3, 9, 10, 12]
2. 스코빌 지수가 3인 음식과 5인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.
   새로운 음식의 스코빌 지수 = 3 + (5 * 2) = 13
   가진 음식의 스코빌 지수 = [13, 9, 10, 12]

모든 음식의 스코빌 지수가 7 이상이 되었고 이때 섞은 횟수는 2회입니다.



### **해설**

````java
import java.util.*;

class Solution {
    
    public int solution(int[] scoville, int K) {
        // 최소 횟수
        int answer = 0;
        // 섞은 음식의 스코빌 지수 변수 선언
        int mixinScoville = 0;
    
        // 배열 -> ArrayList 선언
        ArrayList<Integer> newScovilleList = new ArrayList<Integer>();
        for(int k = 0; k < scoville.length; k++) {
            newScovilleList.add(scoville[k]);
        }
        
        for(int j = 1; j <= newScovilleList.size(); j++) {
            // 섞은 음식의 스코빌 지수 >= K 인지 확인
            if (mixinScoville < K) {
                answer++;
                // 배열 오름 차순 메서드 호출
                Collections.sort(newScovilleList);
                // 섞은 음식의 스코빌 지수 구하기
                mixinScoville = newScovilleList.get(0) + (newScovilleList.get(1)*2);
                newScovilleList.remove(0);
                newScovilleList.remove(0);
                newScovilleList.add(mixinScoville);
            } else {
                return answer;
            }            
        }
        return answer;
    }
}
````

```apl
정확성  테스트
테스트 1 〉실패 (0.26ms, 83.9MB)
테스트 2 〉통과 (0.19ms, 76MB)
테스트 3 〉실패 (0.25ms, 77.1MB)
테스트 4 〉실패 (0.26ms, 75.3MB)
테스트 5 〉실패 (0.24ms, 79.6MB)
테스트 6 〉실패 (4.32ms, 65.7MB)
테스트 7 〉실패 (3.61ms, 83.7MB)
테스트 8 〉실패 (0.68ms, 67.5MB)
테스트 9 〉실패 (0.61ms, 75.7MB)
테스트 10 〉실패 (3.16ms, 73.8MB)
테스트 11 〉실패 (2.44ms, 75.3MB)
테스트 12 〉실패 (7.24ms, 78.4MB)
테스트 13 〉실패 (4.24ms, 74.5MB)
테스트 14 〉실패 (0.26ms, 73.7MB)
테스트 15 〉실패 (6.74ms, 76.9MB)
테스트 16 〉통과 (0.26ms, 72.4MB)
효율성  테스트
테스트 1 〉실패 (시간 초과)
테스트 2 〉실패 (시간 초과)
테스트 3 〉실패 (시간 초과)
테스트 4 〉실패 (시간 초과)
테스트 5 〉실패 (시간 초과)
```

**=> 코드 작성에 대한 효율이 좋지 않아 다른 방안으로 고안**



**우선순위 큐**를 사용

[기본적으로 정수형에 대해서는 **오름차순 정렬**을 한다.](https://tosuccess.tistory.com/155)

자바에서 우선순위 큐를 사용하려면 java.util.PriorityQueue를 import 해야한다.

- [PriorityQueue 사용법](https://docs.oracle.com/javase/7/docs/api/java/util/PriorityQueue.html)

 ````java
pq.add(); // 값 추가
pq.poll(); // 첫번째 값 반환 후 제거 (비어있으면 null)
pq.clear(); // 비우기
pq.isEmpty(); // 비어있는지 확인
pq.remove(); // 첫번째 값 제거
pq.peek(); // 첫번째 값 반환
 ````



1. 우선순위 큐(PriorityQueue) 객체 생성

   ````java
   PriorityQueue<자료형> priorityQueue = new PriorityQueue<>();
   ````

2. 우선순위 큐에 요소 추가

   (* add와 offer의 차이점 : Collection.add(E), Queue.offer(E))

   ````java
   priorityQueue.offer(element);
   ````

3. 우선순위 큐에서 맨앞의 값을 읽어옴

   ````java
   priorityQueue.peek();
   ````

4. 우선순위 큐에서 맨앞의 값을 읽어오고 삭제

   ````java
   priorityQueue.poll();
   ````

5. 우선순위 큐의 크기

   ````java
   priorityQueue.size();
   ````



````java
import java.util.*;

class Solution {
    
    public int solution(int[] scoville, int K) {
        int answer = 0;
        // 우선순위 큐
        PriorityQueue<Integer> pq = new PriorityQueue();
        // 우선순위 큐에 음식의 스코빌 지수 추가
        for(int s : scoville){
            pq.offer(s);
        }
        // 가장 낮은 스코빌 지수가 K 이상일때까지 반복
        while(pq.peek() < K){
            // K 이상으로 만들 수 없는 경우
            if(pq.size() <= 1) return -1;
            
            int first = pq.poll();
            int second = pq.poll();
            
            // 두 음식 섞기
            int mix = first + second * 2;
            pq.offer(mix);
            answer++;
        }
        return answer;
    }
}
````

