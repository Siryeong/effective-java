## 아이템 8. finalizer와 cleaner 사용을 피하라

### finalizer

Java 에서는 가비지 컬렉터의 대상이 될 때 실행되는 메서드를 객체에 정의할 수 있다.

```java
public class Hello {
  @Override
  protected void finalize() throws Throwable {
    // ...
  }  
}
```

java 9부터 deprecated 되었다...

```java
@Deprecated(since="9", forRemoval=true)
protected void finalize() throws Throwable { }
```



### Cleaner

java 9 부터 finalizer의 대안으로 등장한 소멸자이다.

보통 AutoCloseable을 구현해서 사용한다고 한다.

```java
public class Hello implements AutoCloseable {
    private static final Cleaner cleaner = Cleaner.create();

    private static class World implements Runnable {
        @Override
        public void run() {
            // close나 cleaner가 호출합니다.
        }
    }
    
    private final World world;
    private final Cleaner.Cleanable cleanable;

    public Hello() {
        world = new World();
        cleanable = cleaner.register(this, world);
    }

    @Override
    public void close() throws Exception {
        cleanable.clean();;
    }
}
```



### 단점

1. finalizer와 cleaner가 언제 수행 될지 예측할 수 없다. &rarr; 굉장히 불안하다.
2. 심각한 성능 문제를 동반한다. GC효율을 떨어뜨린다.
3. finalizer 공격에 노출될 수 있다.



*finalizer와 cleaner가 생소하여, 충분히 공부 한 후 다시 보도록 하겠습니다.*
