---
layout: post
title: Collections Framework
---

List, Set, Map의 3가지 Interface를 기본으로 하며, List와 Set은 공통 조상인 Collection Interface를 추가로 정의하였다.

List : 순서가 있는 데이터의 집합. 중복 허용 O
Set : 순서가 없는 데이터의 집합. 중복 허용 X
Map : key-value pair로 이루어진 데이터의 집합. 순서가 없다. key는 중복 허용 X, value는 중복 허용 O

Vector, Stack, Hashtable, Properties등을 제외하면 각 class의 이름에 붙는 접미사로 어떤 Interface를 구현한 것인지 쉽게 알 수 있다. 해당 class들은 Collection Framework가 만들어지기 전부터 존재하여 명명법을 따르지 않는다.

Collection Interface에 정의되어있는 method

boolean add(Object o) : 지정된 Object의 객체들을 Collection에 추가
boolean addAll(Collection c) : 지정된 Collection의 객체들을 Collection에 추가
void clear() : Collection의 모든 객체 삭제
boolean contains(Object o) : 지정된 Object가 Collection에 포함되어있는지 확인
boolean containsAll(Collection c) : 지정된 Collection의 객체들이 Collection에 포함되어있는지 확인
boolean equals(Object o) : 동일한 Collection인지 비교
int hashCode() : hash code 반환
boolean isEmpty() : 빈 Collection인지 확인
Iterator iterator() : Iterator를 반환
boolean remove(Object o) : 지정된 Object를 삭제
boolean removeAll(Collection c) : 지정된 Collection에 포함된 모든 객체 삭제
boolean retainAll(Collection c) : 지정된 Collection에 포함된 객체만을 남기고 나머지 모든 객체 삭제. Collection에 변화가 있으면 true, 변화가 없으면 false
int size() : Collection에 저장된 객체의 갯수 반환
Object[] toArray() : Collection에 저장된 Object들을 Object[] 배열로 반환
Object[] toArray(Object[] a) : 지정된 배열 a에 Collection의 객체를 저장해서 반환

List : 중복을 허용하면서 저장 순서가 유지되어야 하는 경우

List - Vector - Stack
	|- ArrayList
	\- LinkedList

List Interface에 정의되어있는 method

void add(int index, Object element) : 지정된 index에 element 추가
boolean addAll(int index, Collection c) : 지정된 index에 Collection에 포함된 객체 모두 추가
Object get(int index) : 지정된 index에 있는 객체 반환
int indexOf(Object o) : 지정된 Object의 위치 반환(순방향)
int lastIndexOf(Object o) : 지정된 Object의 위치 반환(역방향)
ListIterator listIterator() : List의 Object에 접근 가능한 ListIterator 반환
ListIterator listIterator(int index) : index에서 시작하는 ListIterator 반환
Object remove(int index) : 지정된 index에 있는 Object를 삭제하고 삭제한 Object를 반환
Object set(int index, Object element) : 지정된 index에 element 저장
void sort(Comparator c) : 지정된 Comparator로 List 정렬
List subList(int fromIndex, int toIndex) : fromIndex부터 toIndex까지의 객체를 List로 반환

Set : 중복을 허용하지 않고 저장순서가 유지될 필요가 없을 때

Set - SortedSet - TreeSet
   \- HashSet

Map : key와 value를 하나의 쌍으로 묶어서 저장하는 경우

Map - Hashtable
   |- HashMap - LinkedHashMap
   \- SortedMap - TreeMap

Map Interface에 정의되어있는 method

void clear() : Map의 모든 object 삭제
boolean containsKey(Object key) : 지정된 key와 일치하는 key 객체가 있는지 확인
boolean containsValue(Object value) : 지정된 value와 일치하는 value 객체가 있는지 확인
Set entrySet() : key-value쌍을 Map.Entry 타입의 객체로 저장한 Set으로 반환
boolean equals(Object o) : 동일한 Map인지 비교
Object get(Object key) : 지정된 key에 대응되는 value값 반환
int hashCode() : hashCode 반환
boolean isEmpty() : Map이 비어있는지 확인
Set keySet() : Map에 저장된 모든 key 반환
Object put(Object key, Object value) : key 객체에 value 객체를 mapping하여 저장
void putAll(Map t) : 지정된 Map의 모든 key-value pair 저장
Object remove(Object key) : 지정된 key와 일치하는 key-value pair를 찾아 삭제하고 반환
int size() : 저장된 key-value pair의 갯수 반환
Collection values() : 모든 value 객체 반환

keySet()의 경우 key는 중복을 허용하지 않기 때문에 Set 으로 반환되지만, values()의 경우 value는 중복될 수 있기 때문에 Collection 으로 반환된다.

Map.Entry Interface

Map의 내부 Interface이므로 Map을 구현하는 class에서는 Map.Entry도 함께 구현해야한다.

Map.Entry Interface에 정의되어있는 method

boolean equals(Object o) : 동일한 Entry인지 비교
Object getKey() : Entry의 key 객체 반환
Object getValue() : Entry의 value 객체 반환
int hashCode() : Entry의 hashCode 반환
Object setValue(Object value) : Entry의 value 객체를 주어진 value 객체로 바꿈

ArrayList

List Interface를 구현하기 때문에 데이터의 저장 순서를 유지하고 중복을 허용한다.
Vector를 개선하였기에 기능적으로는 동일하다.

ArrayList에 정의되어있는 method

ArrayList() : 크기가 10인 ArrayList 생성
ArrayList(Collection c) : 주어진 Collection이 저장된 ArrayList 생성
ArrayList(int initialCapacity) : 초기용량을 initialCapacity로 갖는 ArrayList 생성
boolean add(Object o) : ArrayList의 마지막에 Object 추가, 성공시 true
void add(int index, Object element) : 지정된 index에 element를 저장
boolean addAll(Collection c) : Collection의 모든 객체를 ArrayList에 저장
boolean addAll(int index, Collection c) : index부터 Collection의 모든 객체 저장
void clear() : ArrayList를 비움
Object clone() : ArrayList 복제
boolean contains(Object o) : Object o 가 ArrayList에 포함되어 있는지 확인
void ensureCapacity(int minCapacity) : ArrayList의 용량이 최소 minCapacity가 되도록 한다.
Object get(int index) : index에 저장된 Object 반환
int indexOf(Object o) : Object가 저장된 index 반환
boolean isEmpty() : ArrayList가 비어있는지 확인
Iterator iterator() : ArrayList의 Iterator 반환
int lastIndexOf(Object o) : Object o가 저장된 index를 역방향으로 검색하여 반환
ListIterator listIterator() : ArrayList의 ListIterator 반환
ListIterator listIterator(int index) : index부터 시작하는 ListIterator 반환
Object remove(index) : index에 있는 Object를 제거하고 반환
boolean remove(Object o) : Object o를 제거,	성공시 true
boolean removeAll(Collection c) : Collection c에 저장된 것과 동일한 객체들을 ArrayList에서 제거
boolean retainAll(Collection c) : Collection c에 저장된 것과 동일한 객체들만 남기고 나머지는 ArrayList에서 제거
Object set(int index, Object element) : index의 Object를 element로 바꿈
int size() : ArrayList에 저장된 객체의 갯수 반환
void sort(Comparator c) : Comparator c를 기준으로 ArrayList를 정렬
List subList(int fromIndex, int toIndex) : fromIndex부터 toIndex까지의 객체를 List로 반환
Object[] toArray() : ArrayList를 Object[]로 반환
Object[] toArray(Object[] a) : ArrayList를 Object[] a로 반환
void trimToSize() : 빈 공간을 잘라내어 크기에 맞게 용량을 줄임

```java
import java.util.*;

class ArrayListEx1 {
	public Static void main(String[] args) {
		ArrayList list1 = new ArrayList(10);

		list1.add(new Integer(5));
		list1.add(new Integer(4));
		list1.add(new Integer(2));
		list1.add(new Integer(0));
		list1.add(new Integer(1));
		list1.add(new Integer(3));

		ArrayList list2 = new ArrayList(list1.subList(1, 4));

		print(list1, list2);		// list1 : [5, 4, 2, 0, 1, 3]	list2 : [4, 2, 0]

		Collections.sort(list1);
		Collections.sort(list2);

		print(list1, list2);		// list1 : [0, 1, 2, 3, 4, 5]	list2 : [0, 2, 4]

		System.out.println("list1.containsAll(list2) : " + list1.containsAll(list2)); //true

		list2.add("B");
		list2.add("C");
		list2.add(3, "A");

		print(list1, list2);		// list2 : [0, 2, 4, A, B, C]

		list2.set(3, "AA");

		print(list1, list2);		// list2 : [0, 2, 4, AA, B, C]

		System.out.println("list1.retainAll(list2) : " + list1.retainAll(list2));	// true

		print(list1, list2);		// list1 : [0, 2, 4]

		for(int i = list2.size() - 1; i >= 0; i--) {
			if(list1.contains(list2.get(i)))
				list2.remove(i);
		}

		print(list1, list2);		// list2 : [AA, B, C]
	}

	static void print(ArrayList list1, Arraylist list2) {
		System.out.println("list1 : " + list1);
		System.out.println("list2 : " + list2);
		System.out.println();
	}
}
```

