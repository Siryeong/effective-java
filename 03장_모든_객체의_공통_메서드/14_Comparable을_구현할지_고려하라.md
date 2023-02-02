## Comparable을 구현할지 고려하라

### compareTo

- Comparable의 유일한 메서드
- Obejcts에는 없다.
- equals의 상위호환
- 순서를 비교할 수 있다.
- 제네릭하다.

순서를 가지는 클래스라면 comparable을 구현하자!

### 일반규약

> equals와 비슷하다.

:exclamation: sgn &rarr; signum function (0, 1, -1만 반환한다)

- comparable을 구현한 클래스는 모든 x, y에 대해 *sgn(x.compareTo(y)) == -sgn(y.compareTo(x))이어야 한다.*
- comparable을 구현한 클래스는 transitivity를 보장해야 한다. <br>&rarr; *x.compareTo(y) > 0 && y.compareTo(z) > 0이면 x.compareTo(z) > 0 이다.*
- comparable을 구현한 클래스는 모든 z에 대해 *x.compareTo(y) == 0이면 sgn(x.compareTo(z)) == sgn(y.compareTo(z))이다.*
- 권고사항, *(x.compareTo(y) == 0) == x.equals(y)이어야 한다.* (권고이지만 반드시 지킬것!)