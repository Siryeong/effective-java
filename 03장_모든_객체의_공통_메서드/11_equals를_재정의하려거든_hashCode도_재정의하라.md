## 아이템 11. equals를 재정의하려거든 hashCode도 재정의하라

### Object 명세

> equals(Object)가 두 객체를 같다고 했으면 hashCode도 같은 값을 반환해야 한다.

같은 객체는 같은 hashCode를 반환하도록 명세되어 있다.

hashCode 재정의를 하지 않으면 HashMap, HashSet 사용시 문제가 발생할 수 있다.

<br>

### 좋은 HashCode에 대해서

해시코드 계산법

1. 기본 타입 &rarr; Type.hashCode 사용
2. 참조 타입 &rarr; null이면 0, 아니면 xxx.hashCode 사용
3. 배열 &rarr; empty or null이면 0, 아니면 Arrays.hashCode 사용

필드마다 해시코드 구하고 31곱하고 더하고.. 반복

```java
public class Hello {
  private int a;
  private World b;
  private int[] c;
  
  @Override 
  public int hashCode() {
    int result = Integer.hashCode(a);
    result = 31 * result + b.hashCode();
    result = 31 * result + Arrays.hashCode(c);
    
    return result;
  }
}
```

***이게 국룰이다.***

<br>

#### 조금 느린 방법

```java
return Objects.hash(a, b, c);
```

<br>

#### Lazy init

> Thread Safe를 신경 써줘야 한다..

```java
private int hashCode; // 0

@Override 
public int hashCode() {
  int result = hashCode;
  if(reseult == 0) {
  	result = Integer.hashCode(a);
  	result = 31 * result + b.hashCode();
  	result = 31 * result + Arrays.hashCode(c);
    hashCode = result;
  }
  return result;
}
```

<br>

### 주의사항

- 성능 높이겠다고 필수로 들어가야 하는 필드 생략하지 말것.
- hashCode 생성 규칙을 api 사용자에게 자세히 공표하지 말것.
