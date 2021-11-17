## 해쉬 테이블[1] (Hash Table)

### 1. 해쉬 테이블
  - **키(Key)에 데이터(Value)를 매핑할 수 있는 데이터 구조**
  - 해쉬 함수를 통해, 배열에 키에 대한 데이터를 저장할 수 있는 주소(인덱스 번호)를 계산
  - Key를 통해 바로 데이터가 저장되어 있는 주소를 알 수 있으므로, 저장 및 탐색 속도가 획기적으로 빨라짐
  - 미리 해쉬 함수가 생성할 수 있는 주소(인덱스 번호)에 대한 공간을 배열로 할당한 후, 키에 따른 데이터 저장 및 탐색 지원
  - 기본연산으로는 탐색(Search), 삽입(Insert), 삭제(Delete)가 있다.
  - 해쉬 테이블은 각각의 Key 값에 해쉬 함수를 적용해 배열의 고유한 index를 생성하고, 이 index를 활용해 값을 저장하거나 검색하게 된다. 여기서 실제 값이 저장되는 장소를 버킷 또는 슬롯이라고 한다.
### 2. 알아둘 용어
* **해쉬 함수(Hash Function)**: 임의의 데이터를 고정된 길이의 값으로 리턴해주는 함수
  - 해쉬 (Hash), 해쉬 값(Hash Value), 또는 해쉬 주소(Hash Address): 해싱 함수를 통해 리턴된 고정된 길이의 값
* **해쉬 테이블(Hash Table)**: 키 값의 연산에 의해 직접 접근이 가능한 데이터 구조
  - 슬롯(Slot): 해쉬 테이블에서 한 개의 데이터를 저장할 수 있는 공간
<img src="https://www.fun-coding.org/00_Images/hashtable2021.jpg" />



### 3. 간단한 해쉬 예



#### 3.1. hash table 클래스 만들기

```java
public class MyHash {
    // 각각의 데이터를 저장할 수 있는 slot을 기반으로 한 해쉬 테이블
    // 해쉬 테이블은 배열로 할당되어있다.
    public Slot[] hashTable;
    
    // 미리 배열의 사이즈를 할당할 수 있도록 구성
    public MyHash(Integer size) {
        this.hashTable = new Slot[size];
    }
    
    // 내부 클래스로 slot을 정의
    // 각각의 slot에는 값이 저장
    public class Slot {
        String value;
        Slot(String value) {
            this.value = value;
        }
    }
}
```



#### 3.2. 초간단 해쉬 함수를 만들어봅니다.

---

**[ Hash 함수(해쉬 함수) ]**

**해쉬 함수에서 중요한 것은 고유한 인덱스 값을 설정하는 것**이다. 해쉬 테이블에 사용되는 대표적인 해쉬 함수로는 아래의 4가지가 있다.

1. **Division Method**: 나눗셈을 이용하는 방법으로 입력값을 테이블의 크기로 나누어 계산한다.( 주소 = 입력값 % 테이블의 크기) 테이블의 크기를 소수로 정하고 2의 제곱수와 먼 값을 사용해야 효과가 좋다고 알려져 있다.
2. **Digit Folding**: 각 Key의 문자열을 ASCII 코드로 바꾸고 값을 합한 데이터를 테이블 내의 주소로 사용하는 방법이다.
3. **Multiplication Method**: 숫자로 된 Key값 K와 0과 1사이의 실수 A, 보통 2의 제곱수인 m을 사용하여 다음과 같은 계산을 해준다. h(k)=(kAmod1) × m
4. **Univeral Hashing**: 다수의 해쉬 함수를 만들어 집합 H에 넣어두고, 무작위로 해쉬 함수를 선택해 해쉬값을 만드는 기법이다.

---

- Key 가 문자열일 때, 문자열의 앞 글자를 숫자로 변환해서, **Division 기법**을 사용하여, Key에 대한 주소(인덱스 번호) 계산
   - **Division 기법**: 가장 간단한 해쉬 함수 중 하나로, 나누기를 통해, 나머지 값을 사용하는 기법

  ```java
  String name = "DaveLee";
  name.charAt(0);
  => D
     
     (int)(name.charAt(0));
     => 68
     
     String name = "DaveLee";
     (int)(name.charAt(0)) % 20
     => 8
     ```
   
     
