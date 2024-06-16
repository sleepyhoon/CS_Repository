# 자바 컬렉션 (Java Collections)

자바 컬렉션은 데이터 구조를 관리하고 조작하는 다양한 클래스를 제공하는 프레임워크입니다. 자바 컬렉션 프레임워크는 데이터를 저장, 검색, 수정, 삭제하는 방법을 표준화하여 데이터 관리의 복잡성을 줄여줍니다.

- List, Set, Queue, Map 등의 다양한 Collection이 존재한다.

### Stream API를 사용하는 이유

**코드 간결성 및 가독성**

- 스트림 API를 사용하면 컬렉션 데이터를 처리하는 코드를 더 간결하고 읽기 쉽게 만들 수 있습니다. 람다 표현식과 메서드 참조를 활용하여 데이터를 필터링, 매핑, 축소하는 작업을 직관적으로 작성할 수 있습니다.

```java
List<String> myList = Arrays.asList("apple", "banana", "cherry", "date");
List<String> result = myList.stream()
                            .filter(s -> s.startsWith("a"))
                            .map(String::toUpperCase)
                            .collect(Collectors.toList());
```

**게으른 연산 (Lazy Evaluation)**

- 스트림의 중간 연산은 게으르게 평가됩니다. 즉, 최종 연산이 호출될 때까지 중간 연산은 실제로 수행되지 않으며, 필요한 경우에만 계산이 이루어집니다. 이는 성능 최적화에 도움이 됩니다.

```java
List<String> myList = Arrays.asList("apple", "banana", "cherry", "date");
Stream<String> stream = myList.stream()
                              .filter(s -> {
                                  System.out.println("filtering: " + s);
                                  return s.startsWith("a");
                              });
System.out.println("Stream created");
stream.forEach(System.out::println);
```

**병렬 처리**

- 스트림 API는 병렬 처리를 간단하게 구현할 수 있도록 도와줍니다. `parallelStream()` 메서드를 사용하면 병렬 스트림을 생성할 수 있으며, 이를 통해 데이터 처리를 병렬로 수행할 수 있습니다.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
int sum = numbers.parallelStream()
                 .filter(n -> n % 2 == 0)
                 .mapToInt(Integer::intValue)
                 .sum();
```

**스트림 파이프라인**

- 스트림은 데이터를 처리하는 파이프라인을 구축하는데 이상적입니다. 데이터를 필터링, 변환, 축소하는 작업을 연속적으로 연결할 수 있습니다. 이러한 파이프라인은 코드를 읽기 쉽고 유지 보수하기 쉽게 만듭니다.

```java
List<String> myList = Arrays.asList("apple", "banana", "cherry", "date");
long count = myList.stream()
                   .filter(s -> s.startsWith("a"))
                   .count();
```