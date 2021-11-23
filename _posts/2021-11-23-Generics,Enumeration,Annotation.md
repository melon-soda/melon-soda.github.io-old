---
layout: post
title: Generics, Enumeration, Annotation
---

Generics : 다양한 type의 객체를 다루는 method / Collection class에 Compile-time type check를 해주는 기능
객체의 type을 compile시에 체크하기 때문에 type 안정성을 높이고 형변환의 번거로움이 줄어든다.

Class에 선언하는 방법

class 옆에 \<T\>를 붙이고 Object를 T로 변경

```java
/* 기존 class */
class Box {
	Object item;

	void setItem(Object item) {
		this.item = item;
	}

	Object getItem() {
		return item;
	}
}

/* generic class */
class Box<T> {
	T item;

	void setItem(T item) {
		this.item = item;
	}

	T getItem() {
		return item;
	}
}
```

T : Type
E : Element
K : Key
V : Value

generic class여도 이전의 방식대로 object를 선언하는 것이 가능하지만 type을 지정하지 않아 안전하지 않다는 경고가 발생한다.

Box\<T\> : generic class
T : 타입 변수 / 타입 매개변수(T : 타입 문자)
Box : 원시 타입(raw type)

generic class의 제한 사항

static 멤버에는 타입 변수 T를 사용할 수 없다(static T item)
generic type의 배열을 생성할 수 없다(new T[10])

generic class의 객체 생성

참조변수와 생성자의 매개변수화 된 타입(T)가 일치해야한다. 상속관계도 불가능
두 generic class가 상속 관계에 있고 매개변수화 된 타입(T)가 동일한경우는 가능하다.
JDK 1.7부터 타입(T)가 같을 경우 생략할 수 있다.
생성된 Box\<T\> 객체에 void add(T item)으로 객체를 추가할 때 매개변수화 된 타입과 다른 객체는 담을 수 없다. 단, T의 자손은 담을 수 있다.

```java
import java.util.ArrayList;

class Fruit {
	public String toString() {
		return "Fruit";
	}
}

class Apple extends Fruit {
	public String toString() {
		return "Apple";
	}
}

class Grape extends Fruit {
	public String toString() {
		return "Grape";
	}
}

class Toy {
	public String toString() {
		return "Toy";
	}
}

class FruitBoxEx1 {
	public static void main(String[] args) {
		Box<Fruit> fruitBox = new Box<Fruit>();
		// Box<Fruit> fruitBox = new Box<>();
		Box<Apple> appleBox = new Box<Apple>();
		Box<Toy> toyBox = new Box<Toy>();
		// Box<Grape> grapeBox = new Box<Apple>;	// Type 불일치

		fruitBox.add(new Fruit());
		fruitBox.add(new Apple());		// void add(Fruit item)

		appleBox.add(new Apple());
		// appleBox.add(new Toy());		// Box<Apple>에는 Apple만 담을 수 있음

		toyBox.add(new Toy());
		// toyBox.add(new Apple());		// Box<Toy>에는 Toy만 담을 수 있음

		System.out.println(fruitBox);
		System.out.println(appleBox);
		System.out.println(toyBox);
	}
}

class Box<T> {
	ArrayList<T> list = new ArrayList<T>();
	
	void add(T item) {
		list.add(item);
	}
	
	T get(int i) {
		return list.get(i);
	}

	int size() {
		return list.size();
	}

	public String toString() {
		return list.toString();
	}
}
```

제한된 generic class

type에 extends를 사용하면 특정 타입의 자손들만 대입할 수 있도록 제한할 수 있다.
interface를 구현하는 경우에도 implements가 아닌 extends를 사용한다.
2개 이상의 interface를 구현하는 경우 & 로 연결하여 사용한다.

