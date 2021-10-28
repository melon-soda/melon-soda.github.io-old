---
layout: post
title: Date, Time & Formatting
---

Calandar : 추상 클래스 -> 직접 객체를 생성할 수 없다.

getInstance()를 사용하면 인스턴스를 Buddhist Calandar(태국)과 Gregorian Calandar(그 외)로 생성할 수 있다.

Date와 Calandar간의 변환

```java
/* Calandar -> Date */

Calandar cal = Calandar.getInstance();
Date d = new Date(cal.getTimteInMillis());

/* Date -> Calandar */

Date d = new Date();
Calandar cal = Calandar.getInstance();
cal.setTime(d);
```

```java
import java.util.*;

class CalandarEx1 {
	public static void main(String[] args) {
		Calandar today = Calendar.getInstance();

		System.out.println("이 해의 년도 : " + today.get(Calendar.YEAR));
		System.out.println("월(0~11) : " + today.get(Calendar.MONTH));
		System.out.println("이 해의 n번째 주 : " + today.get(Calendar.WEEK_OF_YEAR));
		System.out.println("이 달의 n번째 주 : " + today.get(Calendar.WEEK_OF_MONTH));
		System.out.println("이 달의 n번째 일 : " + today.get(Calendar.DATE));
		System.out.println("이 달의 n번째 일 : " + today.get(Calendar.DAY_OF_MONTH));
		System.out.println("이 해의 n번째 일 : " + today.get(Calendar.DAY_OF_YEAR));
		System.out.println("요일(1~7, 1:일요일) : " + today.get(Calendar.DAY_OF_WEEK));
		System.out.println("이 달의 n번째 요일 : " + today.get(Calendar.DAY_OF_WEEK_IN_MONTH));
		System.out.println("오전/오후 : " + today.get(Calendar.AM_PM));
		System.out.println("시간(0~11) : " + today.get(Calendar.HOUR));
		System.out.println("시간(0~23) : " + today.get(Calendar.HOUR_OF_DAY));
		System.out.println("분(0~59) : " + today.get(Calendar.MINUTE));
		System.out.println("초(0~59) : " + today.get(Calendar.SECOND));
		System.out.println("밀리초(0~999) : " + today.get(Calendar.MILLISECOND));
		System.out.println("TimeZone(-12~+12) : " + (today.get(Calendar.ZONE_OFFSET)/(60*60*1000)));
		System.out.println("이 달의 마지막 날 : " + today.getActualMaximum(Calendar.DATE));
	}
}
```

get(Calander.Month)로 얻어오는 값만 0(=1월)부터 시작하기 때문에 주의해야 한다.

```java
import java.util.*;

class CalendarEx2 {
	public static void main(String[] args) {
		/* Calendar.DAY_OF_WEEK은 1부터 시작하기 때문에 0은 비워둔다. */
		final String[] DAY_OF_WEEK = {"", "일", "월", "화", "수", "목", "금", "토"};

		Calendar date1 = Calendar.getInstance();
		Calendar date2 = Calendar.getInstance();

		/* month는 0부터 시작하기 때문에 n-1로 설정해야 n월이 된다. */
		date1.set(2020, 9, 25);	// 2020/10/25
		//date1.set(2021, Calendar.October, 25);

		System.out.println("date1 : " + toString(date1) + DAY_OF_WEEK[date1.get(Calendar.DAY_OF_WEEK)] + "요일");
		System.out.println("date2 : " + toString(date2) + DAY_OF_WEEK[date2.get(Calendar.DAY_OF_WEEK)] + "요일");

		long difference = (date2.getTimeInMillis() - date1.getTimeInMillis())/1000;

		System.out.println(difference + "초 경과");
		System.out.println(difference/(24*60*60) + "일 경과");
	}

	public static String toString(Calendar date) {
		return date.get(Calendar.YEAR) + "년 " + (date.get(Calendar.MONTH) + 1) + "월 " + date.get(Calendar.DATE) + "일 ";
	}
}
```

set()을 사용하면 날짜와 시간을 원하는 값으로 설정 가능하다.

```java
void set(int field, int value);
void set(int year, int month, int date);
void set(int year, int month, int date, int hourOfDay, int minute);
void set(int year, int month, int date, int hourOfDay, int minute, int second);
```

