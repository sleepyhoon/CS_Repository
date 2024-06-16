# Java Collections 정리

### ArrayList

- 선언은 다음과 같이 선언한다

```java
ArrayList list1 = new ArrayList(10);

ArrayList<String> anotherArrayList = new ArrayList<>();
```

- 각 원소에 접근하고 싶다면 []을 사용하는게 아니라 get()을 사용해야 한다.

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        // ArrayList 생성
        ArrayList<String> arrayList = new ArrayList<>();

        // 요소 추가
        arrayList.add("Apple");
        arrayList.add("Banana");
        arrayList.add("Orange");

        // 인덱스로 요소에 접근
        String firstElement = arrayList.get(0);
        String secondElement = arrayList.get(1);

        // 출력
        System.out.println("첫 번째 요소: " + firstElement);
        System.out.println("두 번째 요소: " + secondElement);
    }
}
```

자세한 메소드들은 추후에 찾아보도록 하자.

### Linkedlist vs Arraylist

| 컬렉션 | 읽기(접근시간) | 추가/삭제 | 비고 |
| --- | --- | --- | --- |
| Arraylist | 빠르다 | 느리다 | 순차적인 추가삭제는 더 빠름. 비효율적인 메모리 사용 |
| linkedlist | 느리다. | 빠르다. | 데이터가 많을수록 접근성이 떨어진다. |

다루고자 하는 데이터가 개수가 변하지 않는다면 arraylist를 사용하는게 이상적이고, linkedlist의 경우 데이터의 개수의 변경이 잦다면 사용하는게 이상적이다.

그래서 두 클래스의 장점을 이용해서 조합해서 사용하는 것도 좋다. 컬렉션 프레임워크에 속한 대부분의 컬렉션 클래스들은 서로 변환이 가능한 연산자를 제공하므로 이를 이용하면 간단히 다른 컬렉션 클래스로 데이터를 옮길 수 있다.

```java
ArrayList al = new ArrayList(10000);
for(int i=0;i<10000;i++) al.add(i+"");
LinkedList ll = new LinkedList(al); // 바로 전환이 가능하다.
for(int i=0;i<10000;i++) ll.add(500,"X");
```

```java
ArrayList<String> arrayList = new ArrayList<>();
// arrayList에 요소 추가

LinkedList<String> linkedList = new LinkedList<>(arrayList);
```

## TreeMap, TreeSet

**`TreeMap`**과 **`TreeSet`**은 Java 컬렉션 프레임워크의 일부로서, 이진 검색 트리(binary search tree)를 기반으로 한 자료 구조를 사용하여 데이터를 저장합니다.

### **TreeMap:**

- **`TreeMap`**은 key-value 쌍을 저장하는 자료 구조입니다.
- 키(key)는 중복되지 않으며 정렬됩니다.
- 내부적으로 레드-블랙 트리(red-black tree)를 사용하여 키를 정렬하고 관리합니다.
- 키(key)를 기반으로 검색, 삽입, 삭제 등의 작업을 수행할 수 있습니다.
- 시간 복잡도:
    - 평균적으로는 O(log n)입니다.
    - 최악의 경우에도 O(log n)입니다.
- 관련 메서드
    1. **`put(K key, V value)`**: 지정된 키와 값으로 맵에 매핑을 추가합니다.
    2. **`get(Object key)`**: 지정된 키에 매핑된 값을 반환합니다.
    3. **`remove(Object key)`**: 지정된 키와 연결된 매핑을 맵에서 제거합니다.
    4. **`containsKey(Object key)`**: 맵에 지정된 키가 있는지 확인합니다.
    5. **`keySet()`**: 맵의 모든 키를 포함하는 **`Set`**을 반환합니다.
    6. **`values()`**: 맵의 모든 값들을 포함하는 **`Collection`**을 반환합니다.
    7. **`entrySet()`**: 맵의 모든 키-값 매핑을 포함하는 **`Set`**을 반환합니다.

### **TreeSet:**

- **`TreeSet`**은 중복되지 않는 요소들의 집합을 저장하는 자료 구조입니다.
- 요소들은 정렬됩니다.
- 내부적으로 레드-블랙 트리(red-black tree)를 사용하여 요소를 정렬하고 관리합니다.
- 요소를 기반으로 검색, 삽입, 삭제 등의 작업을 수행할 수 있습니다.
- 시간 복잡도:
    - 평균적으로는 O(log n)입니다.
    - 최악의 경우에도 O(log n)입니다.
- 관련 메서드
    1. **`add(E e)`**: 지정된 요소를 세트에 추가합니다.
    2. **`remove(Object o)`**: 세트에서 지정된 요소를 제거합니다.
    3. **`contains(Object o)`**: 세트에 지정된 요소가 있는지 확인합니다.
    4. **`isEmpty()`**: 세트가 비어 있는지 확인합니다.
    5. **`size()`**: 세트의 크기를 반환합니다.
    6. **`clear()`**: 세트의 모든 요소를 제거합니다.
    7. **`iterator()`**: 세트를 탐색하는 데 사용할 수 있는 반복자를 반환합니다.

둘다 정렬의 기능을 하는 map, set이다. 정렬을 하지 않는다면 기본적인 hashmap이나 set이 더 실행속도가 빠르니까 생각해서 사용하자.

### 번외 : **ConcurrentHashMap**

[https://velog.io/@alsgus92/ConcurrentHashMap의-Thread-safe-원리](https://velog.io/@alsgus92/ConcurrentHashMap%EC%9D%98-Thread-safe-%EC%9B%90%EB%A6%AC) : 자세히 분석은 다른 페이지에서 진행.