```java
import java.util.ArrayList;

class Fruit implements Eatable {
	public String toString() {
		return "Fruit";
	}
}

class Apple extends Fruit {
	public String toString() {
		return "Apple";
	}
}

class Grape extends Fruit {
	public String toString() {
		return "Grape";
	}
}

class Toy {
	public String toString() {
		return "Toy";
	}
}

interface Eatable {

}

class FruitBoxEx2 {
	public static void main(String[] args) {
		FruitBox<Fruit> fruitBox = new FruitBox<Fruit>();
		FruitBox<Apple> appleBox = new FruitBox<Apple>();
		FruitBox<Grape> grapeBox = new FruitBox<Grape>();
		// FruitBox<Toy> toyBox = new FruitBox<Toy>();	// Toy는 Fruit의 자손이 아니므로 담을 수 없음

		fruitBox.add(new Fruit());
		fruitBox.add(new Apple());
		fruitBox.add(new Grape());
		appleBox.add(new Apple());
		// appleBox.add(new Grape());					// Grape는 Apple의 자손이 아니므로 담을 수 없음
		grapeBox.add(new Grape());

		System.out.println(fruitBox);
		System.out.println(appleBox);
		System.out.println(grapeBox);
	}
}

class FruitBox<T extends Fruit & Eatable> extends Box<T> {

}

class Box<T> {
	ArrayList<T> list = new ArrayList<T>();
	
	void add(T item) {
		list.add(item);
	}

	T get(int i) {
		return list.get(i);
	}

	int size() {
		return list.size();
	}

	public String toString() {
		return list.toString();
	}
}
```

wild card

generic type만 다른 것만으로는 overloading이 성립하지 않아 method 중복 정의로 취급된다.
따라서 어떠한 type도 가능한 wild card ? 를 사용한다.

\<? extends T\> : 상한 제한. T와 자손들만 가능
\<? super T\> : 하한 제한. T와 조상들만 가능
\<?\> : 제한 X, \<? extends Object\>와 동일

> \<? extends T & E\>와 같이 wild card에는 & 를 사용할 수 없다.

```java
static Juice makeJuice(FruitBox<? extends Object> box) {
	String tmp = "";

	for(Fruit f : box.getList())	// box의 요소가 Fruit의 자손이라는 보장이 없으므로 에러 발생
		tmp += f + " ";

	return new Juice(tmp);
}
```

```java
/* 이 문장이 있을 경우 위의 코드에서 에러 발생하지 않음 */
/* 컴파일러가 이미 FruitBox의 요소들이 Fruit의 자손이라는 것을 알고있다. */
class FruitBox<T extends Fruit> extends Box<T> {

}
```

```java
import java.util.ArrayList;

class Fruit {
	public String toString() {
		return "Fruit";
	}
}

class Apple extends Fruit {
	public String toString() {
		return "Fruit";
	}
}

class Grape extends Fruit {
	public String toString() {
		return "Grape";
	}
}

class Juice {
	String name;

	Juice(String name) {
		this.name = name + "Juice";
	}

	public String toString() {
		return name;
	}
}

class Juicer {
	static Juice makeJuice(FruitBox<? extends Fruit> box) {
		String tmp = "";

		for(Fruit f : box.getList())
			tmp += f + " ";

		return new Juice(tmp);
	}
}

class FruitBoxEx3 {
	public static void main(String[] args) {
		FruitBox<Fruit> fruitBox = new FruitBox<Fruit>();
		FruitBox<Apple> appleBox = new FruitBox<Apple>();

		fruitBox.add(new Apple());
		fruitBox.add(new Grape());
		appleBox.add(new Apple());
		appleBox.add(new Apple());

		System.out.println(Juicer.makeJuice(fruitBox));
		System.out.println(Juicer.makeJuice(appleBox));
	}
}

class FruitBox<T extends Fruit> extends Box<T> {

}

class Box<T> {
	ArrayList<T> list = new ArrayList<T>();

	void add(T item) {
		list.add(item);
	}

	T get(int i) {
		return list.get(i);
	}

	ArrayList<T> getList() {
		return list;
	}
	
	int size() {
		return list.size();
	}

	public String toString() {
		return list.toString();
	}
}
```

