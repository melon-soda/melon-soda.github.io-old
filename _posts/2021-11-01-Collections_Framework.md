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
