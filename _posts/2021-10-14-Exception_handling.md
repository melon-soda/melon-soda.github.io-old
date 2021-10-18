---
layout: post
title: Exception handling
---

Error
- compile-time error : 컴파일 시에 발생하는 에러
- runtime error : 실행 시에 발생하는 에러
- logical error : 실행은 되지만 의도와 다르게 동작하는 것

- error : 프로그램 코드에 의해서 수습될 수 없는 심각한 오류
- exception : 프로그램 코드에 의해서 수습될 수 있는 다소 미약한 오류

Exception class와 자손들(RuntimeException class와 자손들 제외) : 사용자 실수와 같은 외적 요인에 의해 발생
RuntimeException class와 자손들 : 프로그래머의 실수로 발생

```java
try {
	/* 예외가 발생할 수 있는 문장 */
} catch (Exception1 e1) {
	/* Exception1 발생 시 처리 할 문장 */
} catch (Exception2 e2) {
	/* Exception2 발생 시 처리 할 문장 */
}
```

catch 문이 여러개여도 일치하는 한개의 catch 블럭만이 실행된다.

```java
class ExceptionEx1 {
	public static void main(String[] args) {
		try {
			try {

			} catch (Exception e) {

			}
		} catch (Exception e) {
			try {

		/*	} catch (Exception e) { */		// 변수 e가 중복선언
			} catch (Exception e2) {

			}
		}
	}
}
```

```java
class ExceptionEx3 {
	public static void main(String[] args) {
		int number = 100;
		int result = 0;

		for(int i = 0; i < 10; i++) {
			try {
				result = number / (int)(Math.random() * 10);
				System.out.println(result);
			} catch (ArithmeticException e) {
				System.out.println("0");		// 0으로 나누는 경우 예외 처리, 0 출력
			}
		}
	}
}
```

try-catch 문의 흐름
- try 블럭 내에서 예외가 발생한 경우
	- 예외와 일치하는 catch 블럭이 있으면 실행하고 빠져나가 다음 문장을 실행
	- 일치하는 catch 블럭이 없으면 예외를 처리하지 못함
- try 블럭 내에서 예외가 발생하지 않은 경우
	- catch 블럭을 건너뛰도 다음 문장을 실행

```java
class ExceptionEx6 {
	public static void main(String[] args) {
		System.out.println(1);

		try {
			System.out.println(2);
			System.out.println(0/0);	// 예외 발생
			System.out.println(3);		// 실행되지 않음
		} catch (Exception e) {
			System.out.println(4);		// 예외 발생했으므로 실행 됨
		}

		System.out.println(5);
	}
}
```

```java
class ExceptionEx7 {
	public static void main(String[] args) {
		System.out.println(1);

		try {
			System.out.println(2);
			System.out.println(0/0);		// 예외 발생
			System.out.println(3);			// 실행되지 않음
		} catch (ArithmeticException ae) {	// 이 블럭이 실행되므로 아래의 catch 블럭 무시
			if(ae instanceof ArithmeticException)
				System.out.println("true");
			System.our.println("ArithmeticException");
		} catch (Exception e) {				// ArithmeticException 을 제외한 모든 예외 처리
			System.out.println("Exception");
		}

		System.out.println(4);
	}
}
```

발생한 예외에 관한 정보
- printStackTrace() : 예외 발생 당시의 Call Stack에 있었던 메소드의 정보와 예외 메시지 출력
- getMessage() : 발생한 예외클래스의 인스턴스에 저장된 메시지

```java
class ExceptionEx8 {
	public static void main(String[] args) {
		System.out.println(1);

		try {
			System.out.println(2);
			System.out.println(0/0);				// 예외 발생
			System.out.println(3);
		} catch (ArithmeticException ae) {
			ae.printStackTrace();
			System.out.println(ae.getMessage());	// / by zero
		}

		System.out.println(4);
	}
}
```

Multi Catch Block

JDK 1.7부터 여러 catch블럭을 '|'를 사용하여 합칠 수 있다.