```java
import java.util.*;

class ArrayListEx2 {
	public static void main(String[] args) {
		final int LIMIT = 10;
		String source = "0123456789abcdefghijABCDEFGHIJ!@#$%^&*()ZZZ";
		int length = source.length();

		List list = new ArrayList(length / LIMIT + 10);

		for(int i = 0; i < length; i += LIMIT) {
			if(i + LIMIT < length)
				list.add(source.substring(i, i + LIMIT));
			else
				list.add(source.substring(i));
		}

		for(int i = 0; i < list.size(); i++) {
			System.out.println(list.get(i));
		}
	}
}
```

```java
import java.util.*;

class VectorEx1 {
	public static void main(String[] args) {
		Vector v = new Vector(5);

		v.add("1");
		v.add("2");
		v.add("3");

		print(v);

		v.trimToSize();
		System.out.println("=== After timeToSize() ===");
		print(v);

		v.ensureCapacity(6);
		System.out.println("=== After ensureCapacity(6) ===");
		print(v);

		v.setSize(7);
		System.out.println("=== After setSize(7) ===");
		print(v);

		v.clear();
		System.out.println("=== After clear() ===");
		print(v);
	}

	public static void print(Vector v) {
		System.out.println(v);
		System.out.println("size : " + v.size());
		System.out.println("capacity : " + v.capacity());
		System.out.println();
	}
}
```

Vector의 경우 data를 읽고 저장하는 효율은 좋으나 capacity를 확장하는 경우 배열을 통째로 복사해야하므로 비효율적이다. 이를 방지하기 위해서는 처음부터 충분한 용량의 instance를 생성해야한다.

```java
import java.util.*;

class MyVector implements List {
	Object[] data = null;
	int capacity = 0;
	int size = 0;

	pubilc MyVector(int capacity) {
		if(capacity < 0)
			throw new IllegalArgumentException("유효하지 않은 값입니다. : " + capacity);

		this.capacity = capacity;
		data = new Object[capacity];
	}

	public MyVector() {
		this(10);
	}

	public void ensureCapacity(int minCapacity) {
		if(minCapacity - data.length > 0)
			setCapacity(minCapacity);
	}

	public boolean add(Object obj) {
		ensureCapacity(size + 1);
		data[size++] = obj;

		return true;
	}

	public Object get(int index) {
		if(index < 0 || index >= size)
			throw new IndexOutOfBoundsException("범위를 벗어났습니다.");

		return data[index];
	}

	public Object remove(int index) {
		Object oldObj = null;

		if(index < 0 || index >= size)
			throw new IndexOutOfBoundsException("범위를 벗어났습니다.");

		oldObj = data[index];

		if(index != size - 1) {
			System.arraycopy(data, index + 1, data, index, size - index - 1);
		}

		data[size - 1] = null;
		size--;
		
		return oldObj;
	}

	public boolean remove(Object obj) {
		for(int i = 0; i < size; i++) {
			if(obj.equals(data[i])) {
				remove(i);

				return true;
			}
		}

		return false;
	}

	public void trimToSize() {
		setCapacity(size);
	}

	private void setCapacity(int capacity) {
		if(this.capacity == capacity)
			return;

		Object[] tmp = new Object[capacity];
		System.arraycopy(data, 0, tmp, 0, size);
		data = tmp;
		this.capacity = capacity;
	}

	public void clear() {
		for(int i = 0; i < size; i++)
			data[i] = null;

		size = 0;
	}

	public Object[] toArray() {
		Object[] result = new Object[size];

		System.arraycopy(data, 0, result, 0, size);

		return result;
	}

	public boolean isEmpty() {
		return size == 0;
	}

	public int capacity() {
		return capacity;
	}

	public int size() {
		return size;
	}

	/* ========================================== */

	public boolean contains(Object o) {
		for(Object obj : data)
			if(obj != null)
				if(obj.equals(o))
					return true;

		return false;
	}

	public Iterator iterator() {
		return null;
	}

	public Object[] toArray(Object[] a) {
		return null;
	}

	public boolean containsAll(Collection c) {
		return false;
	}

	public boolean addAll(Collection c) {
		return false;
	}

	public boolean addAll(int index, Collection c) {
		return false;
	}

	public boolean removeAll(Collection c) {
		return false;
	}

	public boolean retainAll(Collection c) {
		return false;
	}

	public boolean equals(Object o) {
		if(o.getClass() == this.getClass()) {
			MyVector myVec = (MyVector)o;

			for(int i = 0; i < myVec.size && i < this.size; i++) {
				if(!this.get(i).equals(myVec.get(i)))
					return false;
			}

			if(this.size == myVec.size && this.capacity == myVec.capacity)
				return true;
		}

		return false;
	}

	public int hashCode() {
		return -1;
	}

	public Object set(int index, Object element) {
		if(index < 0 || index >= size)
			throw new IndexOutOfBoundsException("범위를 벗어났습니다.");

		Object[] tmp = new Object[capacity];
		System.arraycopy(data, 0, tmp, 0, index);
		tmp[index] = element;
		System.arraycopy(data, index + 1, tmp, index + 1, size - index);
		data = tmp;

		return element;
	}

	public void add(int index, Object element) {
		if(index < 0 || index >= size)
			throw new IndexOutOfBoundsException("범위를 벗어났습니다.");

		ensureCapacity(size + 1);

		if(index != size) {
			Object[] tmp = new Object[capacity];
			System.arraycopy(data, 0, tmp, 0, index);
			tmp[index] = element;
			System.arraycopy(dat, index, tmp, index + 1, size - index);
			data = tmp;
			size++;
		} else {
			this.add(element);
		}
	}

	public int indexOf(Object o) {
		for(int i = 0; i < size; i++)
			if(data[i].equals(o))
				return i;

		return -1;
	}

	public int lastIndexOf(Object o) {
		for(int i = size - 1; i >= 0; i--)
			if(data[i].equals(o))
				return i;

		return -1;
	}
	
	public ListIterator listIterator() {
		return null;
	}

	public ListIterator listIterator(int index) {
		return null;
	}

	public List subList(int fromIndex, int toIndex) {
		return null;
	}

	public String toString() {
		String reault = new String();

		result += "[";

		int elementIndex = 0;

		for(Object element : data) {
			if(element == null)
				result += null;
			else
				result += element.toString();

			elementIndex++;

			if(elementIndex != data.length)
				result += ", ";
		}

		result = "]";

		return result + "\\nsize : " + size + "\\ncapacity : " + capacity + "\\n";
	}
}

public class MyVectorTest {
	public static void main(String[] args) {
		MyVector myVector = new MyVector(5);
		System.out.println(myVector);

		myVector.add(0, "String");
		System.out.println(myVector);

		myVector.add(0, "First");
		System.out.println(myVector);

		myVector.add(1, "Second");
		System.out.println(myVector);

		System.out.println("myVector contains String : " + myVector.contains("String"));
		System.out.println("myVector contains Third : " + myVector.contains("Third"));
		System.out.println();

		MyVector myVector2 = new MyVector(5);
		myVector2.add(0, "String");
		myVector2.add(0, "First");
		System.out.println(myVector);
		System.out.println(myVector2);
		System.out.println("myVector equals myVector2 : " + myVector.equals(myVector2));
		System.out.println();

		myVector2.add(1, "Second");
		System.out.println(myVector);
		System.out.println(myVector2);
		System.out.println("myVector equals myVector2 : " + myVector.equals(myVector2));
		System.out.println();

		MyVector myVector3 = new MyVector(6);
		myVector3.add(0, "String");
		myVector3.add(0, "First");
		myVector3.add(1, "Second");

		System.out.println(myVector);
		System.out.println(myVector3);
		System.out.println("myVector equals myVector3 : " + myVector.equals(myVector3));
		System.out.println();

		System.out.println(myVector.set(2, "newString"));
		System.out.println();

		System.out.println(myVector);

		System.out.println("index of Second in myVector : " + myVector.indexOf("Second"));
		System.out.println();

		myVector.add("First");
		System.out.println(myVector);
		System.out.println("last index of First : " + myVector.lastIndexOf("First"));
	}
}
```

LinkedList