```java
import java.util.*;

class CalendarEx3 {
	public static void main(String[] args) {
		final int[] TIME_UNIT = {3600, 60, 1};
		final String[] TIME_UNIT_NAME = {"시간", "분", "초"};

		Calendar time1 = Calendar.getInstance();
		Calendar time2 = Calendar.getInstance();

		time1.set(Calendar.HOUR_OF_DAY, 10);
		time1.set(Calendar.MINUTE, 20);
		time1.set(Calendar.SECOND, 30);

		time2.set(Calendar.HOUR_OF_DAY, 20);
		time2.set(Calendar.MINUTE, 30);
		time2.set(Calendar.SECOND, 10);

		System.out.println("time1 : " + toString(time1));
		System.out.println("time2 : " + toString(time2));


		long difference = Math.abs(time2.getTimeInMillis() - time1.getTimeInMillis())/1000;
		System.out.println("difference : " + difference + "초");

		Strimg tmp = "";

		for(int i = 0; i < TIME_UNIT.length; i++) {
			tmp += difference/TIME_UNIT[i] + TIME_UNIT_NAME[i];
			difference %= TIME_UNIT[i];
		}

		System.out.println("difference : " + tmp);
	}

	public static String toString(Calendar time) {
		return time.get(Calendar.HOUR_OF_DAY) + "시 " + time.get(Calendar.MINUTE) + "분 " + time.get(Calendar.SECOND) + "초 ";
	}
}
```

```java
import jaav.util.*;

class CalendarEx4 {
	public static void main(String[] args) {
		Calendar date = Calendar.getInstance();
		date.set(2015, 7, 31);

		System.out.println(toString(date));
		System.out.println(" = 1일 후 = ");
		date.add(Calendar.DATE, 1);
		System.out.println(toString(date));

		System.out.println(" = 6달 전 = ");
		date.add(Calendar.MONTH, -6);
		System.out.println(toString(date));

		System.out.println(" = 31일 후(roll) = ");
		date.roll(Calendar.DATE, 31);
		System.out.println(toString(date));

		System.out.println(" = 31일 후(add) = ");
		date.add(Calendar.DATE, 31);
		System.out.println(toString(date));
	}

	public static String toString(Calendar date) {
		return date.get(Calendar.YEAR) + "년 " + (date.get(Calendar.MONTH) + 1) + "월 " + date.get(Calendar.DATE) + "일";
	}
}
```

add()는 다른 field의 값도 변경시키지만, roll()은 다른 field의 값은 변경시키지 않고 해당 field만 변경시킨다. 달의 일 수는 해당 달의 일수를 기준으로 계산한다.
Calendar.DATE가 end of month(마지막 날) 일 때는 roll() 역시 Calendar.DATE를 변경시킬 수 있다.

```java
class CalendarEx5 {
	public static void main(String[] args) {
		Calendar date = Calendar.getInstance();

		date.set(2015, 0, 31);			// 2015년 1월 31일
		System.out.println(toString(date));
		date.roll(Calendar.MONTH, 1);	// 2015년 2월 28일
		System.out.println(toString(date));
	}

	public static void toString(Calendar date) {
		return date.get(Calendar.YEAR) + "년 " + (date.get(Calendar.MONTH) + 1) + "월 " + date.get(Calendar.DATE) + "일";
	}
}
```

```java
Calendar date = Calendar.getInstance();
date.set(2021, 2, 1);
date.roll(Calendar.DATE, -32); // 2021년 2월 25일 : -28일 + -4일

date.set(2021, 2, 1);
date.roll(Calendar.DATE, -32); // 2021년 2월 27일 : -29일 + -3일
```

```java
import java.util.*;

class CalendarEx6 {
	public static void main(String[] args) {
		if(args.length != 2) {
			System.out.println("Usage : java CalendarEx6 2015 9");
			return;
		}

		int year = Integer.parseInt(args[0]);
		int month = Integer.parseInt(args[1]);
		int START_DAY_OF_WEEK = 0;
		int END_DAY = 0;

		Calendar sDay = Calendar.getInstance();
		Calendar eDay = Calendar.getInstance();

		sDay.set(year, month - 1, 1);
		eDay.set(year, month, 1);

		eDay.add(Calendar.DATE, -1);

		START_DAY_OF_WEEK = sDay.get(Calendar.DAY_OF_WEEK);

		END_DAY = eDay.get(Calendar.DATE);

		System.out.println("	  " + args[0] + "년 " + args[1] + "월 ");
		System.out.println(" SU MO TU WE TH FR SA");

		for(int i = 1; i < START_DAY_OF_WEEK; i++) {
			System.out.print("   ");
		}

		for(int i = 1, n = START_DAY_OF_WEEK; i <= END_DAY; i++, n++) {
			System.out.print((i < 10)? "  " + i : " " + i);
			if(n % 7 == 0)
				System.out.println();
		}
	}
}
```