```java
import java.util.*;

class Fruit {
	String name;
	int weight;

	Fruit(String name, int weight) {
		this.name = name;
		this.weight = weight;
	}

	public String toString() {
		return name + "(" + weight + ")";
	}
}

class Apple extends Fruit {
	Apple(String name, int weight) {
		super(name, weight);
	}
}

class Grape extends Fruit {
	Grape(String name, int weight) {
		super(name, weight);
	}
}

class AppleComp implements Comparator<Apple> {
	public int compare(Apple t1, Apple t2) {
		return t2.weight - t1.weight;
	}
}

class GrapeComp implements Comparator<Grape> {
	public int compare(Grape t1, Grape t2) {
		return t2.weight - t1.weight;
	}
}

class FruitComp implements Comparator<Fruit> {
	public int compare(Fruit t1, Fruit t2) {
		return t1.weight - t2.weight;
	}
}

class FruitBoxEx4 {
	public static void main(String[] args) {
		FruitBox<Apple> appleBox = new FruitBox<Apple>();
		FruitBox<Grape> grapeBox = new FruitBox<Grape>();

		appleBox.add(new Apple("GreenApple", 300));
		appleBox.add(new Apple("GreenApple", 100));
		appleBox.add(new Apple("GreenApple", 200));

		grapeBox.add(new Grape("GreenGrape", 400));
		grapeBox.add(new Grape("GreenGrape", 300));
		grapeBox.add(new Grape("GreenGrape", 200));

		Collections.sort(appleBox.getList(), new AppleComp());
		Collections.sort(grapeBox.getList(), new GrapeComp());

		System.out.println(appleBox);	// 300, 200, 100
		System.out.println(grapeBox);	// 400, 300, 200
		System.out.println();

		Collections.sort(appleBox.getList(), new FruitComp());
		Collections.sort(grapeBox.getList(), new FruitComp());

		System.out.println(appleBox);	// 100, 200, 300
		System.out.println(grapeBox);	// 200, 300, 400
	}
}

class FruitBox<T extends Fruit> extends Box<T> {

}

class Box<T> {
	ArrayList<T> list = new ArrayList<T>();

	void add(T item) {
		list.add(item);
	}

	T get(int i) {
		return list.get(i);
	}

	ArrayList<T> getList() {
		return list;
	}

	int size() {
		return list.size();
	}

	public String toString() {
		return list.toString();
	}
```

generic method

method의 선언부에 generic type이 선언된 method
반환 타입 앞에 generic type을 선언한다.

```java
static <T> void sort(List<T> list, Comparator<? super T> c)
```

generic class에 정의된 타입 매개변수 T와 generic method에 정의된 타입 매개변수 T는 별개이다.

static 멤버에는 타입 매개변수를 사용할 수 없으나 method에 generic type을 선언하고 사용하는 것은 가능하다.

```java
static Juice makeJuice(FruitBox<? extends Fruit> box) {
	String tmp = "";
	for(Fruitf : box.getList())
		tmp += f + " ";

	return new Juice;
}
```

```java
static <T extends Fruit> Juice makeJuice(FruitBox<T> box) {
	for(Fruitf : box.getList())
		tmp += f + " ";

	return new Juice;
}
```

method 호출 시 type	변수에 type을 대입해야한다.

```java
FruitBox<Fruit> fruitBox = new FruitBox<Fruit>();
FruitBox<Apple> appleBox = new FruitBox<Apple>();

System.out.println(Juicer.<Fruit>makeJuice(fruitBox));
System.out.println(Juicer.<Apple>makeJuice(appleBox));
```

대부분의 경우 compiler가 type을 추정할 수 있기 때문에 생략 가능하다.

```java
System.out.println(Juicer.makeJuice(fruitBox));
System.out.println(Juicer.makeJuice(appleBox));
```

type 매개변수를 생략할 수 없는 경우에는 참조변수나 class 이름을 생략할 수 없다.