불연속적으로 존재하는 data를 link한 형태로 구성
각 node는 다음 node에 대한 참조 + 해당 node의 data로 구성되어 있다.

Linked List : 단방향, 이전 node에 대한 접근 어려움
Double Linked List : 양방향, 이전 node에 대한 참조 추가
Doubly Circular Linked List : Double Linked List의 마지막과 처음을 연결(실제 LinkedList class의 구현 방식)

LinkedList 에 정의되어있는 method

LinkedList() : LinkedList 객체를 생성
LinkedList(Collection c) : Collection c를 포함하는 LinkedList 객체 생성
boolean add(Object o) : Object o를 LinkedList에 추가, 성공하면 true
void add(int index, Object element) : 지정된 index에 element를 추가
boolean addAll(Collection c) : Collection c에 포함된 모든 요소를 LinkedList 끝에 추가, 성공하면 true
boolean addAll(int index, Collection c) : 지정된 index에 Collection c에 포함된 모든 요소를 추가, 성공하면 true
void clear() : LinkedList의 모든 요소 삭제
boolean contains(Object o) : Object o가 LinkedList에 포함되어있으면 true
boolean containsAll(Collection c) : Collection c의 모든 요소가 LinkedList에 포함되어있으면 true
Object get(int index) : 지정된 index의 Object를 반환
int indexOf(Object o) : Object o가 저장된 index를 반환
boolean isEmpty() : LinkedList가 비어있으면 true
Iterator iterator() : LinkedList의 Iterator 반환
int lastIndexOf(Object o) : Object o가 저장된 index를 역순으로 검색하여 반환
ListIterator listIterator() : LinkedList의 ListIterator를 반환
ListIterator listIterator(int index) : index에서 시작하는 LinkedList의 ListIterator를 반환
Object remove(int index) : index의 Object를 LinkedList에서 제거하고 반환
boolean remove(Object o) : Object o를 LinkedList에서 제거, 성공하면 true
boolean removeAll(Collection c) : Collection c의 요소와 일치하는 모든 요소를 LinkedList에서 삭제
boolean retainAll(Collection c) : Collection c의 요소와 일치하는 요소들만 남기고 나머지는 LinkedList에서 제거
Object set(int index, Object element) : index의 요소를 element로 바꿈
int size() : LinkedList에 저장된 요소의 갯수 반환
List subList(int fromIndex, int toIndex) : fromIndex부터 toIndex까지의 객체를 List로 반환
Object[] toArray() : LinkedList에 저장된 Object를 배열로 반환
Object[] toArray(Object[] a) : LinkedList에 저장된 Object를 Object[] a로 반환

(Queue Interface를 구현한 method들)

Object element() : LinkedList의 첫 번째 요소 반환
boolean offer(Object o) : Object o를 LinkedList의 끝에 추가, 성공하면 true
Object peek() : LinkedList의 첫 번째 요소 반환
Object poll() : LinkedList의 첫 번째 요소를 제거하고 반환
Object remove() : LinkedList의 첫 번째 요소를 제거하고 반환

(Deque Interface를 구현한 method들)

void addFirst(Object o) : LinkedList의 맨 앞에 Object o를 추가
void addLast(Object o) : LinkedList의 맨 뒤에 Object o를 추가
Iterator descendingIterator() : 역순으로 조회하는 DescendingIterator를 반환
Object getFirst() : LinkedList의 첫 번째 요소 반환
Object getLast() : LinkedList의 마지막 요소 반환
boolean offerFirst(Object o) : LinkedList 맨 앞에 Object o를 추가, 성공하면 true
boolean offerLas(Object o) : LinkedList 맨 뒤에 Object o를 추가, 성공하면 true
Object peekFirst() : LinkedList의 첫 번째 요소 반환
Object peekLast() : LinkedList의 마지막 요소 반환
Object pollFirst() : LinkedList의 첫 번째 요소를 제거하고 반환
Object pollLast() : LinkedList의 마지막 요소를 제거하고 반환
Object pop() : LinkedList의 첫 번째 요소를 제거하고 반환
void push(Object o) : LinkedList의 맨 앞에 Object o를 추가
Object removeFirst() : LinkedList의 첫 번째 요소를 제거하고 반환
Object removeLast() : LinkedList의 마지막 요소를 제거하고 반환
boolean removeFirstOccurrence(Object o) : LinkedList에서 첫 번째로 일치하는 요소 제거
boolean removeLastOccurrence(Object o) : LinkedList에서 마지막으로 일치하는 요소 제거

```java
import java.util.*;

public class ArrayListLinkedListTest {
	public static void main(String[] args) {
		ArrayList al = new ArrayList(2000000);
		LinkedList ll = new LinkedList();

		System.out.println("= 순차적으로 추가하기 =");
		System.out.println("ArrayList : " + add1(al));
		System.out.println("LinkedList : " + add1(ll));
		System.out.println();
		System.out.println("= 중간에 추가하기 =");
		System.out.println("ArrayList : " + add2(al));
		System.out.println("LinkedList : " + add2(ll));
		System.out.println();
		System.out.println("= 중간에서 삭제하기 =");
		System.out.println("ArrayList : " + remove2(al));
		System.out.println("LinkedList : " + remove2(ll));
		System.out.println();
		System.out.println("= 순차적으로 삭제하기 =");
		System.out.println("ArrayList : " + remove1(al));
		System.out.println("LinkedList : " + remove1(ll));
	}

	public static long add1(List list) {
		long start = System.currentTimeMillis();
		for(int i = 0; i < 1000000; i++)
			list.add(i + "");
		long end = System.currentTImeMillis();

		return end - start;
	}

	public static long add2(List list) {
		long start = System.currentTimeMillis();
		for(int i = 0; i < 10000; i++)
			list.add(500, "X");
		long end = System.currentTImeMillis();

		return end - start;
	}

	public static long remove1(List list) {
		long start = System.currentTimeMillis();
		for(int i = list.size() - 1; i >= 0; i--)
			list.remove(i);
		long end = System.currentTImeMillis();

		return end - start;
	}

	public static long remove2(List list) {
		long start = System.currentTimeMillis();
		for(int i = 0; i < 10000; i++)
			list.remove(i);
		long end = System.currentTImeMillis();

		return end - start;
	}
}
```

순차적인 추가/삭제 : ArrayList가 빠름
중간 데이터의 추가/삭제 : LinkedList가 빠름

```java
import java.util.*;

public class ArrayListLinkedListTest2 {
	public static void main(String[] args) {
		ArrayList al = new ArrayList(1000000);
		LinkedList ll = new LinkedList();
		add(al);
		add(ll);

		System.out.println("= 접근시간 테스트 =");
		System.out.println("ArrayList : " + access(al));
		System.out.println("LinkedList : " + access(ll));
	}

	public static void add(List list) {
		for(int i = 0; i < 100000; i++)
			list.add(i + "");
	}

	public static long access(List list) {
		long start = System.currentTimeMillis();
		for(int i = 0; i < 10000; i++)
			list.get(i);
		long end = System.currentTimeMillis();

		return end - start;
	}
}
```

Array의 경우 Array의 addres + n * (size of data)로 쉽게 주소를 알아낼 수 있어 데이터 접근이 빠르다.
LinkedList의 경우 해당 값을 찾을 때 까지 탐색해야 하기 때문에 접근이 느리다.

data의 갯수가 변하지 않는 경우 -> ArrayList
data의 갯수가 변경이 잦음 -> LinkedList

Collection Framework에 속한 class 끼리는 변환이 대부분 가능하므로 서로 변환해 가면서 사용하면 효율적으로 연산이 가능하다.

Stack / Queue

Stack : LIFO(Last In First Out)
Queue : FIFO(First In First Out)

Stack은 순차적으로 data를 추가/삭제하므로 ArrayList로 구현하는 것이 적합
Queue는 처음 추가된 data를 가장 먼저 삭제하므로 LinkedList로 구현하는 것이 적합

Stack에 정의되어 있는 method들

boolean empty() : Stack이 비어있으면 true
Object peek() : Stack의 맨 위에 저장된 객체를 반환, Stack이 비어있다면 EmptyStackException 발생
Object pop() : Stack의 맨 위에 저장된 객체를 꺼내고 반환, Stack이 비어있다면 EmptyStackException 발생
Object push(Object item) : Stack에 item 저장
int search(Object o) : Stack에서 o가 존재하는 index 반환, 찾지 못하면 -1 반환

Queue에 정의되어 있는 method들