#### 3.3 해쉬 테이블 클래스에 해쉬 함수 추가
```java
public class MyHash {
    public Slot[] hashTable;
    
    public MyHash(Integer size) {
        this.hashTable = new Slot[size];
    }
    
    public class Slot {
        String value;
        Slot(String value) {
            this.value = value;
        }
    }
    
    // 해쉬 함수 선언
    public int hashFunc(String key) {
        return (int)(key.charAt(0)) % this.hashTable.length;
    }
}
```



#### 3.3 해쉬 테이블 클래스에 데이터 저장 메서드 추가
#### 해쉬 테이블 클래스에 saveData() 메서드 추가



---

##### 참고: 객체 배열

- 객체 배열 선언시, 각 배열의 아이템은 각 객체를 참조할 수 있는 주소를 담을 수 있는 공간만 할당
  - 각 아이템 생성시, 별도로 각 객체를 생성해줘야 함
  - 즉, 객체 배열 선언시, 각 생성할 객체를 가리킬 주소만 저장할 공간을 배열로 만드는 것임

```java
public class Slot {
    String value;
    Slot(String value) {
        this.value = value;
    }
}

// 20개의 슬롯 객체를 배열로 만든 것처럼 보이지만, 각각의 ITEM은 NULL로 나온다.
// 주소 공간만 할당해 놓은 것이다.!! (공간은 생성)
Slot[] hashTable = new Slot[20];
System.out.println(hashTable[0]);

=> null
```



```java
public class Slot {
    String value;
    Slot(String value) {
        this.value = value;
    }
}

// 주소 공간을 만든 후 , 각각의 Item은 별도로 Slot을 생성해야한다.
Slot[] hashTable = new Slot[20];
hashTable[0] = new Slot("test");

System.out.println(hashTable[0]);
System.out.println(hashTable[0].value);

=> REPL.$JShell$40$Slot@5a20858a
   test
```

----



```java
public class MyHash {
    public Slot[] hashTable;
    
    public MyHash(Integer size) {
        this.hashTable = new Slot[size];
    }
    
    public class Slot {
        String value;
        Slot(String value) {
            this.value = value;
        }
    }
    
    public int hashFunc(String key) {
        return (int)(key.charAt(0)) % this.hashTable.length;
    }
    
    // 데이터를 저장하는 메서드
    public boolean saveData(String key, String value) {
        // key와 value를 받아 해당 데이터를 저장할 수 있는 주소를 가지고 온다.
        Integer address = this.hashFunc(key);
        // 만약 해쉬 테이블 배열에 해당 주소가 null이 아니라면(데이터가 저장, slot이 생성)
        // 이미 객체가 있으니 value만 바꿔줌
        if (this.hashTable[address] != null) {
            this.hashTable[address].value = value;
        // 해당 주소가 slot이 만들어지지 않았으면 slot 객체를 생성
        } else {
            this.hashTable[address] = new Slot(value);
        }
        return true;
    }
}
```



#### 3.4. 해쉬 테이블 클래스에 key 에 대한 데이터를 가져오는 메서드 추가
````java
public class MyHash {
    public Slot[] hashTable;
    
    public MyHash(Integer size) {
        this.hashTable = new Slot[size];
    }
    
    public class Slot {
        String value;
        Slot(String value) {
            this.value = value;
        }
    }
    
    public int hashFunc(String key) {
        return (int)(key.charAt(0)) % this.hashTable.length;
    }
    
    public boolean saveData(String key, String value) {
        Integer address = this.hashFunc(key);
        if (this.hashTable[address] != null) {
            this.hashTable[address].value = value;
        } else {
            this.hashTable[address] = new Slot(value);
        }
        return true;
    }
    
    // 특정 key에 해당하는 데이터를 가져오는 메서드
    public String getData(String key) {
        // key와 value를 받아 해당 데이터를 저장할 수 있는 주소를 가지고 온다.
        Integer address = this.hashFunc(key);
        // 만약 해쉬 테이블 배열에 해당 주소가 null이 아니라면(데이터가 저장, slot이 존재)
        // 해당 value를 반환
        if (this.hashTable[address] != null) {
            return this.hashTable[address].value;
        // 해당 주소에 객체(데이터)가 없다면 null을 반환
        } else {
            return null;
        }
    }
}
````



#### 3.5. 테스트
```java
MyHash mainObject = new MyHash(20);
mainObject.saveData("DaveLee", "01022223333");
mainObject.saveData("fun-coding", "01033334444");
mainObject.getData("fun-coding");

=> 01033334444
```





참고

[**해시테이블(HashTable)이란?**](https://mangkyu.tistory.com/102)