```java
import java.util.*;

class CalendarEx7 {
	public static void main(String[] args) {
		if(args.length != 2) {
			System.out.println("Usage : java CalendarEx7 2015 11");
			return;
		}

		int year = Integer.parseInt(args[0]);
		int month = Integer.pareseInt(args[1]);

		Calendar sDay = Calendar.getInstance();
		Calendar eDay = Calendar.getInstance();

		sDay.set(year, month - 1, 1);
		eDay.set(year, month - 1, sDay.getActualMaximum(Calendar.DATE));

		sDay.add(Calendar.DATE, -sDay.get(Calendar.DAY_OF_WEEK) + 1);
		eDay.add(Calendar.DATE, 7 - eDay.get(Calendar.DAY_OF_WEEK));

		System.out.println("      " + year + "년 " + month + "월");
		System.out.println(" SU MO TU WE TH FR SA");

		for(int n = 1; sDay.before(eDay) || sDay.equals(eDay); sDay.add(Calendar.DATE, 1)) {
			int day = sDay.get(Calendar.DATE);
			System.out.print((day < 10)? "  " + day : " " + day);
			if(n++ % 7 == 0)
				System.out.println();
		}
	}
}
```

```java
class CalendarEx8 {
	public static void main(String[] args) {
		String date1 = "201508";
		Stirng date2 = "201405";

		int month1 = Integer.parseInt(date1.subString(0,4)) * 12
					+ Integer.parseInt(date2.subString(4));
		int month2 = Integer.parseInt(date2.subString(0,4)) * 12
					+ Integer.parseInt(date2.subString(4));

		System.out.println(date1 + "과 " + date2 + "의 차이는 " + Math.abs(month1 - month2) + " 개월 입니다.");
	}
}
```

```java
class CalendarEx9 {
	public static void main(String[] args) {
		System.out.println("2014. 5.31 : " + getDayOfWeek(2014, 5, 31));
		System.out.println("2012. 6. 1 : " + getDayOfWeek(2012, 6, 1));
		System.out.println("2014. 5. 1 - 2014. 4.28 : " + dayDiff(2014, 5, 1, 2014, 4, 28));
		System.out.println("2015. 6.29 : " + convertDateToDay(2015, 6, 29));
		System.out.println("735778 : " + convertDayToDate(735578));
	}

	public static int[] endOfMonth = {31, 28, 31, 30, 31, 30,
									  31, 31, 30, 31, 30, 31};

	public static boolean isLeapYear(int year) {
		return ((year % 4 == 0) && (year % 100 != 0) || (year % 400 == 0));
	}

	public static int dayDiff(int y1, int m1, int d1, int y2, int m2, int d2) {
		return convertDateToDay(y1, m1, d1) - convertDateToDay(y2, m2, d2);
	}

	public static int getDayOfWeek(int year, int month, int day) {
		return convertDateToDay(year, month, day) % 7 + 1;
	}

	public static String convertDayToDate(int day) {
		int year = 1;
		int month = 0;

		while(true) {
			int aYear = isLeapYear(year) ? 366 : 365;

			if(day > aYear) {
				day -= aYear;
				year++;
			} else {
				break;
			}
		}

		while(true) {
			int endDay = endOfMonth[month];

			if(isLeapYear(year) && month == 1)		// 2월
				endDay++;

			if(day > endDay) {
				day -= endDay;
				month++;
			} else {
				break;
			}
		}

		return year + "-" + (month + 1) + "-" + day;
	}

	public static int convertDateToDay(int year, int month, int day) {
		int numOfLeapYear = 0;

		for(int i = 1; i < year; i++) {
			if(isLeapYear(i))
				numOfLeapYear++;
		}

		int toLastYearDaySum = (year - 1) * 365 + numOfLeapYear;

		int thisYearDaySum = 0;

		for(int i = 0; i < month - 1; i++)
			thisYearDaySum += endOfMonth[i];

		if(month > 2 && isLeapYear(year))
			thisYearDaySum++;

		thisYearDaySum += day;

		return toLastYearDaySum + thisYearDaySum;
	}
}
```

형식화 클래스

DecimalFormat : 숫자의 형식화

0 : 10진수, 값이 없으면 0
\# : 10진수
. : 소수점
\- : 음수부호
, : 단위 구분자
E : 지수기호
; : 패턴 구분자
% : 퍼센트
\\u2030 : 퍼밀
\\u00A4 : 통화
' : escape