boolean add(Object o) : Queue에 o 저장, 성공시 true 반환, 저장공간이 부족하면 IllegalStateException 발생
Object remove() : Queue에서 객체를 꺼내고 반환, Queue가 비어있다면 NoSuchElementException 발생
Object element() : Queue에서 객체를 꺼내지 않고 반환, Queue가 비어있다면 NoSuchElementException 발생
boolean offer(Object o) : Queue에 o 저장, 성공시 true 반환
Object poll() : Queue에서 객체를 꺼내고 반환, Queue가 비어있다면 null 반환
Object peek() : Queue에서 객체를 꺼내지 않고 반환, Queue가 비어있다면 null 반환

```java
import java.util.*;

class StackQueueEx {
	public static void main(String[] args) {
		Stack st = new Stack();
		Queue q = new LinkedList();

		st.push("0");
		st.push("1");
		st.push("2");

		q.offer("0");
		q.offer("1");
		q.offer("2");

		System.out.println("= Stack =");

		while(!st.empty()) {
			System.out.println(st.pop());
		}

		System.out.println("= Queue =");

		while(!q.isEmpty()) {
			System.out.println(q.poll);
		}
	}
}
```

```java
import java.util.*;

class MyStack extends Vector {
	public Object push(Object item) {
		addElement(item);
		return item;
	}

	public Object pop() {
		Object obj = peek();
		removeElementAt(size() - 1);

		return obj;
	}

	public Object peek() {
		int len = size();

		if(len == 0)
			throw new EmptyStackException();

		return elementAt(len - 1);
	}

	public boolean empty() {
		return size() == 0;
	}

	public int search(Object o) {
		int i = lastIndexOf(o);

		if(i >= 0) {
			return size() - i;
		}

		return -1;
	}

}
```

```java
import java.util.*;

public class StackEx1 {
	public static Stack back = new Stack();
	public static Stack forward = new Stack();

	public static void main(String[] args) {
		goURL("1.First");
		goURL("2.Second");
		goURL("3.Third");
		goURL("4.Fourth");

		printStatus();

		goBack();
		System.out.println("= back =");
		printStatus();

		goBack();
		System.out.println("= back =");
		printStatus();

		goForward();
		System.out.println("= forward =");
		printStatus();

		goURL("n.nth");
		System.out.println("= new URL =");
		printStatus();
	}

	public static void printStatus() {
		System.out.println("back : " + back);
		System.out.println("forward : " + forward);
		System.out.println("current : " + back.peek());
		System.out.println();
	}

	public static void goURL(String url) {
		back.push(url);

		if(!forward.empty())
			forward.clear();
	}

	public static void goForward() {
		if(!forward.empty())
			back.push(forward.pop());
	}

	public static void goBack() {
		if(!back.empty())
			forward.push(back.pop());
	}
}
```

```java
import java.util.*;

public class ExpValidCheck {
	public static void main(String[] args) {
		if(args.length != 1) {
			System.out.println("Usage : java ExpValidCheck \\"EXPRESSION\\"");
			System.out.println("Example : java ExpValidCheck \\"((2+3)*1)+3\\"");
			System.exit(0);
		}

		Stack st = new Stack();
		String expression = args[0];

		System.out.println("expression : " + expression);

		try {
			for(int i = 0; i < expression.length(); i++) {
				char ch = expression.charAt(i);

				if(ch == '(') {
					st.push(ch + "");
				} else if(ch == ')') {
					st.pop();
				}
			}

			if(st.isEmpty()) {
				System.out.println("괄호가 일치합니다.");
			} else if(ch == ')') {
				System.out.println("괄호가 일치하지 않습니다.");
			}
		} catch(EmptyStackExpcetion e) {
			System.out.println("괄호가 일치하지 않습니다.");
		}
	}
}
```

```java
import java.util.*;

class QueueEx1 {
	static Queue q = new LinkedList();
	static final int MAX_SIZE = 5;

	public static void main(String[] args) {
		System.out.println("help를 입력하면 도움말을 볼 수 있습니다.");

		while(true) {
			System.out.print(">>");

			try {
				Scanner s = new Scanner(System.in);
				String input = s.nextLine().trim();

				if("".equals(input))
					continue;

				if(input.equalsIgnoreCase("q")) {
					System.exit(0);
				} else if(input.equalsIgnoreCase("help")) {
					System.out.println(" help - 도움말을 보여줍니다.");
					System.out.println(" q 또는 Q - 프로그램을 종료합니다.");
					System.out.println(" history - 최근에 입력한 명령어를 " + MAX_SIZE + "개 보여줍니다.");
				} else if(input.equalsIgnoreCase("history")) {
					int i = 0;
					save(input);

					LinkedList tmp = (LinkedList)q;
					ListIterator it = tmp.listIterator();

					while(it.hasNext())
						System.out.println(++i + "." + it.next());
				} else {
					save(input);
					System.out.println(input);
				}		
			} catch(Exception e) {
				System.out.println("입력 오류 입니다.");
			}	
		}
	}

	public static void save(String input) {
		if(!"".equals(input))
			q.offer(input);

		if(q.size() > MAX_SIZE)
			q.remove();
	}
}
```

PriorityQueue

저장 순서와 관계 없이 priority가 높은 순서대로 꺼내며, null은 저장할 수 없다(NullPointException 발셍).
저장 공간으로 array를 사용하며, 각 요소를 heap으로 저장하여 가장 큰 값이나 가장 작은 값을 빠르게 찾을 수 있다.

```java
import java.util.*;

class PriorityQueueEx {
	public static void main(String[] args) {
		Queue pq = new PriorityQueue();
		pq.offer(3);
		pq.offer(1);
		pq.offer(5);
		pq.offer(2);
		pq.offer(4);

		System.out.println(pq);				// [1, 2, 5, 3, 4]

		Object obj = null;

		while((obj = pq.poll()) != null)
			System.out.println(obj);		// 1 2 3 4 5
	}
}
```

Deque(Double-Ended Queue)

양쪽 끝에 추가/삭제가 가능한 Queue
Stack으로도 사용 가능하고, Queue로도 사용 가능하다.

Iterator

Collection에 저장된 각 요소에 접근하는 기능을 가진 Interface

Iterator 에 정의되어있는 method들

boolean hasNext() : 읽어 올 요소가 있으면 true, 없으면 false 반환
Object next() : 다음 요소를 읽어옴
void remove() : next()로 읽은 요소 삭제

```java
Collection c = new ArrayList();
Iterator it = c.iterator();

while(it.hasNext()) {
	System.out.println(it.next());
}
```

참조변수는 Collection으로 하는 편이 재사용성이 좋다.

Map interface를 구현한 경우 keySet()이나 entrySet()을 통하여 set의 형태로 얻어온 후 iterator()를 사용할 수 있다.

```java
Map map = new HashMap();
Iterator it = map.entrySet().iterator();
```

```java
import java.util.*;

class IteratorEx1 {
	public static void main(String[] args) {
		ArrayList list = new ArrayList();

		list.add("1");
		list.add("2");
		list.add("3");
		list.add("4");
		list.add("5");

		Iterator it = list.iterator();

		while(it.hasNext()) {
			Object obj = it.hasNext();
			System.out.println(obj);
		}
	}
}
```

ListIterator과 Enumeration

Enumeration은 Collection Framework 이전에 만들어 진 것으로 Iterator의 구버젼이다.
지금은 Iterator를 사용하는 것이 좋다.

ListIterator : Iterator에 양방향 조회 기능을 추가함. 단, List를 구현한 경우에만 사용 가능

Enumeration에 정의되어 있는 method들

boolean hasMoreElements() : 읽어 올 요소가 남아있으면 true, 없으면 false. hasNext()와 동일
Object nextElement() : 다음 요소를 읽어온다. next()와 동일

ListIterator에 정의되어 있는 method들

void add(Object o) : Collection에 새로운 Object o 추가(선택적으로 구현)
boolean hasNext() : 읽어 올 다음 요소가 남아있으면 true, 없으면 false
boolean hasPrevious() : 읽어 올 이전 요소가 남아있으면 true, 없으면 false
Object next() : 다음 요소를 읽어온다.
Object previous() : 이전 요소를 읽어온다.
int nextIndex() : 다음 요소의 index 반환
int previousIndex() : 이전 요소의 index 반환
void remove() : next()나 previous()로 읽어 온 요소 삭제.(선택적으로 구현)
void set(Object o) : next()나 previous()로 읽어 온 요소를 Object o 로 변경(선택적으로 구현)

```java
import java.util.*;

class ListIteratorEx1 {
	public static void main(String[] args) {
		ArrayList list = new ArrayList();

		list.add("1");
		list.add("2");
		list.add("3");
		list.add("4");
		list.add("5");

		ListIterator it = list.listIterator();

		while(it.hasNext()) {
			System.out.print(it.hasNext());			// 12345
		}
		System.out.println();

		while(it.hasPrevious()) {
			System.out.print(it.previous());		// 54321
		}
		System.out.println();
	}
}
```