```java
// System.out.println(<Fruit>makeJuice(fruitBox));	// 생략 불가
System.out.println(this.<Fruit>makeJuice(fruitBox));
System.out.println(Juicer.<Fruit>makeJuice(fruitBox));
```

주로 매개변수의 type이 복잡할 경우 generic method를 사용하면 보다 간결하게 줄일 수 있다.

```java
public static void printAll(ArrayList<? extends Product> list, ArrayList<? extends Product> list2) {
	for(Unit u : list) {
		System.out.println(u);
	}
}
```

```java
public static <T extends Product> void printAll(ArrayList<T> list, ArrayList<T> list2) {
	for(Unit i : list) {
		System.out.println(u);
	}
}
```

generic type의 형변환

raw type \<-\> generic type : 가능, 경고 발생
generic type\<A\> \<-\> generic type\<B\> : 불가능

```java
Box box = null;
Box<Object> objBox = null;

box = (Box)objBox;			// 가능. generic type -> raw type. 경고 발생
objBox = (Box<Object>)box;	// 가능. raw type -> generic type. 경고 발생
```

```java
Box<Object> objBox = null;
Box<String> strBox = null;

objBox = (Box<Object>)strBox;	// 불가능
strBox = (Box<String>)objBox;	// 불가능
```

```java
Box<? extends Object> wBox = new Box<String>();		// 가능. 다형성 적용 가능

Box<? extends Object> wBox2 = null;
Box<String> strBox = (Box<String>)wBox2;// 가능. 경고 발생 : 확인되지 않은 형변환
```

```java
public final class Optional<T> {
	private static final Optional<?> EMPTY = new Optional<>();		//(1)
	private final T value;

	public static<T> Optional<T> empty() {
		Optional<T> t = (Optional<T>)EMPTY;							//(2)
		return t;
	}
}
```

\(1\) : Optional<? extends Object> EMPTY = new Optional\<Object\> 와 동일
\(2\) : Optional\<Object\>가 아닌 Optional\<?\>로 했기때문에 Optional\<T\>로 형변환 가능
Optional\<Object\> -\> Optional\<T\>						: 불가능
Optional\<Object\> -\> Optional\<?\> -\> Optional\<T\>		: 가능, 경고 발생

wild card가 사용된 generic type 끼리도 형변환이 가능하나 확정된 type이 아니므로 경고가 발생한다.

```java
FruitBox<? extends Object> objBox = null;
FruitBox<? extends String> strBox = null;

strBox = (FruitBox<? extends String>)objBox;		// 가능, 미확정 type으로 형변환 경고
objBox = (FruitBox<? extends Object>)strBox;		// 가능, 미확정 type으로 형변환 경고
```

generic type의 제거

compile된 class 파일에는 generic type에 대한 정보가 없다.
가능하면 raw type을 사용하는 것을 지양하는것이 좋다.

1. generic type의 bound 제거

\<T extends Fruit\> -\> Fruit
\<T\> -\> Object

```java
class Box<T extends Fruit> {
	void add(T t) {

	}
}
```

```java
class Box {
	void add(Fruit t) {

	}
}
```

2. type이 일치하지 않으면 형변환 추가

```java
T get(int i) {
	return list.get(i);
}
```

```java
Fruit get(int i) {
	return (Fruit)list.get(i);
}
```

enums(열거형)

서로 관련된 상수를 편리하게 선언하기 위한 것
JDK 1.5부터 추가되었다.

enum enumName {const1, const2, ... }

상수 간의 비교에는 ==를 사용할 수 있다.
\<, \>는 사용할 수 없으니 compareTo()를 사용 가능하다.

switch문의 case에도 사용 가능하나, 상수의 이름만 적어야한다.

```java
switch(dir) {
	case EAST :
		x++;
		break;
/*
    case Direction.EAST :		// 불가능
		x++;
		break;
*/
}
```

java.lang.Enum : 모든 열거형의 조상

Enum에 정의되어 있는 method들

