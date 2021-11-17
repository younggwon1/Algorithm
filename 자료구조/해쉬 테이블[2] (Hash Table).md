# 해쉬 테이블[2] (Hash Table)

### 4. 자료 구조 해쉬 테이블의 장단점과 주요 용도

- 장점
  - 데이터 저장/읽기 속도가 빠르다. (**검색 속도가 빠르다.**)
  - 해쉬는 키에 대한 데이터가 있는지(**중복) 확인이 쉬움**
- 단점 
  - 일반적으로 저장공간이 좀더 많이 필요하다.
  - **여러 키에 해당하는 주소가 동일할 경우 <u>충돌</u>을 해결하기 위한 별도 자료구조가 필요함**
- 주요 용도
  - 검색이 많이 필요한 경우
  - 저장, 삭제, 읽기가 빈번한 경우
  - 캐쉬 구현시 (중복 확인이 쉽기 때문)



### 5. 충돌(Collision) 해결 알고리즘 (좋은 해쉬 함수 사용하기)

> 해쉬 테이블의 가장 큰 문제는 충돌(Collision)의 경우입니다. 이 문제를 충돌(Collision) 또는 해쉬 충돌(Hash Collision)이라고 부릅니다.

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
    
    public boolean saveData(String key, String value) {
        Integer address = this.hashFunc(key);
        if (this.hashTable[address] != null) {
            this.hashTable[address].value = value;
        } else {
            this.hashTable[address] = new Slot(value);
        }
        return true;
    }
    
    public String getData(String key) {
        Integer address = this.hashFunc(key);
        if (this.hashTable[address] != null) {
            return this.hashTable[address].value;
        } else {
            return null;
        }
    }
}
```



#### 기존 알고리즘의 문제점

=> 앞글자의 "D"를 기반으로 주소에 데이터를 삽입하기 때문에 데이터가 덮어 씌어진다.

```java
MyHash mainObject = new MyHash(20);
mainObject.saveData("DaveLee", "01022223333");
mainObject.saveData("fun-coding", "01033334444");
mainObject.saveData("David", "01044445555");
mainObject.saveData("Dave", "01055556666");
mainObject.getData("DaveLee");

=> 01055556666
```



### 5.1. Chaining 기법

- **개방 해슁 또는 Open Hashing** 기법 중 하나: **해쉬 테이블 저장공간 외**의 공간을 활용하는 기법
- **충돌이 일어나면, 링크드 리스트라는 자료 구조를 사용해서, 링크드 리스트로 데이터를 추가로 뒤에 연결시켜서 저장하는 기법**

<div class="alert alert-block" style="border: 1px solid #FFB300;background-color:#F9FBE7;font-size:1em;line-height:1.4em">
<font size="3em" style="font-weight:bold;color:#3f8dbf;">연습해보기</font><br><br>
기존 알고리즘에 Chaining 기법을 구현해보기 <br>

```java
public class MyHash {
    public Slot[] hashTable;
    
    public MyHash(Integer size) {
        this.hashTable = new Slot[size];
    }
    
    public class Slot {
        String key;
        String value;
        // 링크드리스트 포인터 값(next)
        Slot next;
        Slot(String key, String value) {
            this.key = key;
            this.value = value;
            this.next = null;
        }
    }
    
    public int hashFunc(String key) {
        return (int)(key.charAt(0)) % this.hashTable.length;
    }
    
    public boolean saveData(String key, String value) {
        Integer address = this.hashFunc(key);
        // 해당 주소에 이미 slot이 존재하면 (데이터가 존재하면)
        if (this.hashTable[address] != null) {
            // 내부 코드가 링크드 리스트일 수 있으므로 두가지 변수 선언
            Slot findSlot = this.hashTable[address];
            Slot prevSlot = this.hashTable[address];
            while (findSlot != null) {
                if (findSlot.key == key) {
                    findSlot.value = value;
                    return true;
                } else {
                    // 링크드 리스트 순회
                    prevSlot = findSlot;
                    findSlot = findSlot.next;
                }
            }
            prevSlot.next = new Slot(key, value);
        // 해당 주소에 slot이 존재하지 않으면 (데이터가 존재하지 않으면)
        } else {
            // 새로운 slot을 만들어 key, value를 저장
            this.hashTable[address] = new Slot(key, value);
        }
        return true;
    }
    