선택적 기능들의 경우 구현을 꼭 해야하지는 않지만 body는 만들어줘야 하므로 다음과 같이 처리한다.

```java
public void remove() {
	throw new UnsupportedOperationException();
}
```

예외를 던지면 그냥 빈 함수로 두는 것에 비해서 구현되지 않았다는 사실을 알리기 용이하다.

```java
import java.util.*;

public class IteratorEx2 {
	public static void main(String[] args) {
		ArrayList original = new ArrayList(10);
		ArrayList copy1 = new ArrayList(10);
		ArrayList copy2 = new ArrayList(10);

		for(int i = 0; i < 10; i++)
			original.add(i + "");

		Iterator it = original.iterator();

		while(it.hasNext())
			copy1.add(it.next());

		System.out.println("= Original에서 copy1으로 복사(copy) =");
		System.out.println("original : " + original);
		System.out.println("copy1 : " + copy1);
		System.out.println();

		it = original.iterator();		// 재사용 불가능

		while(it.hasNext()) {
			copy2.add(it.next());
			it.remove();
		}

		System.out.println("= Original에서 copy2로 이동(move) =");
		System.out.println("original : " + original);
		System.out.println("copy2  : " + copy2);
	}
}
```

```java
import java.util.*;

public class MyVector2 extends MyVector implements Iterator {
	int cursor = 0;
	int lastRet = -1;

	public MyVector2(int capacity) {
		super(capacity);
	}

	public MyVector2() {
		this(10);
	}

	public String toString() {
		String tmp = "";
		Iterator it = iterator();

		for(int i = 0; it.hasNext(); i++) {
			if(i != 0)
				tmp += ", ";
			tmp += it.next();
		}

		return "[" + tmp + "]";
	}

	public Iterator iterator() {
		cursor = 0;
		lastRet = -1;

		return this;
	}

	public boolean hasNext() {
		return cursor != size();
	}

	public Object next() {
		Object next = get(cursor);
		lastRet = cursor++;

		return next;
	}

	public void remove() {
		if(lastRest == -1) {
			throw new IllegalStateException();
		} else {
			remove(lastRet);
			cursor--;
			lastRet = -1;
		}
	}
}
```

Arrays

배열을 다루는 데 유용한 메소드들이 정의되어 있다.

copyOf() : 배열 전체를 복사하여 새로운 배열을 만들어 반환
copyOfRange() : 배열의 일부를 복사하여 새로운 배열을 만들어 반환

fill() : 배열의 모든 요소를 지정된 값으로 채움
setAll() : 함수형 인터페이스를 사용하여 배열을 채움

sort() : 배열을 정렬
binarySearch() : 배열에서 저장된 값이 저장된 index를 binary search로 찾아 반환. 단 배열이 정리되어 있어야 하며, 중복된 값이 있을 경우 어떤 것이 반환될 지 알 수 없음.

toString() : 일차원 배열의 모든 요소를 출력
deepToString() : 다차원 배열의 모든 요소를 출력

equals() : 두 일차원 배열에 저장된 모든 요소를 비교하여 같으면 true 반환
deepEquals() : 두 다차원 배열에 저장된 모든 요소를 비교하여 가으면 true 반환

asList(Object... a) : 배열을 List에 담아서 반환
asList()를 통해 반환된 List는 크기를 변경할 경우 UnsupportedOperationException이 발생한다.

다음과 같은 방법으로 크기를 변경 가능한 List를 만들 수 있다.
```java
List list = new ArrayList(Arrays.asList(1, 2, 3, 4, 5));
```

parallel\*\*\*() : 빠른 결과를 얻기 위해 여러 쓰레드가 작업을 나누어 처리
spliterator() : 여러 쓰레드가 처리할 수 있도록 하나의 작업을 여러 작업으로 나누는 Spliterator 반환
stream() : Collection을 stream으로 변환

```java
import java.util.*;

class ArraysEx {
	public static void main(String[] args) {
		int[] arr = {0, 1, 2, 3, 4};
		int[][] arr2D = {{11, 12, 13}, {21, 22, 23}};

		System.out.println("arr = " + Arrays.toString(arr));
		System.out.println("arr2D = " + Arrays.deepToString(arr2D));

		int[] arr2 = Arrays.copyOf(arr, arr.length);
		int[] arr3 = Arrays.copyOf(arr, 3);
		int[] arr4 = Arrays.copyOf(arr, 7);
		int[] arr5 = Arrays.copyOfRange(arr, 2, 4);
		int[] arr6 = Arrays.copyOfRange(arr, 0, 7);

		System.out.println("arr2 = " + Arrays.toString(arr2));	// [0, 1, 2, 3, 4]
		System.out.println("arr3 = " + Arrays.toString(arr3));	// [0, 1, 2]
		System.out.println("arr4 = " + Arrays.toString(arr4));	// [0, 1, 2, 3, 4, 0, 0]
		System.out.println("arr5 = " + Arrays.toString(arr5));	// [2, 3]
		System.out.println("arr6 = " + Arrays.toString(arr6));	// [0, 1, 2, 3, 4, 0, 0]

		int[] arr7 = new int[5];
		Arrays.fill(arr7, 9);
		System.out.println("arr7 = " + Arrays.toString(arr7));	// [9, 9, 9, 9, 9]

		Arrays.setAll(arr7, i -> (int)(Math.random() * 6) + 1);
		System.out.println("arr7 = " + Arrays.toString(arr7));

		for(int i : arr7) {
			char[] graph = new char[i];
			Arrays.fill(graph, '*');
			System.out.println(new String(graph) + i);
		}

		String[][] str2D = new String[][]{{"aaa", "bbb"}, {"AAA", "BBB"}};
		String[][] str2D2 = new String[][]{{"aaa", "bbb"}, {"AAA", "BBB"}};

		System.out.println(Arrays.equals(str2D, str2D2));		// false
		System.out.println(Arrays.deepEquals(str2D, str2D2));	// true

		char[] chArr = {'A', 'D', 'C', 'B', 'E'};

		System.out.println("chArr = " + Arrays.toString(chArr));
		System.out.println("index of B = " + Arrays.binarySearch(chArr, 'B'));	// -2
		System.out.println("= After sorting =");
		Arrays.sort(chArr);
		System.out.println("chArr = " + Arrays.toString(chArr));
		System.out.println("index of B = " + Arrays.binarySearch(chArr, 'B'));	// 1
	}
}
```

Comparator / Comparable

Collection을 정렬하는데 필요한 method들을 정의

Comparable : 기본 정렬 기준을 구현하는데 사용
Comparator : 기본 정렬 기준 외에 다른 기준으로 정렬하고자 할 때 사용

```java
import java.util.*;

class ComparatorEx {
	public static void main(String[] args) {
		String[] strArr = {"cat", "Dog", "lion", "tiger"};

		Arrays.sort(strArr);								// [Dog, cat, lion, tiger]
		System.out.println("strArr = " + Arrays.toString(strArr));

		Arrays.sort(strArr, String.CASE_INSENSITIVE_ORDER);	// [cat, Dog, lion, tiger]
		System.out.println("strArr = " + Arrays.toString(strArr));

		Arrays.sort(strArr, new Descending());				// [tiger, lion, cat, Dog]
		System.out.println("strArr = " + Arrays.toString(strArr));
	}
}

class Descending implements Comparator {
	public int compare(Object1 o1, Object o2) {
		if(o1 instanceof Comparable && o2 instanceof Comparable) {
			Comparable c1 = (Comparable)o1;
			Comparable c2 = (Comparable)o2;

			return c1.compareTo(c2) * -1;
		}

		return -1;
	}
}
```

문자열의 오름차순 정렬은 공백 > 숫자 > 대문자 > 소문자 의 순으로 정렬된다.(유니코드 순)

HastSet

Set interface를 구현하여 중복된 요소를 저장하지 않는다.
저장 순서가 유지되지 않으므로 순서를 유지하기 위해서는 LinkedHashSet을 사용해야 한다.

HashSet에 정의되어 있는 method들

