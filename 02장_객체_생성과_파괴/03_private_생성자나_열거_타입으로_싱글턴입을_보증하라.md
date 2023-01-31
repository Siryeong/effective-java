## 아이템 3. private 생성자나 열거 타입으로 싱글턴임을 보증하라

### 싱글턴 만들기

> 싱글턴, 오직 하나의 인스턴스만

- private 생성자
- instance는 public static으로 접근

<br>

#### public field로 들고오기

```java
// instance 바로 들고오기
public class SingleBungle {
  public static final SingleBungle INSTANCE = new SingleBungle();
  private SingleBungle() { ... }
  
  public void leaveTheBuilding() { ... }
}
```

##### 장점

1. api만 봐도 싱글턴인걸 알 수 있다.

2. 간결하다.

<br>

#### static factory method로 들고오기

```java
// static factory method로 들고오기
public class SingleBungle {
  private static final SingleBungle INSTANCE = new SingleBungle();
  private SingleBungle() { ... }
  public static SingleBungle getInstance() { return INSTANCE; }
  
  public void leaveTheBuilding() { ... }
}
```

##### 장점

1. 싱글턴 아니게 만들기 편하다.
2. static factory &rarr; generic singleton factory로 만들 수 있다.
3. getInstance를 supplier로 사용할 수 있다.

<br>

#### Serialize 문제

싱글턴을 직렬화 하려면 readResolve 메서드를 제공해야 한다.

안그러면 역직렬화 할때마다 새로운 인스턴스가 만들어진다.

<br>

#### Enum Type으로 만들기

```java
// enum singleton
public enum SingleBungle {
  INSTANCE;
  
  public void leaveTheBuilding() { ... }
}
```

##### 장점

1. Serialize가 간결하다.
2. 좀 이상하긴 한데, 대부분의 상황에서 가장 좋은 싱글턴 만들기 방법이다.