```java
import java.text.*;

class DecimalFormatEx1 {
	public static void main(String[] args) throws Exception {
		double number = 1234567.89;

		String[] pattern = {
			"0",					// 1234568			// 정수 부분, 남는자리 0
			"#",					// 1234568			// 정수 부분
			"0.0",					// 1234567.9		// 소수점 첫째 자리까지, 남는자리 0
			"#.#",					// 1234567.9		// 소수점 첫째 자리까지
			"0000000000.0000",		// 0001234567.8900	// 소수점 넷째 자리까지, 남는자리 0
			"##########.####",		// 1234567.89		// 소수점 넷째 자리까지
			"#.#-",					// 1234567.9-		// 소수점 첫째 자리까지, 음수부호
			"-#.#",					// -1234567.9		// 음수부호, 소수점 첫째 자리까지
			"#,###.##",				// 1,234,567.89		// 3자리씩 끊고 소수점 둘째 자리까지
			"#,####.##",			// 123,4567.89		// 4자리씩 끊고 소수점 둘째 자리까지
			"#E0",					// .1E7				// #은 E앞에 사용시 소수점을 강제하는것으로 보임
			"0E0",					// 1E6				// 0은 정수로 나오는 것으로 보임
			"##E0",					// 1.2E6
			"00E0",					// 12E5
			"####E0",				// 123.5E4
			"0000E0",				// 1235E3
			"#.#E0",				// 1.2E6
			"0.0E0",				// 1.2E6
			"0.000000000E0",		// 1.234567890E6
			"00.00000000E0",		// 12.34567890E5
			"000.0000000E0",		// 123.4567890E4
			"#.#########E0",		// 1.23456789E6
			"##.########E0",		// 1.23456789E6
			"###.#######E0",		// 1.23456789E6
			"#,###.##+;#,###.##-",	// 1,234,567.89+
			"#.#%",					// 123456789%
			"#.#\\u2030",			// 1234567890\u2030
			"\\u00A4 #,###",		// \ 1,234,568
			"'#'#,###",				// \#1,234,568
			"''#,###"				// \'1,234,568
		};

		for(int i = 0; i < pattern.length; i++) {
			DecimalFormat df = newDecimalFormat(pattern[i]);
			System.out.println("%19s : %s\\n", pattern[i], df.format(number));
		}
	}
}
```

```java
import java.text.*;

class DecimalFormatEx2 {
	public static void main(Stirng[] args) {
		DecimalFormat df = new DecimalFormat("#,###.##");
		DecimalFormat df2 = new DecimalFormat("#.###E0");

		try {
			Number num = df.parse("1,234,567.89");
			System.out.println("1,234,567.89" + " -> ");

			double d = num.doubleValue();
			System.out.println(d + " -> ");			// 1234567.89

			System.out.println(df2.format(num));	// 1.235E6
		} catch(Exception e) {

		}
	}
}
```

Integer.parseInt()는 ','가 포함된 문자열을 숫자로 반환할 수 없지만 parse()는 가능하다.

SimpleDateFormat

날짜 데이터를 원하는 대로 출력할 수 있게 도와주는 클래스

G : 연대(BC, AD)
y : 년도
M : 월
L : 월
w : 년의 w번째 주
W : 월의 W번째 주
D : 년의 D번째 일
d : 월의 d번째 일
F : 월의 F번째 요일
E : 요일
a : 오전/오후 (AM/PM)
H : 시간(0~23)
k : 시간(1~24)
K : 시간(0~11)
h : 시간(1~12)
m : 분(0~59)
s : 초(0~59)
S : 밀리초(0~999)
z : Time zone(General Time Zone)
Z : Time zone(RFC 822 Time Zone)
\' : escape 문자

```java
import java.util.*;
import java.text.*;

class DateFormatEx1 {
	public static void main(String[] args) {
		Date today = new Date();

		SimpleDateFormat sdf1, sdf2, sdf3, sdf4;
		SimpleDateFormat sdf5, sdf6, sdf7, sdf8, sdf9;

		sdf1 = new SimpleDateFormat("yyyy-MM-dd");
		sdf2 = new SimpleDateFormat("''yy년 MMM dd일 E요일");
		sdf3 = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss.SSS");
		sdf4 = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss a");

		sdf5 = new SimpleDateFormat("오늘은 올 해의 D번째 날입니다.");
		sdf6 = new SimpleDateFormat("오늘은 이 달의 d번째 날입니다.");
		sdf7 = new SimpleDateFormat("오늘은 올 해의 w번째 주입니다.");
		sdf8 = new SimpleDateFormat("오늘은 이 달의 W번째 주입니다.");
		sdf9 = new SimpleDateFormat("오늘의 이 달의 F번째 E요일입니다.");

		System.out.println(sdf1.format(today));
		System.out.println(sdf2.format(today));
		System.out.println(sdf3.format(today));
		System.out.println(sdf4.format(today));
		System.out.println();
		System.out.println(sdf5.format(today));
		System.out.println(sdf6.format(today));
		System.out.println(sdf7.format(today));
		System.out.println(sdf8.format(today));
		System.out.println(sdf9.format(today));
	}
}
```