```java
try {
	/* */
} catch (ExceptionA | ExceptionB e) {
	e.printStackTrace();
}

/* 예외 클래스가 조상과 자손 관계라면 조상 클래스만 써도 되므로 에러 발생 */
/*
try {

} catch (ParentException | ChildException e) {
	e.printStackTrace();
}
*/
```

Multi Catch Block 내에서는 어떤 예외가 발생한 것인지 알 수 없으므로 사용한 예외들의 공통 분모 조상 예외클래스에 선언된 멤버만 사용 가능하다.
참조변수 e는 상수이므로 값을 변경할 수 없다.

예외 발생시키기

throw를 이용하여 예외를 발생시킬 수 있다.

```java
class ExceptionEx9 {
	public static void main(String[] args) {
		try {
			Exception e = new Exception("고의로 발생시킨 예외");
			throw e;		// 예외 발생시킴
			// throw new Exception("고의로 발생시킨 예외");
		} catch (Exception e) {
			System.out.println("에러 메시지 : " + e.getMessage());
			e.printStackTrace();
		}

		System.out.println("프로그램 종료");
	}
}
```

Exception 생성자에 매개변수로 넣은 String은 getMessage()로 가져올 수 있다.

```java
class ExceptionEx10 {
	public static void main(String[] args) {
		// throw new Exception(); // 예외 처리가 되어있지 않으므로 컴파일 에러 발생
	}
}
```

```java
class ExceptionEx11 {
	public static void main(String[] args) {
		throw new RuntimeException(); // RuntimeException을 고의로 발생시킴
	}
}
```

RuntimeException과 자손들은 프로그래머의 실수에 의해 발생하기 때문에 예외처리를 해주지 않아도 컴파일이 된다. 나머지 Exception의 경우 항상 예외처리를 해주어야 한다.
컴파일러가 예외처리를 확인하지않는 RuntimeException 클래스들을 unchecked 예외라고 부르고, 예외처리를 확인하는 Exception 클래스들을 checked 예외라고 부른다.

메소드에도 예외 선언이 가능하다.

```java
void method() throws Exception1, Exception2, ... ExceptionN {
	/* */
}
```

선언된 예외들은 발생할 가능성이 있으니 예외 처리를 강제한다.

Java API 문서에서는 메소드와 함께 반드시 처리해야 하는 예외를 throws와 같이 기술해놓았다.
적혀있는 예외는 반드시 처리해야 하며, 처리하지 않아도 컴파일이 되는 RuntimeException의 경우 일반적으로 같이 적지 않는다.

throws는 예외를 처리하지 않고, 해당 메소드를 호출한 상위 메소드에 예외를 전달하여 예외 처리를 떠맡긴다. 처리되지 않는 예외는 Call Stack을 따라 올라가고, main에서도 처리되지 않으면 프로그램이 종료된다.

```java
class ExceptionEx13 {
	public static void main(String[] args) {
		method1();
	}

	static void method1() {
		try {
			throw new Exception();
		} catch (Exception e) {
			System.out.println("method1에서 예외 처리");
			e.printStackTrace();
		}
	}
}
```

```java
class ExceptionEx14 {
	public static void main(String[] args) {
		try {
			method1();
		} catch (Exception e) {
			System.out.println("main에서 예외 처리");
			e.printStackTrace();
		}
	}
	
	static void method1() throws Exception {
		throw new Exception();
	}
}
```

```java
import java.io.*;

class ExceptionEx15 {
	public static void main(String[] args) {
		File f = createFile(args[0]);
		System.out.println(f.getName() + " 파일이 성공적으로 생성되었습니다.");
	}

	static File createFile(String fileName) {
		try {
			if(fileName == null || fileName.equals(""))
				throw new Exception("파일 이름이 유효하지 않습니다.");
		} catch (Exception e) {
			fileName = "제목없음.txt";
		} finally {
			File f = new File(fileName);
			createNewFile(f);

			return f;
		}
	}

	static void createNewFile(File f) {
		try {
			f.createNewFile();
		} catch (Exception e) {

		}
	}
}
```

