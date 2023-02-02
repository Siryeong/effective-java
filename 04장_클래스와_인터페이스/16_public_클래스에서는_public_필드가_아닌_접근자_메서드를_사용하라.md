## 아이템 16. public 클래스에서는 public 필드가 아닌 접근자 메서드를 사용하라

> getter, setter 써라..

### 퇴보한 클래스

```java
class Point {
  public double x;
  public double y;
}
```

<br>

### getter setter

```java
class Point {
  private double x;
  private double y;
  
  public Point(double x, double y) {
    this.x = x;
    this.y = y;
  }
  
  public double getX() { return x; }
  public double getY() { return y; }
  
  public void setX(double x) { this.x = x; }
  public void setY(double y) { this.y = y; }
}
```

<br>

### 허용되는 경우

- *package-private, private 중첩 클래스라면 데이터 필드를 노출해도 된다.*

불변 필드는 허용 되는가? <br> &rarr; 덜 위험하지만 허용하지 않는다.

***가변필드는 절대 안된다.***