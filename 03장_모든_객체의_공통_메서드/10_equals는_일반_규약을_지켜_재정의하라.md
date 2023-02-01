## 아이템 10. equals는 일반 규약을 지켜 재정의하라

### equals 재정의 하지 말아야될 상황

- 각 인스턴스가 본질적으로 고유한 경우. 이를테면, Thread 같은얘들.
- 인스턴스의 logical equality를 검사할 일이 없는 경우.
- 상위클래스의 equals가 하위 클래스에도 딱인경우.
- private class 혹은 package-private class 이고 equals 호출할 일이 없는 경우.

<br>

### equals를 재정의 해야 하는 상황

- logical equality를 확인해야 하는 경우

<br>

### equals 재정의시 지켜야할 것

- Reflexivity : null이 아닌 모든 참조 값 x 에 대해 x.equals(x) 는 true다.
- Symmetry : null이 아닌 모든 참조 값 x, y에 대해 x.equals(y)가 true이면 y.equals(x)도 true다.
- Transitivity : null이 아닌 모든 참조값 x, y, z에 대해 x.equals(y) 가 true고 y.equals(z)가 true면 x.equals(z)도 true다.
- Consistency : null이 아닌 모든 참조 값 x, y에 대해 x.equals(y)를 반복 호출하면 항상 같은 결과가 나온다.
- Not-Null : null이 아닌 모든 참조값 x에 대해 x.equals(null)은 false다.

<br>

### 좋은 equals 재정의

- == 연산자를 사용해 입력이 자기 자신의 참조인지 확인한다.
- instanceof 연산자로 입력이 올바른 타입인지 확인한다.
- 입력을 올바른 타입으로 형변환한다.
- 입력객체와 자기 자신의 대응되는 '핵심' 필드들이 모두 일치하는지 하나씩 검사한다.
  - 필드들의 동치만 검사해도 복잡하지 않게 equals를 구현할 수 있다.

<br>

***귀찮으니까 구글이 만든 AutoValue 프레임워크 쓰자!***

***클래스 애너테이션만 달아주면 된다.***