## 아이템 24. 멤버 클래스는 되도록 static으로 만들어라

### nested class

클래스 안에 있는 클래스 (마트료시카)

네가지 정도로 분류할 수 있다.

- static member class
- non static member class
- anonymous class
- local class

#### static member class

- static member class 는 보통 도우미 클래스로 활용된다. <br> &rarr; `Calculator.Operation.PLUS` 처럼 내부 연사나 타입을 정의 한다던지

#### non-static member class

- non static member class 는 보통 adapter를 정의할 때 활용된다. <br> &rarr; 어댑터 패턴 참고 (usb convertor를 생각해봅시다.)
- non static neseted class 는 바깥쪽 인스턴스와 암묵적으로 연결된다(숨은참조).  따라서 밖에 있는 데이터를 가져가 뭔가 할 수 있음.
- ***멤버 클래스에서 바깥 인스턴스에 접근할 일이 없다면 무조건 static으로 만들자*** <br> &rarr; 숨은 참조로 인해 메모리공간, 생성시간이 추가로 필요.

#### private static

- entry class를 만들때 사용한다.

#### anonymous class

- 이름없는 클래스
- 람다식 만들때 쓴다.
- static factory method구현할때도 쓸 수 있다.

#### local class

- local variable처럼 사용하기 위한 클래스

