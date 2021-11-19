# 해쉬 테이블[3] (Hash Table)

### 5.3. 빈번한 충돌을 개선하는 기법

- **해쉬 테이블 저장공간을 확대** 및 **해쉬 함수 재정의**

```java
String name = "Dave";
int key = 0;
for (int i = 0; i < name.length(); i++) {
    key += name.charAt(i);
}

(int)(key) % 200

=> 184
```



----

#### 참고: JAVA HashMap

- 해쉬 테이블 구조를 활용하여 구현된 JAVA Collection Framework 에 속한 클래스

=>  JAVA 문법 강의는 아니지만, 참고로 관련 기능을 가진 클래스를 소개하며, 이후 알고리즘 강의에서 코드 구현에 필요한 자료구조 기능으로 HashMap 을 활용할 예정



```java
import java.util.HashMap;

HashMap<Integer, String> map1 = new HashMap();
map1.put(1, "사과");
map1.put(2, "바나나");
map1.put(3, "포도");

HashMap<String, String> map2 = new HashMap();
map2.put("DaveLee", "01033334444");
map2.put("Dave", "01032221111");
map2.put("David", "0104445555");

map1.get(2);
=> 바나나
map2.get("Dave");
=> 01032221111 
```



----