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