```java
import java.util.*;
import java.text.*;

class DateFormatEx2 {
	public static void main(String[] args) {
		Calendar cal = Calendar.getInstance();
		cal.set(2005, 9, 3);		// 2005-10-03

		Date day = cal.getTime();	// Calender -> Date

		SimpleDateFormat sdf1, sdf2, sdf3, sdf4;

		sdf1 = new SimpleDateFormat("yyyy-MM-dd");
		sdf2 = new SimpleDateFormat("yy-MM-dd E요일");
		sdf3 = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss.SSS");
		sdf4 = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss a");

		System.out.println(sdf1.format(day));
		System.out.println(sdf2.format(day));
		System.out.pritnln(sdf3.format(day));
		System.out.println(sdf4.format(day));		
	}
}
```

getTime() : Calendar -> Date
setTime() : Date -> Calendar

```java
import java.util.*;
import java.text.*;

class DateFormatEx3 {
	public static void main(String[] args) {
		DateFormat df = new SimpleDateFormat("yyyy년 MM월 dd일");
		DateFormat df2 = new SimpleDateFormat("yyyy/MM/dd");

		try {
			Date d = df.parse("2015년 11월 23일");
			System.out.println(df2.format(d));
		} catch(Exception e) {

		}
	}
}
```

```java
import java.util.*;
import java.text.*;

class DateFormatEx4 {
	public static void main(String[] args) {
		String pattern = "yyyy/MM/dd";
		DateFormat df = new SimpleDateFormat(pattern);
		Scanner s = new Scanner(System.in);

		Date inDate = null;

		System.out.println("날짜를 " + pattern + " 의 형태로 입력해주세요. (입력예 : 2015/12/31)");

		while(s.hasNextLine()) {
			try {
				inDate = df.parse(s.nextLine());
				break;
			} catch(Exception e) {
				System.out.println("날짜를 " + pattern + " 의 형태로 입력해주세요. (입력 예 : 2015/12/31)");
			}
		}

		Calendar cal = Calendar.getInstance();
		cal.setTime(inDate);
		Calendar today = Calendar.getInsatnce();
		long day = (cal.getTimeInMillis() - today.getTimeInMillis())/(60*60*1000);
		System.out.println("입력하신 날짜는 현재와 " + day + "시간 차이가 있습니다.");
	}
}
```

Choice Format

특정 범위에 속하는 값을 문자열로 변환

연속적으로 변하는 값에 대하여 if나 switch문에 비하여 적절하다.

```java
import java.text.*;

class ChoiceFormatEx1 {
	public static void main(String[] args) {
		double[] limits = {60, 70, 80 ,90};
		String[] grades = {"D", "C", "B", "A"};

		int[] scores = {100, 95, 88, 70, 52, 60, 70};

		ChoiceFormat form = new ChoiceFormat(limits, grades);

		for(int i = 0; i < scores.length; i++) {
			System.out.println(scores[i] + " : " + form.format(scores[i]));
		}
	}
}
```

경계값은 항상 오름차순으로 정렬되어 있어야 하고, 문자열은 경계값과 갯수가 일치해야 한다.

```java
import java.text.*;

class ChoiceFormatEx2 {
	String pattern = "60#D|70#C|80<B|90#A";
	int[] scores = {91, 90, 80, 88, 70, 52, 60};

	ChoiceFormat form = new ChoiceFormat(pattern);

	for(int i = 0; i < scores.length; i++) {
		System.out.println(scores[i] + " : " + form.format(scores[i]));
	}
}
```

\#는 경계값을 범위에 포함하고, \<는 경계값을 범위에 포함하지 않는다.

MessageFormat

데이터를 정해진 양식에 맞춰 출력

```java
import java.text.*;

class MessageFormatEx1 {
	public static void main(String[] args) {
		String msg = "Name : {0} \nTel : {1} \nAge : {2} \nBirthday : {3}";

		Object[] arguments = {
			"Name", "01-2345-6789", "27", "10-28"
		};

		String result = MessageFormat.format(msg, arguments);
		System.out.println(result);
	}
}
```

```java
import java.text.*;

class MessageFormatEx2 {
	public static void main(String[] args) {
		String tableName = "CUST_INFO";
		String msg = "INSERT INTO " + tableName + " VALUES (''{0}'', ''{1}'', ''{2}'', ''{3}'');";

		Object[][] arguments = {
			{"First", "01-2345-6789", "27", "10-28"},
			{"Second", "02-3456-7890", "33", "12-08"};
		};

		for(int i = 0; i < arguments.length; i++) {
			String result = MessageFormat.format(msg, arguments[i]);
			System.out.println(result);
		}
	}
}
```

```java
import java.text.*;

class MessageFormatEx3 {
	public static void main(String[] args) throws Exception {
		String[] data = {
			"INSERT INTO CUST_INFO VALUES('First', '01-2345-6789', '27', '10-28');",
			"INSERT INTO CUST_INFO VALUES('Second', '02-3456-7890', '33', '12-08');"
		};

		String pattern = "INSERT INTO CUST_INFO VALUES({0}, {1}, {2}, {3});";
		MessageFormat mf = new MessageFormat(pattern);

		for(int i = 0; i < data.length; i++) {
			Object[] objs = mf.parse(data[i]);
			for(int j = 0; j < objs.length; j++) {
				System.out.println(objs[j] + ",");
			}
			System.out.println();
		}
	}
}
```