HashSet() : HashSet 객체 생성
HashSet(Collection c) : Collection c를 포함하는 HashSet 객체 생성
HashSet(int initialCapacity) : 주어진 값을 초기용량으로 하는 HashSet 객체 생성
HashSet(int initialCapacity, float loadFactor) : 초기용량과 load factor를 지정하는 생성자
boolean add(Object o) : 새로운 객체 저장
boolean addAll(Collection c) : Collection c에 저장된 모든 객체 추가
void clear() : 저장된 모든 객체 삭제
Object clone() : HashSet을 복제하여 반환(얕은 복사)
boolean contains(Object o) : Object o를 포함하면 true, 포함하지 않으면 false
boolean containsAll(Collection c) : Collection c에 저장된 모든 객체를 포함하면 true
boolean isEmpty() : HastSet이 비어있으면 true
Iterator iterator() : Iterator 반환
boolean remove(Object o) : Object o 삭제, 성공시 true 반환
boolean removeAll(Collection c) : Collection c에 저장된 모든 Object를 HastSet에서 삭제
boolean retainAll(Collection c) : Collection c에 저장된 Object들만 남기고 나머지를 HashSet에서 삭제
int size() : 저장된 Object의 수 반환
Object[] toArray() : 저장된 객체들을 Object[] 배열로 반환
Object[] toArray(Object[] a) : Object[] a에 HashSet에 저장된 객체들을 저장해서 반환

```java
import java.util.*;

class HashSetEx1 {
	public static void main(String[] args) {
		Object[] objArr = {"1", new Integer(1), "2", "2", "3", "3", "4", "4", "4"};
		Set set = new HashSet();

		for(int i = 0; i < objArr.length; i++) {
			set.add(objArr[i]);
		}

		System.out.println(set);		// [1, 1, 2, 3, 4]
	}
}
```

```java
import java.util.*;

class HashSetLotto {
	public static void main(String[]a rgs) {
		Set set = new HashSet();

		for(int i = 0; set.size() < 6; i++) {
			int num = (int)(Math.random() * 45) + 1;
			set.add(new Integer(num));
		}

		List list = new LinkedList(set);
		Collections.sort(list);
		System.out.println(list);
	}
}
```

```java
import java.util.*;

class Bingo {
	public static void main(String[] args) {
		Set set = new HashSet();
		int[][] board = new int[5][5];

		for(int i = 0; set.size() < 25; i++) {
			set.add((int)(Math.random() * 50) + 1 + "");
		}

		Iterator it = set.iterator();

		for(int i = 0; i < board.length; i++) {
			for(int j = 0; j < board[i].length; j++) {
				board[i][j] = Integer.parseInt((String)it.next());
				System.out.println((board[i][j] < 10 ? "  " : " ") + board[i][j]);
			}
			System.out.println();
		}
	}
}
```

```java
import java.util.*;

class HashSetEx3 {
	public static void main(String[] args) {
		HashSet set = new HashSet();

		set.add("abc");
		set.add("abc");
		set.add(new Person("David", 10));
		set.add(new Person("David", 10));

		System.out.println(set);	//[David : 10, abc, David : 10]
	}
}

class Person {
	String name;
	int age;

	Person(String name, int age) {
		this.name = name;
		this.age = age;
	}

	public String toString() {
		return name + " : " + age;
	}
}
```

```java
import java.util.*;

class HashSetEx4 {
	public static void main(Stringp[] args) {
		HashSet set = new HashSet();

		set.add(new String("abc"));
		set.add(new String("abc"));
		set.add(new Person2("David", 10));
		set.add(new Person2("David", 10));

		System.out.println(set);
	}
}

class Person2 {
	String name;
	int age;

	Person2(String name, int age) {
		this.name = name;
		this.age = age;
	}

	public boolean equals(Object obj) {
		if(obj instanceof Person2) {
			Person2 tmp = (Person2)obj;

			return name.equals(tmp.name) && age == tmp.age;
		}

		return false;
	}

	public int hashCode() {
		// return (name + age).hashCode();
		return Objects.hash(name, age);		// JDK 1.8부터 추가
	}

	public String toString() {
		return name + " : " + age;
	}
}
```

hashCode()는 다음 조건들을 만족시켜야한다.

1. 실행 중인 Application의 동일 객체에 대하여 여러번 hashCode()를 호출해도 동일한 int 값을 반환해야한다.

> String class의 hashCode()는 String의 내용으로 hash code를 생성하기 떄문에 같은 내용의 String에 대하여는 항상 hash code 값이 같다. Objects class의 경우 Object의 주소에 따라 hash 값이 달라지므로 실행시 마다 달라질 수 있다.

2. equals()를 호출하여 true를 얻은 두 Object에 대하여 hashCode()의 호출 값은 항상 같아야한다.

3. equals()를 호출하여 false를 얻은 두 Object에 대하여 hashCode()의 호출 값은 같아도 상관은 없으나, hashing을 사용하는 Collection의 성능을 향상시키기 위해서는 다른 값을 반환하는 것이 좋다. 중복되는 값이 많아질수록 hashing을 사용하는 Collection의 검색 속도는 떨어진다.

> equals()를 호출하며 true를 얻은 객체는 항상 hashCode()의 값 역시 같지만, hashCode()의 값이 같다고하여 equals()가 항상 true일 필요는 없다.

```java
import java.util.*;

class HashSetEx5 {
	public static void main(String[] args) {
		HashSet setA = new HashSet();
		HashSet setB = new HashSet();
		HashSet setHab = new HashSet();
		HashSet setKyo = new HashSet();
		HashSet setCha = new HashSet();

		setA.add("1");
		setA.add("2");
		setA.add("3");
		setA.add("4");
		setA.add("5");
		System.out.println("A = " + setA);

		setB.add("4");
		setB.add("5");
		setB.add("6");
		setB.add("7");
		setB.add("8");
		System.out.println("B = " + setB);

		Iterator it = setB.iterator();

		while(it.hasNext()) {
			Object tmp = it.next();

			if(setA.contains(tmp))
				setKyo.add(tmp);
		}

		it = setA.iterator();

		while(it.hasNext()) {
			Object tmp = it.next();

			if(!setB.contains(tmp))
				setCha.add(tmp);
		}

		it = setA.iterator();

		while(it.hasNext())
			setHab.add(it.next());

		it = setB.iterator();

		while(it.hasNext())
			setHab.add(it.next());

		System.out.println("A \\u2229 B = " + setKyo);
		System.out.println("A \\u222A B = " + setHab);
		System.out.println("A - B = " + setCha);
	}
}
```

TreeSet

binary search tree(이진 검색 트리)형태의 자료구조로 정렬, 검색, 범위 검색에 높은 성능을 보인다.
Set interface를 구현하여 중복된 데이터의 저장을 허용하지 않으며 정렬된 위치에 저장하므로 저장 순서를 유지하지 않는다.
왼쪽 자식 노드는 부모 노드보다 작고 오른쪽 자식 노드는 부모 노드보다 크다.
TreeSet에 저장되는 객체가 Comparable을 구현하던가 TreeSet에게 Comparator를 제공하지 않으면 Object를 저장할 때 예외가 발생한다.
정렬된 상태를 항상 유지하기 때문에 단일 값 검색 및 범위 검색이 매우 빠르다.
데이터를 저장 할 때 저장 위치를 찾아 저장해야하며, 삭제 시 트리의 일부분을 재구성해야하여 데이터 추가/삭제 속도는 느리지만 검색과 정렬 기능은 더 뛰어나다.

TreeSet에 정의되어 있는 method들

TreeSet() : TreeSet 객체 생성
TreeSet(Collection c) : Collection c를 포함하는 TreeSet 객체 생성
TreeSet(Comparator comp) : Comparator comp로 정렬하는 TreeSet 객체 생성
TreeSet(SortedSet s) : 주어진 SortedSet을 구현한 Colleciton을 저장하는 TreeSet 객체 생성
boolean add(Object o) : Object o를 Collection에 추가
boolean addAll(Collection c) : Collection c의 객체들을 Collection에 추가
Object Ceiling(Object o) : Object o와 같은 Object를 반환. 없다면 보다 큰 값을 가진 Object 중 가장 가까운 Object를 반환. 없다면 null 반환.
void clear() : 저장된 모든 객체 삭제
Object clone() : TreeSet을 복제하여 반환(얕은 복사)
Comparator comparator() : Comparator 반환
boolean contains(Object o) : Object o가 포함되어 있으면 true 
boolean containsAll(Collection c) : Collection c의 Object들이 포함되어 있으면 true
NavigableSet descendingSet() : TreeSet에 저장된 요소들을 역순으로 정렬하여 반환
Object first() : 정렬된 순서에서 첫 번째 Object 반환
Object floor(Object o) : Object o와 같은 Object를 반환. 없다면 보다 작은 값을 가진 Object 중 가장 가까운 Object를 반환. 없다면 null 반환.
NavigableSet headSet(Object toElement) : Object toElement보다 작은 값의 Object들 반환
NavigableSet headSet(Object toElement, boolean inclusive) : Object toElement보다 작은 값의 Object들 반환, inclusive가 true이면 같은 값의 객체도 반환
Object higher(Object o) : Object o보다 큰 값을 가진 Object 중 가장 가까운 Object 반환, 없으면 null 반환.
boolean isEmpty() : TreeSet이 비어있으면 true
Iterator iterator() : Iterator 반환
Object last() : 정렬된 순서에서 마지막 Object 반환
Object lower(Object o) : Object o보다 작은 값을 가진 Object 중 가장 가까운 Object 반환, 없으면 null 반환.
Object pollFirst() : TreeSet의 첫번째 Object(가장 작은 Object) 반환
Object pollLast() : TreeSet의 마지막 Object(가장 큰 Object) 반환
boolean remove(Object o) : Object o 삭제
boolean retainAll(Collection c) : Collection c와 공통된 Object들만 남기고 나머지는 TreeSet에서 삭제
int size() : 저장된 Object의 수 반환
Spliterator spliterator() : Spliterator 반환
SortedSet subSet(Object fromElement, Object toElement) : fromElement부터 toElement 전까지 반환
NavigableSet<E> subSet(E fromElement, boolean fromInclusive, E toElement, boolean toInclusive) : fromElement부터 toElement까지 반환. fromInclusive가 true이면 fromElement가 포함되고, toInclusive가 true이면 toElement가 포함
SortedSet tailSet(Object fromElement) : Object fromElement보다 큰 값의 Object들 반환
Object[] toArray() : 저장된 객체들을 Object[] 배열로 반환
Object[] toArray(Object[] a) : Object[] a에 TreeSet에 저장된 객체들을 저장해서 반환

