## 아이템 26. row 타입은 사용하지 말라

### 제네릭 클래스, 제네릭 인터페이스

> 선언부에 타입 매개변수가 있는 경우 제네릭 이라고 한다.

**제네릭 타입**

보통 제네릭 클래스, 제네릭 인터페이스를 제네릭 타입이라고 한다.

List 인터페이스의 경우 `List<E>` 가 정식 명칭.

여기서 `List` 을 row type이라 한다.

<br>

### row type

> 자바5에서 제네릭이 추가되었다.
>
> 그전에는 row type을 매번 형변환 해서 사용해야 했다.

```java
private final Collection stamps = ...;
```

- 이렇게 사용하게 되면 stamp에 뭘 넣어도 에러없이 컴파일 된다.
- 제네릭의 안정성, 표현력의 장점이 사라진다.

```java
private final Collection<Stamp> stamps = ...;
```

꼭 타입을 적어주자!

<br>

### 와일드카드 ?

```java
static int numElementsInCommon (Set<?> s1, Set<?> s2) { ... }
```

만약에 타입을 몰라도 되고싶으면 와일드카드(물음표 '?')를 사용해라

*row type이랑은 뭐가 다릅니까?* <br> &rarr; 이친구 null 빼고 아무것도 못집어 넣는다. <br>

*그러면 어떻게 쓰란 말이요* <br> &rarr; method parameter로 사용합니다.

<br>

###  예외

- class 리터럴에는 row type을 사용해야 한다.

- instanceof 연산자 사용시에는 타입을 적어주나 row type을 쓰나 똑같이 동작한다.<br>

  ``` java
  if (o instanceof Set) {
  	Set<?> s = (Set<?>) o;
  }
  ```

<br>

### 용어정리

| 한글                     | 영어                    | code                               | 아이템 |
| ------------------------ | ----------------------- | ---------------------------------- | ------ |
| 매개변수화 타입          | parameterized type      | `List<String>`                     | 26     |
| 실제 타입 매개변수       | actual type parameter   | `String`                           | 26     |
| 제네릭 타입              | generic type            | `List<E>`                          | 26, 29 |
| 정규 타입 매개변수       | formal type parameter   | `E`                                | 26     |
| 비한정적 와일드카드 타입 | unbounded wildcard type | `List<?>`                          | 26     |
| 로 타입                  | raw type                | `List`                             | 26     |
| 한정적 타입 매개변수     | bounded type parameter  | `<E extends Number>`               | 29     |
| 재귀적 타입 한정         | recursive type bound    | `<T extends Comparable<T>>`        | 30     |
| 한정적 와일드카드 타입   | bounded wildcard type   | `List<? extends Number>`           | 31     |
| 제네릭 메서드            | generic method          | `static <E> List<E> asList(E[] a)` | 30     |
| 타입 토큰                | type token              | `String.class`                     | 33     |