```java
import java.util.*;
import java.text.*;
import java.io.*;

class MessageFormatEx4 {
	public static void main(String[] args) throws Exception {
		String tableName = "CUST_INFO";
		String fileName = "data4.txt";
		String msg = "INSERT INTO " + tableName + " VALUES({0}, {1}, {2}, {3})";

		Scanner s = new Scanner(new File(fileName));

		String pattern = "{0}, {1}, {2}, {3}";
		MessageFormat mf = new MessageFormat(pattern);

		while(s.hasNextLine()) {
			String line = s.nextLine();
			Object[] objs = mf.parse(line);
			System.out.println(MessageFormat.format(msg, objs));

			s.close();
		}
	}
}
```

java.time package

java.time.chrono : 비표준 달력 시스템을 위한 class
java.time.format : 날짜와 시간 parsing 및 formatting을 위한 class
java.time.temporal : 날짜와 시간의 field 및 unit을 위한 class
java.time.zone : time-zone과 관련된 class

모든 class는 immutable하므로 기존 객체를 변경하지 않고 변경한 새로운 객체를 반환한다.
multi-thread 환경에서 안전하다(thread-safe).

LocalDate : 날짜
LocalTime : 시간
LocalDateTime = LocalDate + LocalTime
ZonedDateTime = LocalDateTime + TimeZone 관련 기능
Instant : 날짜와 시간을 나노초 단위로 표현

Period : 날짜 간의 차이
Duration : 시간의 차이

java.time package에 속한 객체 생성

now() : 현재 날짜와 시간을 저장하는 객체 생성
of() : 해당 필드의 값을 순서대로 지정하면 값에 맞는 객체를 생성

Temporal, TemporalAccessor, TemporalAdjuster interface
- LocalDate, LocalTime, LocalDateTime, ZonedDateTime, Instant 등에서 구현
TemporalAmount interface
- Period, Duration 에서 구현

TemporalUnit : 날짜의 시간과 unit을 정의한 interface -> Enum ChronoUnit에서 구현
TemporalField : 날짜와 시간의 field를 정의한 interface -> Enum ChronoField에서 구현

LocalDate/LocalTime

```java
LocalDate today = LocalDate.now();	// 현재 날짜
LocalTime now = LocalTime.now();	// 현재 시각
```

now(), of() 모두 static method이다.

static LocalDate of(int year, Month month, int dayOfMonth)
static LocalDate of(int year, int month, int dayOfMonth)

static LocalTime of(int hour, int min)
static LocalTime of(int hour, int min, int sec)
static LocalTime of(int hour, int min, int sec, int nanoOfSecond)

```java
LocalDate someDate = LocalDate.ofYearDay(1999, 365);	// 1999년의 365번째 날(12/31)
LocalTime someTime = LocalTime.ofSecondDay(86399);		// 86399초 (23시 59분 59초)
```

LocalDate - getMethod

int getYear() : 년도(2021)
int getMonthValue() : 월(10)
Month getMonth() : 월(October) -> getMonth().getValue() = 10
int getDayOfMonth() : 일(28)
int getDayOfYear() : 해당 해의 n번째 일
DayOfWeek getDayOfWeek() : 요일(THURSDAY) -> getDayOfWeek.getValue() = 4
int lengthOfMonth() : 해당 달의 총 일수(31)
int lengthOfYear() : 해당 해의 총 일수(356), 윤년이면 366
boolean isLeapYear() : 윤년이면 true, 아닐 경우 false

LocalTime - getMethod

int getHour() : 시
int getMinute() : 분
int getSecond() : 초
int getNano() : 나노초

int get(TemporalField field),
long getLong(TemporalField field) : 필드를 지정할 수 있다. 필드에 따라 getLong()을 사용