Class\<E\> getDeclaringClass() : 열거형의 Class 객체 반환
String name() : 열거형 상수의 이름을 문자열로 반환
int ordinal() : 열거형 상수가 정의된 순서 반환
T valueOf(Class\<T\> enumType, String name) : enumType에서 name과 일치하는 열거형 상수 반환

static E values() : 열거형의 모든 상수를 배열에 담아 반환
static E valueOf() : 열거형 상수의 이름으로 문자열 상수에 대한 참조 반환

```java
enum Direction { EAST, SOUTH, WEST, NORTH }

class EnumEx1 {
	public static void main(String[] args) {
		Direction d1 = Direction.EAST;
		Direction d2 = Direction.valueOf("WEST");
		Direction d3 = Enum.valueOf(Direction.class, "EAST");

		System.out.println("d1 = " + d1);
		System.out.println("d2 = " + d2);
		System.out.println("d3 = " + d3);

		System.out.println("d1 == d2 ? " + (d1 == d2));
		System.out.println("d1 == d3 ? " + (d1 == d3));
		System.out.println("d1.equals(d3) ? " + d1.equals(d3));
		// System.out.println("d2 > d3 ? " + (d2 > d3));	// <, >로 비교 불가
		System.out.println("d1.compareTo(d2) ? " + (d1.compareTo(d2)));
		System.out.println("d1.compareTo(d3) ? " + (d1.compareTo(d3)));

		switch(d1) {
			case EAST :
				System.out.println("The direction is EAST.");
				break;
			case WEST :
				System.out.println("The direction is WEST.");
				break;
			case SOUTH :
				System.out.println("The direction is SOUTH.");
				break;
			case NORTH :
				System.out.println("The direction is NORTH.");
				break;
			deafult : 
				System.out.println("Invalid direction.");
				break;
		}

		Direction[] dArr = Direction.values();

		for(Direction d : dArr)
			System.out.printf("%s = %d\\n", d.name(), d.ordinal());
	}
}
```

ordinal()은 열거형 상수가 정의된 순서를 반환하나 내부적인 용도로 사용되기 때문에 사용하지 않는 것이 좋다.
불연속적인 값을 가지는 경우는 상수 이름 옆에 ()와 원하는 값을 적고, 인스턴스 변수롸 생성자를 추가해야한다.

```java
enum Direction {
	EAST(1), WEST(-1), SOUTH(2), NORTH(-2);

	private final int value;

	Direction(int value) {
		this.value = value;
	}

	public int getValue() {
		return value;
	}
}
```

생성자를 추가하여도 enum의 생성자는 private이기 때문에 외부에서 enum의 객체를 생성할 수 없다.

하나의 열거형 상수에 여러 값을 지정할 수도 있으나 각각에 맞는 instance 변수와 생성자 등을 추가해야한다.

```java
enum Direction {
	EAST(1, ">"), SOUTH(2, "V"), WEST(3, "<"), NORTH(4, "^");

	private static final Direction[] DIR_ARR = Direction.values();
	private final int value;
	private final String symbol;

	Direction(int value, String symbol) {
		this.value = value;
		this.symbol = symbol;
	}

	public int getValue() {
		return value;
	}

	public String getSymbol() {
		return symbol;
	}

	public static Direction of(int dir) {
		if(dir < 1 || dir > 4) {
			throw new IllegalArgumentException("Invalid Value : " + dir);
		}

		return DIR_ARR[dir - 1];
	}

	public Direction rotate(int num) {
		num = num % 4;

		if(num < 0)
			num += 4;

		return DIR_ARR[(value - 1 + num) % 4];
	}

	public String toString() {
		return name() + getSymbol();
	}
}

class EnumEx2 {
	public static void main(String[] args) {
		for(Direction d : Direction.values())
			System.out.printf("%s = %d\\n", d.name(), d.getValue());

		Direction d1 = Direction.EAST;
		Direction d2 = Direction.of(1);

		System.out.printf("%d1 = %s, %d\\n", d1.name(), d1.getValue());
		System.out.printf("%d2 = %s, %d\\n", d2.name(), d2.getValue());
		System.out.println(Direction.EAST.rotate(1));
		System.out.println(Direction.EAST.rotate(2));
		System.out.println(Direction.EAST.rotate(-1));
		System.out.println(Direction.EAST.rotate(-2));
	}
}
```