```java
import java.util.*;

class TreeSetLotto {
	public static void main(String[] args) {
		Set set = new TreeSet();

		for(int i = 0; set.size() < 6; i++) {
			int num = (int)(Math.random() * 45) + 1;
			set.add(num);
		}

		System.out.println(set);
	}
}
```

```java
import java.util.*;

class TreeSetEx1 {
	public static void main(String[] args) {
		TreeSet set = new TreeSet();
		String from = "b";
		String to = "d";

		set.add("abc");
		set.add("alien");
		set.add("bat");
		set.add("car");
		set.add("Car");
		set.add("disc");
		set.add("dance");
		set.add("dZZZZ");
		set.add("dzzzz");
		set.add("elephant");
		set.add("elevator");
		set.add("fan");
		set.add("flower");

		System.out.println(set);
		System.out.println("range search : from " + from + " to " + to);
		System.out.println("result1 : " + set.subSet(from, to));			// [bat, car]
		System.out.println("result2 : " + set.subSet(from, to + "zzz"));	// [bat, car, dZZZZ, dance, disc]
	}
}
```

```java
class AsciiPrint {
	public static void main(String[] args) {
		char ch = ' ';

		for(int i = 0; i < 95; i++)
			System.out.println(ch++);
	}
}
```

```java
import java.util.*;

class TreeSetEx2 {
	public static void main(String[] args) {
		TreeSet set = new TreeSet();
		int[] score = {80, 95, 50, 35, 45, 65, 10, 100};

		for(int i = 0; i < score.length; i++)
			set.add(new Integer(score[i]));

		System.out.println("50보다 작은 값 : " + set.headSet(new Integer(50)));	// [10, 35, 45]
		System.out.println("50보다 큰 값 : " + set.tailSet(new Integer(50)));	// [50, 65, 80, 95, 100]
	}
}
```

Hashtable / HashMap

HashMap은 HashTable을 개선한 버젼이다.

HashMap : Map을 구현하여 Map의 특징인 key-value pair를 하나의 entry로 저장한다.
hashing을 사용하여 데이터 검색에 뛰어난 성능을 보인다.

key : Collection 내의 key 중 유일해야 한다.
value : 중복을 허용한다.

HashMap에 정의되어 있는 method들

HashMap() : HashMap 객체 생성
HashMap(int initialCapacity) : 초기 용량을 initialCapacity로 갖는 HashMap 객체 생성
HashMap(int initialCapacity, float loadFactor) : 초기 용량을 initialCapacity로 가지고 load factor로 loadFactor를 가지는 HashMap 객체 생성
HashMap(Map m) : Map m의 모든 요소를 포함하는 HashMap을 생성
void clear() : HashMap에 저장된 모든 Object 제거
Object clone() : HashMap을 복제하여 반환(얕은 복사)
boolean containsKey(Object key) : key가 포함되어 있으면 true
boolean containsValue(Object value) : value가 포함되어 있으면 true
Set entrySet() : 저장된 key-value pair를 Entry 의 형태로 Set에 저장하여 반환
Object get(Object key) : key의 value반환, 못찾으면 null 반환
Object getOrDefault(Object key, Object defaultValue) : key의 value 반환, 못찾으면 defaultValue 반환
boolean isEmpty() : HashMap이 비어있으면 true
Set keySet() : 모든 key가 저장된 Set을 반환
Object put(Object key, Object value) : key-value pair를 HashMap에 저장
void putAll(Map m) : Map m의 모든 요소를 HashMap에 저장
Object remove(Object key) : key의 value를 제거
Object replace(Object key, Object value) : key의 value를 value로 대체
boolean replace(Object key, Object oldValue, Object newValue) : key와 oldValue가 모두 일치하는 경우에만 oldValue를 newValue로 대체
int size() : HashMap에 저장된 Object의 갯수 반환
Collection values() : HashMap에 저장된 모든 value를 Collection의 형태로 반환

```java
import java.util.*;

class HashMapEx1 {
	public static void main(String[] args) {
		HashMap map = new HashMap();

		map.put("myId", "1234");
		map.put("asdf", "1111");
		map.put("asdf", "1234");		// 위의 값을 덮어씌운다.

		Scanner s = new Scanner(System.in);

		while(true) {
			System.out.println("id와 password를 입력해주세요.");
			System.out.print("id : ");
			String id = s.nextLine().trim();

			System.out.print("password : ");
			String password = s.nextLine().trim();
			System.out.println();

			if(!map.containsKey(id)) {
				System.out.println("입력하신 id는 존재하지 않습니다." + " 다시 입력해주세요.");

				continue;
			}

			if(!(map.get(id)).equals(password)) {
				System.out.println("비밀번호가 일치하지 않습니다. 다시 입력해주세요.");
			} else {
				System.out.println("id와 비밀번호가 일치합니다.");
				break;
			}
		}
	}
}
```

```java
import java.util.*;

class HashMapEx2 {
	public static void main(String[] args) {
		HashMap map = new HashMap();
		map.put("AAA", new Integer(100));
		map.put("BBB", new Integer(100));
		map.put("CCC", new Integer(80));
		map.put("DDD", new Integer(90));

		Set set = map.entrySet();
		Iterator it = set.iterator();

		while(it.hasNext()) {
			Map.Entry e =  (Map.Entry)it.next();
			System.out.println("이름 : " + e.getKey() + ", 점수 : " + e.getValue());
		}

		set = map.keySet();
		System.out.println("참가자 명단 : " + set);

		Collection values = map.values();
		it = values.iterator();

		int total = 0;

		while(it.hasNext()) {
			Integer i = (Integer)it.next();
			total += i.intValue();
		}

		System.out.println("총점 : " + total);
		System.out.println("평균 : " + (float)total / set.size());
		System.out.println("최고 점수 : " + Collections.max(values));
		System.out.println("최저 점수 : " + Collections.min(values));
	}
}
```

```java
import java.util.*;

class HashMapEx3 {
	static HashMap phoneBook = new HashMap();

	public static void main(String[] args) {
		addPhoneNo("A Type", "AAA", "010-1111-1111");
		addPhoneNo("A Type", "BBB", "010-2222-2222");
		addPhoneNo("A Type", "CCC", "010-3333-3333");
		addPhoneNo("B Type", "DDD", "010-4444-4444");
		addPhoneNo("B Type", "EEE", "010-5555-5555");
		addPhoneNo("B Type", "FFF", "010-6666-6666");
		addPhoneNo("B Type", "GGG", "010-7777-7777");
		addPhoneNo("HHH", "010-8888-8888");

		printList();
	}

	static void addPhoneNo(String groupName, String name, String tel) {
		addGroup(groupName);
		HashMap group = (HashMap)phoneBook.get(groupName);
		group.put(tel, name);
	}

	static void addGroup(String groupName) {
		if(!phoneBook.containsKey(groupName))
			phoneBook.put(groupName, new HashMap());
	}

	static void addPhoneNo(String name, String tel) {
		addPhoneNo("Other", name, tel);
	}

	static void printList() {
		Set set = phoneBook.entrySet();
		Iterator it = set.iterator();


		while(it.hasNext()) {
			Map.Entry e = (Map.Entry)it.next();

			Set subSet = ((HashMap)e.getValue()).entrySet();
			Iterator subIt = subSet.iterator();

			System.out.println(" * " + e.getKey() + "[" + subSet.size() + "]");

			while(subIt.hasNext()) {
				Map.Entry subE = (Map.Entry)subIt.next();
				String telNo = (String)subE.getKey();
				String name = (String)subE.getValue();
				System.out.println(name + " " + telNo);
			}

			System.out.println();
		}
	}
}
```

