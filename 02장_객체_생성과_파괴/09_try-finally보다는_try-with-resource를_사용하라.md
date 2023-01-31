## 아이템 9. try-finally보다는 try-with-resource를 사용하라

> 자바에는 닫아야될 친구들이 많습니다.

<br>

### 자원 회수하기

#### 1. try finally와 함께

```java
BufferedReader br = new BufferedReader(new FileReader(path));
try {
  br.readLine();
} finally {
  br.close();
}
```

*JDBC에서 많이들 사용해 보았을 것이다.*

```java
public class Hello {
  public void world() {
    Connection conn = null;
    PreparedStatement pstmt = null;
    ResultSet rs = null; 
    try {
      conn = JDBCUtil.getConnection();
      pstmt = conn.prepareStatement("SELECT ...");
      rs = pstmt.executeQuery();
      while(rs.next()) {
        // ...
      }
    } catch(Exception e) {
      // ...
    } finally {
      JDBCUtil.close(conn, pstmt, rs)
    }
  }
}
```

##### 단점

finally에서도 예외가 발생할 수 있다. 그럼 예외 추적하기가 어려워진다.

<br>

#### 2. try-with-resource와 함께

java 7 부터는 try-with-resource를 사용할 수 있다.

단, AutoCloseable을 구현한 객체만 사용 가능하다!

```java
try (
  Connection conn = DriverManager.getConnection("...");
  Statement stmt = conn.createStatement();
  ResultSet rs = stat.executeQuery("SELECT ...")
) {
  // ...
} catch (Exception e) {
  // ...
} 
```

<br>

Java 9부터는 향상된 try-with-resource를 사용할 수 있다.

```java
Connection conn = DriverManager.getConnection("...");
Statement stmt = conn.createStatement();
ResultSet rs = stat.executeQuery("SELECT ...");

try (conn; stmt; rs) {
  // ...
} catch (Exception e) {
  // ...
} 
```

##### 장점

자원을 쉽고 정확하게 회수할 수 있다.

