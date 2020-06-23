---
title: "Java 기초 개념 정리"
date: 2020-06-23
categories: Java TIL
---

자바를 사용하는 곳은 정말 많고 다양합니다.
이번에 컴퓨터 언어 수업을 수강하게 되어 시험 대비 겸 자바에서 사용하는 개념 및 문법을 정리하고자 합니다. :smile:
나중에 혹시나 자바 개발이 필요할 때 자료를 참고할 저를 위해 해당 글을 작성하게 되었습니다.


이 글에서 다룰 내용은 다음과 같습니다. 


[반복문, 조건문, 배열, 함수, 오버로딩, 클래스, 생성자 함수, 접근 제어자,
상속, 오버라이딩, 추상클래스, 인터페이스, 형변환, 다형성, static, 재귀함수, 
예외처리, 입력, 어레이리스트, 해시맵]


> Array


```java
// 1. arr 선언후 직접 대입하는 방법
int[] arr1 = new int[5];
arr1[0] = 100;
arr1[1] = 100;
arr1[2] = 100;
arr1[3] = 100;
arr1[4] = 100;

// 값을 넣고 선언
int[] arr2 = {10, 20, 30, 40, 50};

// 멀티 배열 작성법
int [][] arrMul = new int [3][2];
arrMul[0][0] = 10;
arrMul[0][1] = 100;
```

> 자료형


```java
int x = 10;
int y = 20;

System.out.println(x/y); // result: 0
// x, y 모두 정수형이기에 결과도 정수인 0으로 출력된다.
```


> do while 문, 반복문


```java
		// 조건이 틀리더라도 무조건 한 번은 출력을 한 번은 한다. - Chicken 출력된다.
		do {
			System.out.println("Chicken");
		}
		while (false);
		
		// 구구단 출력하기
		for (int a=2; a<10; a++) {
			for (int b=1;b<10;b++) {
				System.out.println(a+"*"+b+"="+a*b);
			}
		}
```

> 함수


클래스를 실행할 때, 따로 함수를 호출하지 않아도 main 함수는 실행된다.
자바의 함수를 사용할 때, 원하는 return의 자료형이 있다면 함수 선언시 함께 선언해주어야 한다.
만약 return 값을 원하지 않는다면 void 를 사용한다.

```java
	// 매개변수: 함수에 값을 전달해 주는 변수이다. 
	// 변수 앞에 자료형을 꼭 입력해주어야만 한다. 
	public static double multiple(int a, int b) {
		int result = a*b;
		return result;
	}
```

> 오버로딩(Overloading) 개념이란?


자바에서 사용되는 개념이다.
동일한 이름으로 여러 함수를 선언할 수 있는데, method의 이름은 동일하게 하되 매개 변수의 자료형에 따라 다른 내용의 함수 작성이 가능하다.
```java
	public static int minus(int a, int b) {
		return a-b;
	}
	public static double minus(double a, double b) {
		return a-b;
	}
```


> 클래스(Class)와 생성자 함수

클래스는 int, char 등이 대표되는 자료형과 같은 일종의 객체를 만들 수 있게 한다.
흔히들 예시로 많이 나오는 것이 Car로 예시를 드는데 간단히 책으로 예시를 들어보고자 한다.
클래스로 객체를 만들 때, 딱 한 번 실행되는 함수를 생성자 함수라 한다.
이 함수는 클래스 이름과 같아야 한다.

```java
class Book {
	String Name;
	int page;
	String Author;
	
  // 생성자 함수 - 클래스로 객체를 만들 때 딱 한 번 실행됨. (단, 클래스 이름과 동일해야 함!)
	Book(String a, int b, String c) {
		Name = a;
		page = b;
		Author = c;
	}
	public void print() {
		System.out.println(Name+"/"+Author+"/"+page);
	}
}
// 그 후 메인 함수에서 아래와 같이 Book 객체를 생성하면 된다.
// Book book = new Book("치킨", 1,  "냠냠");
```

> 접근제어자: public, protected, private

public: 어디서든 사용 가능
protected: 상속받은 자식 클래스에서만 사용 가능
private: 본인 객체에서만 사용 가능
안쓰기: 같은 패키지내에서만 사용 가능


> 상속


상속은 피상속 객체의 데이터 및 함수들을 그대로 이어받아 사용할 수 있다.
오버라이딩은 자식 클래스에서 재정의가 가능한 것을 의미한다.
부모 클래스에서 protected로 정의한 것은 상속받은 자식 클래스에서도 사용이 가능하다.
단, private로 선언된 경우는 본인 클래스에서만 사용이 가능하다.