```java
import java.io.*;

class ExceptionEx16 {
	public static void main(String[] args) {
		try {
			File f = createFile(args[0]);
			System.out.println(f.getName() + " 파일이 성공적으로 생성되었습니다.");
		} catch (Exception e) {
			/* 값을 다시 받아야 하므로 호출한 메소드에서 예외 처리 */
			System.out.println(e.getMessage() + " 다시 입력해 주시기 바랍니다.");
		}
	}

	static File createFile(String fileName) throws Exception {
		if(fileName == null || fileName.equals(""))
			throw new Exception("파일 이름이 유효하지 않습니다.");

		File f = new File(fileName);
		f.createNewFile();
		
		return f;
	}
}
```

Finally Block
- 예외의 발생여부에 상관 없이 실행되어야할 코드
- try-catch문의 끝에 선택적으로 덧붙여 사용할 수 있음

```java
try {
	/* 예외가 발생 가능한 문장 */
} catch (Exception e) {
	/* 예외 처리 */
} finally {
	/* 항상 수행 할 문장 */
}
```

```java
class FinallyTest {
	public static void main(String[] args) {
		try {
			startInstall();
			copyFiles();
			// deleteTempFiles();
		} catch (Exception e) {
			e.printStackTrace();
			// deleteTempFiles();
		} finally {
			deleteTempFiles();		// 예외 발생 여부 없이 실행되어야 하므로 finally 블럭에 추가
		}
	}

	static void startInstall() {

	}

	static void coptFiles() {

	}

	static void deleteTempFiles() {

	}
}
```

try-catch에 return문이 있어도 finally블럭이 실행된 후에 메소드가 종료된다.

try-with-resources

```java
try {
	fis = new FileInputStream("score.dat");
	dis = new DataInputStream(fis);

	while(true) {
		score = dis.readInt();
		System.out.println(score);
		sum += score;
	}
} catch (IOException ie) {
	ie.printStackTrace();
} finally {
	try {
		if(dis != null)
			dis.close();			// close()문에서 예외 발생 가능
	} catch (IOException ie) {
		ie.printStackTrace();
	}
}
```

```java
try (FileInputStream fis = new FileInputStream("score.dat");
		DataInputStream dis = new DataInputStream(fis)) {
	while(true) {
		score = dis.readInt();
		System.out.println(score);
		sum += score;
	}
} catch (EOFException e) {
	System.out.println("score : " + sum);
} catch (IOException ie) {
	ie.printStackTrace();
}
```

try문의 괄호 안에서 객체를 생성하면 따로 close()를 호출하지 않아도 try문을 벗어나는 순간 자동으로 close()가 호출된다.

```java
class TryWithResourceEx {
	public static void main(String[] args) {
		try (CloseableResource cr = new CloseableResource()) {
			cr.exceptionWork(false);
		} catch (WorkException e) {
			e.printStackTrace();
		} catch (CloseException e) {
			e.printStackTrace();
		}

		System.out.println();

		try (CloseableResource cr = new CloseableResource()) {
			cr.exceptionWork(true);
		} catch (WorkException e) {
			e.printStackTrace();
		} catch (CloseException e) {
			e.printStackTrace();
		}
	}
}

class CloseableResource implements AutoCloseable {
	public void exceptionWork(boolean exception) throws WorkException {
		System.out.print("exceptionWork(" + exception + ")가 호출됨");

		if(exception)
			throw new WorkException("WorkException 발생!");
	}

	public void close() throws CloseException {
		System.out.println("close()가 호출됨");
		throw new CloseException("CloseException 발생!");
	}
}

class WorkException extends Exception {
	WorkException(String msg) {
		super(msg);
	}
}

class CloseException extends Exception {
	CloseException(String msg) {
		super(msg);
	}
}
```