ERA : 시대
YEAR\_OF\_ERA, YEAR : 년
MONTH\_OF\_YEAR : 월
DAY\_OF\_WEEK : 요일
DAY\_OF\_MONTH : 일
AMPM\_OF\_DAY : 오전/오후
HOUR\_OF\_DAY : 시간(0~23)
CLOCK\_HOUR\_OF\_DAY : 시간(1~24)
HOUR\_OF\_AMPM : 시간(0~11)
CLOCK\_HOUR\_OF\_AMPM : 시간(1~12)
MINUTE\_OF\_HOUR : 분
SECOND\_OF\_MINUTE : 초
MILLI\_OF\_SECOND : 10^-3초
\* MICRO\_OF\_SECOND : 10^-6초
\* NANO\_OF\_SECOND : 10^-9초
DAY\_OF\_YEAR : 해당 해의 n번째 날
\* EPOCH\_DAY : EPOCH(1970.01.01)로부터 n번째 날
MINUTE\_OF\_DAY : 당일의 n번째 분
SECOND\_OF\_DAY : 당일의 n번째 초
MILLI\_OF\_DAY : 당일의 n번째 10^-3초
\* MICRO\_OF\_DAY : 당일의 n번째 10^-6초
\* NANO\_OF\_DAY : 당일의 n번째 10^-9초
ALIGNED\_WEEK\_OF\_MONTH : 해당 달의 n번째 주(1~7일 : 1주, 8~14일 : 2주, ...)
ALIGNED\_WEEK\_OF\_YEAR : 해당 해의 n번째 주(1~7일 : 1주, 8~14일 : 2주, ...)
ALIGNED\_DAY\_OF\_WEEK\_IN\_MONTH : 해당 달의 n요일(1일 : 월요일)
ALIGNED\_DAY\_OF\_WEEK\_IN\_YEAR : 해당 해의 n요일(1월 1일 : 월요일)
INSTANT\_SECONDS : 년월일을 초단위호 환산(1970-01-01 00:00:00 UTC가 0초)
OFFSET\_SECONDS : UTC와의 시차
PROLEPTIC\_MONTH : 년월을 월단위로 환산

Calendar와 다르게 month의 범위는 1~12이고, 요일의 경우 월요일이 1이고 일요일이 7이다.

.range() 메소드를 사용하여 가질 수 있는 값의 범위를 알 수 있다.

field 값 변경하기

LocalDate withYear(int year)
LocalDate withMonth(int month)
LocalDate withDayOfMonth(int dayOfMonth)
LocalDate withDayOfYear(int dayOfYear)

LocalTime withHour(int hour)
LocalTime withMinute(int minute)
LocalTime withSecond(int second)
LocalTime withNano(int nanoOfSecond)


with()를 사용하면 직접 field를 지정할 수 있다.

LocalDate with(TemporalField field, long newValue)

LocalTime plus(TemporalAmount amountToAdd)
LocalTime minus(TemporalAmount amountToSubtract)
LocalTime plus(long amountToAdd, TemporalUnit unit)
LocalTime minus(long amountToSubtract, TemporalUnit unit)

LocalDate plus(TempoalAmount amountToAdd)
LocalDate minus(TemporalAmount amountToSubtract)
LocalDate plus(long amountToAdd, TemporalUnit unit)
LocalDate minus(long amountToSubtract, TempotalUnit unit)

LocalDate plusYears(long yearsToAdd)
LocalDate minusYears(long yearsToSubtract)
LocalDate plusMonths(long monthsToAdd)
LocalDate minusMonths(long monthsToSubtract)
LocalDate plusDays(long daysToAdd)
LocalDate minusDays(long daysToSubtract)
LocalDate plusWeeks(long weeksToAdd)
LocalDate minusWeeks(long weeksToSubtract)

LocalTime plusHours(long hoursToAdd)
LocalTime minusHours(long hoursToSubtract)
LocalTime plusMinutes(long minutesToAdd)
LocalTime minusMinutes(long minutesToSubtract)
LocalTime plusSeconds(long secondsToAdd)
LocalTime minusSeconds(long secondsToSubtract)
LocalTime plusNanos(long nanosToAdd)
LocalTime minusNanos(long nanosToSubtract)

LocalTime truncatedTo(TemporalUnit unit) : 지정된 것보다 작은 단위의 field를 모두 0으로 만듦
-> LocalDate는 0이 될 수 있는 field가 없으므로 truncatedTo()가 존재하지 않는다.

날짜와 시간의 비교

boolean isAfter(ChronoLocalDate other)
boolean isBefore(ChronoLocalDate other)
boolean isEqual(ChronoLocalDate other)

compareTo()로도 비교 가능하다.

int result = date1.compareTo(date2);

equals()로도 비교 가능하나, 모든 field가 같아야 true가 나오기 때문에 chronology(연표)가 다른 날짜를 비교하면 false가 나온다. 
isEqual()은 오직 날짜만 비교하기 때문에 chronology가 달라도 날짜가 같으면 true가 나온다.