```java
class BMW extends Cars {
	// 부모 클래스에 있는 생성자를 동일하게 만들어 준다 
	// 만들어주지 않으면 오류가 발생한다.
	// super = 부모 생성자의 함수.. 그래서 아래 부모께 실행이 되는 것..!
	BMW(String c, int v, int w) {
		super(c, v, w);
	}
	
	// BMW에만 주고 싶은 기능이 있다면 ?! 이렇게 만든다. 
	public void light() {
		System.out.println("불켜!");
	}

	// 아래와 같은 경우, 오버라이딩의 개념 - Car 클래스에 이미 left()가 정의된 경우
  
	// 오버라이딩 : 자식 클래스에서 재정의 가능함 
	public void left() {
		System.out.println("부드러운 좌회전");
	}
}
```


> 추상클래스(abstract class)


추상클래스란, 말 뜻 그대로 구체적이지 않은 클래스이다.
추상메소드는 어떤 기능을 하는지 로직을 작성하지 않으며 오직 자식에서 작성할 수 있게끔 한다.
추상클래스를 상속받는 자식 클래스 안에서 새로운 함수를 사용할 수도 있다.


```java
// Animal이란 추상클래스 만들기

abstract class Animal {
	String name;
	public Animal(String n) {
		name = n;
	}
	public void run() {
		System.out.println("와다다!");
	}

  // 추상메소드 voice();
	abstract public void voice();
}

class Cat extends Animal {
	public Cat(String n) {
		super(n);
	}

	@Override
	public void voice() {
		System.out.println("애오옹-");
	}
}
```


> 인터페이스(Interface)


인터페이스는 주로 어떤 기능이 있는지부터 정의하고 싶을 떄 사용한다.
함수와 정수등 내부 코드가 자세히 작성되어있는 일반 클래스와 달리, 추상 메소드만 사용이 가능하다.


```java

// interface로 선언하기
interface Controller_v2 {
	abstract public void play();
}
interface Controller {
	abstract public void stop();	
}

// 추상 클래스를 상속 받았던 것처럼 모든 값들을 정의해줘야 된다. 
// 여러 개 상속 받을 수도 있다.
class MP3Player_Ver1 implements Controller, Controller_v2 {
	@Override
	public void play() {
		// TODO Auto-generated method stub
		System.out.println("play");
	}

	@Override
	public void stop() {
		// TODO Auto-generated method stub
		System.out.println("stop");
	}
}
```


> 형변환


형변환이란 자료형을 바꿔주는 것을 의미합니다.

```java
double a = 3.14;
int b = (int) a;
```

> 입력 받기


사용자의 입력을 받는 데엔 scanner가 존재합니다.
string만을 입력받을 때는 buffered reader를 이용해서 받을 수도 있습니다.


```java
    // 스캐너를 이용한 입력 받기
		Scanner scanner = new Scanner(System.in);
		System.out.print("정수를 입력하세요.:");
		iVal = scanner.nextInt();
		
		System.out.println("입력한 정수:"+iVal);
		
		System.out.print("실수를 입력하세요.:");
		dVal = scanner.nextDouble();
		System.out.println("입력한 실수:"+dVal);
		
		
		// buffered reader를 이용해 입력받기
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		System.out.print("문자열을 입력하세요: ");
		sVal = br.readLine(); // 예외처리를 하지 않으면 오류 발생!
		System.out.println("입력 문장열: "+sVal);
```

> 예외처리


예외를 처리하고 싶을 땐 try catch를 사용한다.
```java
try {
      실행 문장
		} catch(Exception e) {
			System.out.println("예외 발생! "+e);
		}
```

> 반복문에서의 break와 continue

continue는 아래 반복문 문장 싹 빼고 다음 문장으로 넘어가고자 할 때,
break는 아래 문장에서 멈추고자 할 때 사용한다.


> static


따로 불렀던 변수를 불러 호출하는 것이 아닌, 처음 호출했던 클래스로 호출이 가능하다.
모든 객체가 공통적으로 공유되기 때문에 값을 바꿀 수 없다.


> 재귀함수


> ArrayList


기존의 Array보다 조금 더 사용하기 쉬운 배열 클래스이다.
파이썬에서 사용하던 배열이 떠오른다. 여전히 배열의 자료형은 함께 선언해주어야 한다.
아래처럼 import 하여 쉽게 사용이 가능하다.

```java
import java.util.ArrayList;
```


```java
		ArrayList<String> list = new ArrayList<String>();
		
		list.add("hello"); // 값 추가
		list.set(0, "java"); // 값 변경
		list.remove(0); // 값 제거
    list.clear(); // 전체 값 지우기
    list.isEmpty(); // 빈 리스트인가?
```

> 해시맵


key와 value 값을 설정해서 넣어줄 수 있다.
이것 또한 java.util.HashMap으로 불러올 수 있다.


```java
HashMap<Integer, String> map = new HashMap<Integer, String>();
map.put(5,  "hello");
map.put(1, "java");
    
String str = map.get(5); // 값 꺼내올 때

```


역시 자바의 세계는 어렵네요. 끝까지 읽어주셔서 감사합니다~ 열공이에요 😎
