---
layout: post
title: CS Study 08 - Java Backend Interview Quesitons
---

### JVM의 구조와 Java의 실행 방식을 설명해주세요.

`Garbage Collector`, `Execution Engine`, `Class Loader`, `Runtime Data Area`

Execution Engine의 경우 처음에는 interpreter 방식이었지만 JIT 방식으로 바뀌면서 속도가 빨라졌다.
단 변환에 비용이 발생하기 때문에 모든 코드를 변환하지는 않고, interpreter를 사용하다가 일정 기준이 넘어가면 JIT로 변환한다.

GC는 Heap영역에 있는 것들 중 참조되지 않는 데이터를 제거

Runtime Data Area는 memory 영역. application 실행 시 사용되는 data가 여기에 적재된다.
-> `Method Stack`, `Heap Area`, `Stack Area`, `PC Register`, `Native Method Stack`

<br>

### Collection Framework에 대해서 설명해주세요.

객체 및 데이터들을 효율적으로 관리하기 위해 사용하는 라이브러리
시간이 감소하고, 검증되어 있기 때문에 코드의 품질 보장 가능
Generics : 잘못된 타입의 Object를 설정하면 컴파일 타임에 검출 가능하다. instanceof를 쓰지 않아서 코드도 간결하다.
List, Set, Map
Collection에 List, Set 포함

Collection은 Cloneable, Serializable을 상속받지 않는다 : Object를 묶어주기만 함, (추가 이유 1)
Map은 Collection을 상속받지 않는다 : Element Group
HaspMap : Hashing 알고리즘 사용, hashCode()와 equals()를 put()과 get()에 사용
o1.equals(o2) ==> o1.hashCode() = o2.hashCode()
o1.hashCode() = o2.hashCode() =/=> o1.equals(o2)

equals() 오버라이딩 시 hashCode()도 오버라이딩 해야한다.
equals()를 사용하지 않으면 hashCode()도 사용하지 않아야한다.

<br>

### Overriding, Overloading에 대하여 설명해주세요.

Overloading : 확장
메소드의 이름은 같지만 매개변수의 갯수나 타입이 반드시 달라야한다.
접근제어자도 자유롭게 줄 수 있지만 접근제어자만 다르고 매개변수의 갯수와 타입이 같으면 안된다.

Overriding : 상위 클래스의 메소드보다 좁은 범위의 접근 제어자를 사용할 수 없다. 예외는 더 큰 범위로 설정할 수 없다.

@Override Annotation : 없어도 작동되지만 overriding이 잘못된 경우 경고를 띄워 알려주기 때문에 버그 잡기 편하고, 코드 리딩시에도 이점이 있다(overriding된 메소드임을 바로 확인 가능)

<br>

### Annotation이 뭐에요?

코드에 대한 정보를 담고 있는 표시 - 유효성 검사, 메타 데이터
meta-data : data에 대한 설명을 의미하는 data
Meta Annotation : Custom Annotation을 작성할 수 있게 해주는 annotation, `@Retention`(어느 시점까지 annotation이 영향을 미치는가), `@Target`(annotation의 적용대상), `@Documented`(javadoc에 포함), `@Inherited`(상속 가능하도록), `@Repeatable`(연속적으로 annotation을 선언할 수 있도록)
기본 annotation의 종류 : `@Override`(오버라이딩 체크), `@Deprecated`(사용하지 않는 메소드), `@SuppressWarnings`(경고 무시), `@SafeVarargs`(Generic 가변인자 매개변수 경고 무시), `@FunctionalInterface`(함수형 인터페이스 체크)

<br>

### Interface와 Abstract Class의 차이에 대하여 설명해주세요.

둘 다 추상 method를 포함하고, 객체 생성이 불가능
abstract class는 일반 method도 생성할 수 있지만, interface는 추상 method만 가능하다!
Abstract class는 다중 상속 불가능, Interface는 다중 상속 가능

`abstact class` : IS-A
`interface` : HAS-A

- java 8 부터 호환성을 위해 default method에 한정하여 interface 에서도 method의 몸통 부분을 구현할 수 있다.
  - 상위 interface를 구현/상속하는 class/interface가 많으면, 상위 interface에 method 하나를 추가하면 그 interface를 구현/상속한 모든 class/interface가 모두 그 method를 구현해야한다. 이러한 상황을 방지하기 위해 default 키워드로 method를 interface에서도 구현할 수 있도록 하였다.

관련성이 높은 class간 코드를 공유하고 싶은 경우 : abstract class
관련성이 없는 class들이 interface를 구현하는 경우 : interface

<br>

### 접근 제어자의 종류와 이에 대해 설명해주세요.

`private`(같은 class 내에서만) < `(default)`(같은 package 내에서만) < `protected`(자식 class들 까지만) < `public`(모두)

`static abstract` -> 불가능. static 은 몸통이 있어야 한다.
`abstract final` -> 불가능. 상속을 통해 완성해야하는데 상속이 안된다.
`private abstract` -> 불가능. 접근이 안되어 구현이 안된다.

<br>

### 객체지향

객체 : 실생활에서 사용하는 모든 것이 객체이다. 객체 지향 프로그래밍에서의 객체는 이를 추상화시켜 표현한 것. Class는 객체를 만들어내는 틀이고, 이 틀을 사용하며 만들어 낸 것이 instance 이다.

OOP의 특징
`Abstraction`(추상화) : 공통된 특징을 도출하여 틀(class)로 만든다.
`Encapsulation`(캡슐화) : 구현 부분을 외부에 드러내지 않고 숨긴다. 데이터와 기능이 하나로 묶여 객체마다 존재할 수 있다. 외부에서는 객체를 사용할 수 있다.
`Inheritance`(상속성) : 부모 class가 가진 속성을 자식 class가 그대로 사용할 수 있다. 코드의 재사용성의 기반이 된다.
`Polymorphism`(다형성) : 동일한 이름으로 다양한 method를 사용할 수 있다(overloading, overriding).
`Dynaminc Binding`(동적 바인딩) : 바인딩이 실행시간에 결정된다. overriding 된 method가 호출되는 방법이다.

<br>

### SOLID 원칙

`SPR(Single Responsibility Principle)` : 단일 책임 원칙

- 하나의 역할만을 가져야한다. 많은 역할을 가진 class는 자손 class로 분리해야한다.

`OCP(Open Closed Principle)` : 개방 폐쇄 원칙

- 확장에 대해서는 개방되어 있어야 하고, 변경에 대해서는 폐쇄되어 있어야 한다.

`LSP(Liskov Substitution Principle)` : 리스코프 치환 원칙

- sub-type은 base-type으로 교체할 수 있어야 한다. 부모 class/interface 형 참조변수로 자손 class instance를 참조할 수 있어야한다.

`ISP(Interface Segregation Principle)` : 인터페이스 분리 원칙

- client가 자신이 이용하지 않는 method에 의존하면 안된다. 사용하지 않는 method가 있다면 부모 interface에서 그 method는 다른 interface로 분리해야한다.

`DIP(Dependency Inversion Principle)` : 의존 역전 원칙

- 고차원 모듈은 저차원 모듈에 의존하면 안된다. 추상화 된 것은 구체적인 것에 의존하면 안되고, 구체적인 것이 추상화 된 것에 의존해야한다. 구체 클래스/하위 클래스는 변경이 별로 없을 가능성이 추상 클래스/상위 클래스/interface에 의존해야한다.