```java
class NewExceptionTest {
	public static void main(String[] args) {
		try {
			startInstall();
			copyFiles();
		} catch (SpaceException e) {
			System.out.println("Error message : " + e.getMessage());
			e.printStackTrace();
			System.out.println("공간을 확보한 후에 다시 설치하시기 바랍니다.");
		} catch  (MemoryException me) {
			System.out.println("에러 메시지 : " + me.getMessage());
			me.printStackTrace();
			System.gc();
			System.out.println("다시 설치를 시도하세요.");
		} finally {
			deleteTempFiles();
		}
	}

	static void startInstall() throws SpaceException, MemoryException {
		if(!enoughSpace())
			throw new SpaceException("설치할 공간이 부족합니다.");
		if(!enoughMemory())
			throw new MemoryException("메모리가 부족합니다.");
	}

	static void copyFiles(); {

	}

	static void deleteTempFiles() {

	}

	static boolean enoughSpace() {
		return false;
	}

	static boolean enoughMemory() {
		return true;
	}
}

class SpaceException extends Exception {
	SpaceException(String msg) {
		super(msg);
	}
}

class MemoryException extends Exception {
	MemoryException(String msg) {
		super(msg);
	}
}
```

exception re-throwing(예외 되던지기)

예외가 발생할 가능성이 있는 메소드에서 try-catch문을 사용하여 예외를 처리한 후 throw를 사용하여 다시 예외를 발생시킨다. 다시 발생된 예외는 호출한 메소드로 넘어가고, 해당 메소드의 try-catch문에서 처리된다.

```java
class ExceptionEx17 {
	public static void main(Stirng[] args) {
		try {
			method1();
		} catch (Exception e) {
			System.out.println("main에서 exception 처리");
		}
	}

	static void method1() throws Exception {
		try {
			throw new Exception();
		} catch (Exception e) {
			System.out.println("method1에서 exception 처리");
			throw e;
		}
	}
}
```

chained exception(연결된 예외)

- 여러 가지 예외를 하나의 큰 분류의 예외로 묶어서 다루기 위해 사용
- 원인 예외를 등록하고, 다시 예외를 발생시킨다.

Throwable initCause(Throwable cause) : 지정한 예외를 원인 예외로 등록
Throwable getCause() : 원인 예외를 반환

예외들의 공통 조상 예외를 try-catch문에서 사용하게 되면, 복수의 예외가 있을 경우 어떤 예외가 발생했는지 알 수 없으며, 해당 예외들의 상속관계도 변경해야한다. 원인 예외를 포함하고 던지면 상속관계가 아니어도 던질 수 있다.

```java
class ChainedExceptionEx {
	public static void main(String[] args) {
		try {
			install();
		} catch (InstallException e) {
			e.printStackTrace();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

	static void install() throws InstallException {
		try {
			startInstall();
			copyFiles();
		} catch (SpaceException se) {
			InstallException ie = new InstallException("설치 중 예외 발생");
			ie.initCause(se);
			throw ie;
		} catch (MemoryException me) {
			InstallException ie = new InstallException("설치 중 예외 발생");
			ie.initCause(me);
			throw ie;
		} finally {
			deleteTempFiles();
		}
	}

	static void startInstall() throws SpaceException, MemoryException {
		if(!enoughSpace()) {
			throw new SpaceException("설치할 공간이 부족합니다.");
		}

		if(!enoughMemory()) {
			throw new MemoryException("메모리가 부족합니다.");
//			throw new RuntimeException(new MemoryException("메모리가 부족합니다."));
		}
	}

	static void copyFiles() {

	}

	static void deleteTempFiles() {

	}

	static boolean enoughSpace() {
		return false;
	}

	static boolean enoughMemory() {
		return true;
	}
}

class InstallException extends Exception {
	InstallException(String msg) {
		supeR(msg);
	}
}

class SpaceException extends Exception {
	SpaceException(String msg) {
		super(msg);
	}
}

class MemoryException extends Exception {
	MemoryException(String msg) {
		super(msg);
	}
}
```