```java
import java.time.*;
import java.time.temporal.*;

class NewTimeEx1 {
	public static void main(String[] args) {
		LocalDate today = LocalDate.now();
		LocalTime now = LocalTime.now();

		LocalDate someDate = LocalDate.of(2020,12,31);
		LocalTime someTime = LocalTime.of(23, 59, 59);

		System.out.println("today = " + today);							// 2021-10-28
		System.out.println("now = " + now);								// 18:53:52.266336
		System.out.println("someDate = " + someDate);					// 2020-12-31
		System.out.println("someTime = " + someTime);					// 23:59:59

		System.out.println(someDate.withYear(2000));					// 2000-12-31
		System.out.println(someDate.plusDays(1));						// 2021-01-01
		System.out.println(someDate.plus(1, ChronoUnit.DAYS));			// 2021-01-01

		System.out.println(someTime.truncatedTo(ChronoUnit.HOURS));		// 23:00

		System.out.println(ChronoField.CLOCK_HOUR_OF_DAY.range());		// 1 - 24
		System.out.println(ChronoField.HOUR_OF_DAY.rang());				// 0 - 23
	}
}
```

Instant

Epoch time(1970-01-01 00:00:00 UTC) 부터 경과한 시간을 나노초 단위로 표현

```java
Instant now = Instant.now();
Instant now2 = Instant.ofEpochSecond(now.getEpochSecond());
Instant now3 = Instant.ofEpochSecond(now.getEpochSecond(), now.getNano());

long epochSec = now.getEpochSecond();
int nano = now.getNano();

long toEpochMilli();
```

Instant는 항상 UTC(+00:00) 기준이기 때문에 LocalTime과 차이가 있을 수 있다.
시간대를 고려해야 한다면 OffsetDateTime이 더 좋은 선택이다.

Instant는 java.util.Date를 대체하기 위한 것이다.
JDK 1.8부터 Date와 Instant 간 변환할 수 있는 method가 추가되었다.

```java
static Date from(Instant instant);		// Instant -> Date
Instant toInstant();					// Date -> Instant
```

LocalDateTime / ZonedDateTime

LocalDate와 LocalTime을 합쳐 LocalDateTime을 만들 수 있다.

```java
/* LocalDate + LocalTime -> LocalDateTime */
LocalDate date = LocalDate.of(2020, 12, 31);		// 2020-12-31
LocalTime time = LocalTime.of(12, 34, 56);			// 12:34:56o

LocalDateTime dt = LocalDateTime.of(date, time);
LocalDateTime dt2 = date.atTime(time);
LocalDateTime dt3 = time.atDate(date);
LocalDateTime dt4 = date.atTime(12, 34, 56);
LocalDateTIme dt5 = time.atDate(LocalDate.of(2020, 12, 31));
LocalDateTime dt6 = date.atStartOfDay();			// dt6 = date.atTime(0, 0, 0);

/* LocalDateTime으로 직접 지정 */
LocalDateTime dateTime = LocalDateTime.of(2020, 12, 31, 12, 34, 56);
LocalDateTime today = LocalDateTime.now();

/* LocalDateTime -> LocalDate / LocalTime */
LocalDateTime dt = LocalDateTime.of(2020, 12, 31, 12, 34, 56);

LocalDate date = dt.toLocalDate();					// LocalDateTime -> LocalDate
LocalTime time = dt.toLocalTime();					// LocalDateTime -> LocalTime

/* LocalDateTime -> ZonedDateTime */
LocalDateTime dateTime = LocalDateTime.of(2020, 12, 31, 23, 59, 59);
ZoneId zid = ZoneId.of("Asia/Seoul");
ZonedDateTIme = dateTime.atZone(zid);
System.out.println(zdt);					// 2020-12-31T23:59:59+09:00[Asia/Seoul]

ZonedDateTime zdt2 = LocalDate.now().atStartOfDay(zid);
System.out.println(zdt2);					// 2021-10-29T00:00+09:00[Asia/Seoul]

ZoneId nyId = ZoneId.of("America/New_York");
ZonedDateTime nyTime = ZonedDateTime.now().withZoneSameInstant(nyId);
System.out.println(nyTime);					// 2021-10-28T12:42:33.003218-04:00[America/New_York]

/* UTC와의 시간 차 */
ZoneOffset krOffset = ZonedDateTime.now().getOffset();	// krOffset = ZoneOffset.of("+9");	// +09:00
int krOffsetInSec = krOffset.get(ChronoField.OFFSET_SECONDS);	// 32400 (= 3600 * 9)

/* OffsetDateTime : 다른 시간대에 존재하는 컴퓨터간의 통신에 필요 */
ZonedDateTime zdt = ZonedDateTime.of(date, time, zid);
OffsetDateTime odt = OffsetDateTime.of(date, time, krOffset);
System.out.println(odt);					// 2020-12-31T23:59:59+09:00

/* ZonedDateTime -> OffsetDateTime */
OffsetDateTime odt2 = zdt.toOffsetDateTime();
System.out.println(odt2);					// 2020-12-31T23:59:59+09:00

/* GregorianCalendar <-> ZonedDateTime */
GregorianCalendar gc = GregorianCalendar.from(ZonedDateTime zdt);	// static method
ZonedDateTime zdt4 = gc.toZonedDateTime();
```