열거형에 추상메소드를 선언하면 각 상수가 이 추상메소드를 각각 구현할 수 있도록 할 수 있다.

```java
enum Transportation {
	BUS(100) {
		int fare(int distance) {
			return distance * BAISC_FARE;
		}
	},
	TRAIN(150) {
		int fare(int distance) {
			return distance * BASIC_FARE;
		}
	},
	SHIP(100) {
		int fare(int distance) {
			return distance * BASIC_FARE;
		}
	},
	AIRPLANE(300) {
		int fare(int distance) {
			return distance * BASIC_FARE;
		}
	};

	protected final int BASIC_FARE;

	Transportation(int basicFare) {
		BASIC_FARE = basicFare;
	}

	public int getBasicFare() {
		return BASIC_FARE;
	}

	abstract int fare(int distance);
}

class EnumEx3 {
	public static void main(String[] args) {
		System.out.println("bus fare = " + Transportation.BUS.fare(100));
		System.out.println("train fare = " + Transportation.TRAIN.fare(100));
		System.out.println("ship fare = " + Transportation.SHIP.fare(100));
		System.out.println("airplane fare = " + Transportation.AIRPLANE.fare(100));
	}
}
```

```java
abstract class MyEnum<T extends MyEnum<T>> implements Comparable<T> {
	static int id = 0;
	int ordinal;
	String name = "";

	public int ordinal() {
		return ordinal;
	}

	MyEnum(String name) {
		this.name = name;
		ordinal = id++;
	}

	public int compareTo(T t) {
		return ordinal - t.ordinal();
	}
}

abstract class MyTransportation extends MyEnum {
	static final MyTransportation BUS = new MyTransportation("BUS", 100) {
		int fare(int distance) {
			return distance * BASIC_FARE;
		}
	};

	static final MyTransportation TRAIN = new MyTransportation("TRAIN", 100) {
		int fare(int distance) {
			return distance * BASIC_FARE;
		}
	};

	static final MyTransportation SHIP = new MyTransportation("SHIP", 100) {
		int fare(int distance) {
			return distance * BASIC_FARE;
		}
	};

	static final MyTransportation AIRPLANE = new MyTransportation("AIRPLANE", 300) {
		int fare(int distance) {
			return distance * BASIC_FARE;
		}
	};

	abstract int fare(int distance);

	protected final int BASIC_FARE;

	private MyTransportation(String name, int basicFare) {
		super(name);
		BASIC_FARE = basicFare;
	}

	public String name() {
		return name;
	}

	public String toString() {
		return name;
	}
}

class EnumEx4 {
	public static void main(String[] args) {
		MyTransportation t1 = MyTransportation.BUS;
		MyTransportation t2 = MyTransportation.BUS;
		MyTransportation t3 = MyTransportation.TRAIN;
		MyTransportation t4 = MyTransportation.SHIP;
		MyTransportation t5 = MyTransportation.AIRPLANE;

		System.out.printf("t1 = %s, %d\\n", t1.name(), t1.ordinal());
		System.out.printf("t2 = %s, %d\\n", t2.name(), t2.ordinal());
		System.out.printf("t3 = %s, %d\\n", t3.name(), t3.ordinal());
		System.out.printf("t4 = %s, %d\\n", t4.name(), t4.ordinal());
		System.out.printf("t5 = %s, %d\\n", t5.name(), t5.oridnal());
		System.out.println("t1 == t2 ? " + (t1 == t2));
		System.out.println("t1.compareTo(t3) = " + t1.compareTo(t3));
	}
}
```