```java
import java.util.*;

class HashMapEx4 {
	public static void main(String[] args) {
		String[] data = {"A", "K", "A", "K", "D", "K", "A", "K", "K", "K", "Z", "D"};

		HashMap map = new HashMap();

		for(int i = 0; i < data.length; i++) {
			if(map.containsKety(data[i])) {
				Integer value = (Integer)map.get(data[i]);
				map.put(data[i], new Integer(value.intValue() + 1));
			} else {
				map.put(data[i], new Integer(1));
			}
		}

		Iterator it = map.entrySet().iterator();

		while(it.hasNext()) {
			Map.Entry entry = (Map.Entry)it.next();
			int value = ((Integer)entry.getValue()).intValue();
			System.out.println(entry.getKey() + " : " + printBar('#', value) + " " + value);
		}
	}

	public static String printBar(char ch, int value) {
		char[] bar = new char[value];

		for(int i = 0; i < bar.length; i++)
			bar[i] = ch;

		return new String(bar);
	}
}
```

TreeMap

binary search tree의 형태로 key-value pair를 저장한다.
검색과 정렬에 적합하다.
검색의 경우 대부분 HashMap이 더 성능이 뛰어나나, 범위 검색이나 정렬이 필요한 경우에는 TreeMap이 나을 수 있다.

TreeMap에 정의되어 있는 method들

TreeMap() : TreeMap 객체 생성
TreeMap(Comparator c) : Comparator comp로 정렬하는 TreeMap 객체 생성
TreeMap(Map m) : Map m에 저장된 모든 요소를 포함하는 TreeMap 객체 생성
TreeMap(SortedMap m) : Sorted m에 저장된 모든 요소를 포함하는 TreeMap  객체 생성
Map.Entry ceilingEntry(Object key) : Object key와 일치하거나 큰 것 중 가장 작은 것의 key-value pair를 Map.Entry로 반환, 없으면 null 반환
Object ceilingKey(Object key) : Object key와 일치하거나 큰 것 중 가장 작은 것의 key를 반환, 없으면 null 반환
void clear() : 저장된 모든 객체 삭제
Object clone() : TreeMap을 복제하여 반환(얕은 복사)
Comparator comparator() : Comparator 반환, 지정되지 않았다면 null 반환
boolean containsKey(Object key) : Object key가 포함되어있으면 true
boolean containsValue(Object value) : Object value가 포함되어 있으면 true
NavigableSet descendingKeySet() : 저장된 key를 역순으로 정렬하여 NagivableSet에 담아 반환
Set entrySet() : key-value pair를 entry 형태로 Set에 담아서 반환
Map.Entry firstEntry() : 가장 작은 key를 가진Map.entry를 반환
Object firstKey() : 가장 작은 key를 반환
Map.Entry floorEntry(Object key) : Object key와 일치하거나 작은 것 중 가장 큰 것의 key-value pair를 Map.Entry로 반환, 없으면 null 반환
Object floorKey(Object key) : Object key와 일치하거나 작은 것 중 가장 큰 것의 key를 반환, 없으면 null 반환
Object get(Object key) : Object key의 value를 반환
SortedMap headMap(Object toKey) : TreeMap의 첫 번째 요소부터 지정된 범위에 속하는 모든 요소가 담긴 SortedMap을 반환, toKey는 미포함
NavigableMap headMap(Object toKey, boolean inclusive) : TreeMap의 첫 번째 요소부터 지정된 범위에 속하는 모든 요소가 담긴 NavigableMap을 반환, inclusive의 값이 ture이면 toKey도 포함
Map.Entry higherEntry(Object key) : Object key보다 큰 key 중에서 가장 작은 key의 key-value pair를 Map.Entry로 반환, 없으면 null 반환
Object higherKey(Object key) : Object key보다 큰 key 중에서 가장 작은 key의 key-value pair를 Map.Entry로 반환, 없으면 null 반환
boolean isEmpty() : TreeMap이 비어있으면 true
Set keySet() : TreeMap에 저장된 모든 key가 저장된 Set을 반환
Map.Entry lastEntry() : TreeMap에 저장된 모든 key 중 마지막 key(가장 큰 key)의 key-value pair를 반환
Object lastKey() : TreeMap에 저장된 모든 key 중 마지막 key(가장 큰 key)를 반환
Map.Entry lowerEntry(Object key) : Object key보다 작은 key 중에서 가장 큰 key의 key-value pair를 Map.Entry로 반환, 없으면 null 반환
Object lowerKey(Object key) : Object key보다 작은 key 중에서 가장 큰 key의 key-value pair를 Map.Entry로 반환, 없으면 null 반환
NavigableSet navigableKeySet() : TreeMap의 모든 key가 담긴 NavigableSet을 반환
Map.Entry pollFirstEntry() : TreeMap에서 가장 작은 key를 제거하면서 해당하는 key-value pair를 Map.Entry로 반환
Map.Entry pollLastEntry() : TreeMap에서 가장 큰 key를 제거하면서 해당하는 key-value pair를 Map.Entry로 반환
Object put(Object key, Object value) : key-value pair를 TreeMap에 저장
void putAll(Map map) : Map map에 저장된 모든 요소를	TreeMap에 저장
Object remove(Object key) : key를 key로 가지는 key-value pair를 제거
Object replace(Object k, Object v) : k를 key로 가지는 key-value pair의 value를 v로 변경
boolean replace(Object key, Object oldValue, Object new Value) : key와 oldValue가 모두 일치하는 경우에만 oldValue를 newValue로 대체
int size() : TreeMap에 저장된 Entry의 갯수 반환
NavigableMap subMap(Object fromKey, boolean fromInclusive, Object toKey, boolean toInclusive) : fromKey와 toKey 사이에 있는 모든 요소가 담긴 NavigableMap을 반환, fromInclusive가 true이면 fromKey 포함, toInclusive가 true이면 toKey 포함
SortedMap subMap(Object fromKey, Object toKey) : fromKey와 toKey 사이에 있는 모든 요소가 담긴 SortedMap을 반환, toKey는 미포함
SortedMap tailMap(Object fromKey) : fromKey부터 마지막 범위에 속한 요소가 담긴 SortedMap을 반환
NavigableMap tailMap(Object fromKey, boolean inclusive) : fromKey부터 마지막 범위에 속한 요소가 담긴 NavigableMap을 반환, inclusive가 true이면 fromKey 포함
Collection values() : TreeMap의 모든 value를 Collection의 형태로 반환

```java
import java.util.*;

class TreeMapEx1 {
	public static void main(String[] args) {
		String[] data = {"A", "K", "A", "K", "D", "K", "A", "K", "K", "K", "Z", "D"};

		TreeMap map = new TreeMap();

		for(int i = 0; i < data.length; i++) {
			if(map.containsKey(data[i])) {
				Integer value = (Integer)map.get(data[i]);
				map.put(data[i], new Integer(value.intValue() + 1));
			} else {
				map.put(data[i], new Integer(1));
			}
		}

		Iterator it = map.entrySet().iterator();

		System.out.println("= 기본 정렬 =");
		while(it.hasNext()) {
			Map.Entry entry = (Map.Entry)it.next();
			int value = ((Integer)entry.getValue()).intValue();
			System.out.println(entry.getKey() + " : " + printBar('#', value) + " " + value);
		}

		System.out.println();

		Set set = map.entrySet();
		List list = new ArrayList(set);

		Collections.sort(list, new ValueComparator());

		it = list.iterator();

		System.out.println("= 값의 크기가 큰 순서로 정렬 =");
		while(it.hasNext()) {
			Map.Entry entry = (Map.Entry)it.next();
			int value = ((Integer)entry.getValue()).intValue();
			System.out.println(entry.getKey() + " : " + printBar('#', value) + " " + value);
		}
	}

	static class ValueComparator implements Comparator {
		public int compare(Object o1, Object o2) {
			if(o1 instanceof Map.Entry && o2 instanceof Map.Entry) {
				Map.Entry e1 = (Map.Entry)o1;
				Map.Entry e2 = (Map.Entry)o2;

				int v1 = ((Integer)e1.getValue()).intValue();
				int v2 = ((Integer)e2.getValue()).intValue();

				return v2 - v1;
			}

			return -1;
		}
	}

	public static String printBar(char ch, int value) {
		char[] bar = new char[value];

		for(int i = 0; i < bar.length; i++) {
			bar[i] = ch;
		}

		return new String(bar);
	}
}
```