    public String getData(String key) {
        Integer address = this.hashFunc(key);
        // 해당 주소에 이미 slot이 존재하면 (데이터가 존재하면)
        if (this.hashTable[address] != null) {
            // 링크드 리스트 순회
            Slot findSlot = this.hashTable[address];
            while (findSlot != null) {
                if (findSlot.key == key) {
                    return findSlot.value;
                } else {
                    findSlot = findSlot.next;
                }
            }
            return null;
        // 해당 주소에 slot이 존재하지 않으면 (데이터가 존재하지 않으면)
        } else {
            return null;
        }
    }
}
```



#### 테스트

```java
MyHash mainObject = new MyHash(20);
mainObject.saveData("DaveLee", "01022223333");
mainObject.saveData("fun-coding", "01033334444");
mainObject.saveData("David", "01044445555");
mainObject.saveData("Dave", "01055556666");
mainObject.getData("Dave");

=> 01055556666
```



### 5.2. Linear Probing 기법

- **폐쇄 해슁 또는 Close Hashing** 기법 중 하나: **해쉬 테이블 저장공간 안**에서 충돌 문제를 해결하는 기법
- **충돌이 일어나면, 해당 hash address의 다음 address부터 맨 처음 나오는 빈 공간에 저장하는 기법**
  - 저장공간 활용도를 높이기 위한 기법

<div class="alert alert-block" style="border: 1px solid #FFB300;background-color:#F9FBE7;font-size:1em;line-height:1.4em">
<font size="3em" style="font-weight:bold;color:#3f8dbf;">연습해보기</font><br><br>
기존 알고리즘에 Linear Probing 기법을 구현해보기 <br>

```java
public class MyHash {
    public Slot[] hashTable;
    
    public MyHash(Integer size) {
        this.hashTable = new Slot[size];
    }
    
    public class Slot {
        String key;
        String value;
        Slot(String key, String value) {
            this.key = key;
            this.value = value;
        }
    }
    
    public int hashFunc(String key) {
        return (int)(key.charAt(0)) % this.hashTable.length;
    }
    
    public boolean saveData(String key, String value) {
        Integer address = this.hashFunc(key);
        if (this.hashTable[address] != null) {
            if (this.hashTable[address].key == key) {
                this.hashTable[address].value = value;
                return true;
            } else {
                Integer currAddress = address + 1;
                while (this.hashTable[currAddress] != null) {
                    if (this.hashTable[currAddress].key == key) {
                        this.hashTable[currAddress].value = value;
                        return true;
                    } else {
                        currAddress++;
                        if (currAddress >= this.hashTable.length) {
                            return false;
                        }                        
                    }
                }
                this.hashTable[currAddress] = new Slot(key, value);
                return true;
            }
        } else {
            this.hashTable[address] = new Slot(key, value);
        }
        return true;
    }
    
    public String getData(String key) {
        Integer address = this.hashFunc(key);
        if (this.hashTable[address] != null) {
            if (this.hashTable[address].key == key) {
                return this.hashTable[address].value;
            } else {
                // 참고: 다음 코드를 수정합니다.
                // Integer currAddress = address + 1;                 
                // 예외 케이스로, 키에 해당하는 주소가 가장 마지막 슬롯일 경우, 
                // this.hashTable[address + 1] 에 해당하는 배열은 없기 때문에, 
                // 예외 케이스에서도 동작하도록 currAddress 는 address 만 대입하고 진행합니다
                Integer currAddress = address; // 수정 
                while (this.hashTable[currAddress] != null) {
                    if (this.hashTable[currAddress].key == key) {
                        return this.hashTable[currAddress].value;
                    } else {
                        currAddress++;
                        if (currAddress >= this.hashTable.length) {
                            return null;
                        }
                    }
                }
                return null;
            }
        } else {
            return null;
        }
    }
}
```



```java
MyHash mainObject = new MyHash(20);
mainObject.saveData("DaveLee", "01022223333");
mainObject.saveData("fun-coding", "01033334444");
mainObject.saveData("David", "01044445555");
mainObject.saveData("Dave", "01055556666");
mainObject.getData("fun-coding");

=> 01033334444
```