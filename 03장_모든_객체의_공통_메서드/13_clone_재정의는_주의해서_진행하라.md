## 아이템 13. clone 재정의는 주의해서 진행하라

> clone 메서드의 일반 규약은 허술하다.

### cloneable

cloneable 인터페이스에는 clone이 없다.

clone은 Object에 선언된 메서드이다.

*그럼 cloneable의 역할이 무엇이죠?*<br>&rarr; **Object의 *protected* 메서드인 clone의 동작 방식을 결정한다.**

cloneable을 구현한 클래스는 public으로 clone이 잘 될것이라 예상한다.

<br>

### 허술한 clone 일반 규약

- x.clone() != x 는 참이다.
- x.clone().getClass() == x.getClass() 는 참이다.
- x.clone().equals(x) 는 참이다. (필수는 아님..)

<br>

### clone 재정의 문제점

#### 1. clone이 super.clone()이 아니라 그냥 생성자로 인스턴스 만들어서 리턴해도 모른다.

```java
@Override
public Hello clone () {
  Hello result = (Hello) super.clone();
  return result;
}

@Override
public Hello clone () {
  Hello result = (Hello)new SuperClass();
  return result;
}
```

#### 2. 클래스가 가변 객체를 참조하는 경우 복제품에서 원본 데이터를 수정하게 될 수도 있다.

```java
public class Stack implements Cloneable {
  private Object[] elements;
  private int size = 0;
  private static final int DEFAULT_INITIAL_CAPACITY = 16;

  public Stack() {
    this.elements = new Object[DEFAULT_INITIAL_CAPACITY];
  }

  public void push(Object e) {
    ensureCapacity();
    elements[size++] = e;
  }

  public Object pop() {
    if (size == 0)
      throw new EmptyStackException();
    Object result = elements[--size];
    elements[size] = null; // 다 쓴 참조 해제
    return result;
  }

  private void ensureCapacity() {
    if (elements.length == size) {
      elements = Arrays.copyOf(elements, 2 * size + 1);
    }
  }

  @Override
  public Stack clone() {
		try {
      Stack result = (Stack) super.clone();
      result.elements = elements.clone(); // clone을 재귀호출해서 해결해야 한다.
      return result;
    } catch (CloneNotSupportedException) {
     	throw new AssertionError(); 
    }
  }
}
```

#### 3. 2번을 해결하기 위해 clone을 재귀호출 하는 경우 final 필드를 사용하지 못하는 문제가 발생한다.

<br>

### 복사 생성자, 복사 팩터리

> 더 나은 대안을 제공한다.

```java
class Hello {
	public Hello (Hello hello) {};
 	public static Hello newInstance(Hello hello) {}; 
}
```

***이거 씁시다.***

