---
tag : oop 백엔드
aliases : 자바
---

# 개요
> zulu8 JDK / 자바 1.8 버전 / IDE([[이클립스]] 2021-06) / 톰캣 8.5.78v 기준 설명

-  VSC에서 자바하려면 JDK 17버전 이상 필요
-  **자바에 대해서** 
	- 객체지향프로그래밍 언어 #oop
	- 자바에서는 object가 클래스로 자바의 업무 단위는 프로젝트가 기본
	- **장점** : JVM을 통해 어느 운영체제에서도 작동
	- **단점** : JVM 때문에 작동이 느림
- **자바의 네이밍 규칙**
	- 대문자 : 프로젝트 / 소스파일
	- 소문자 : 패키지

# 자바 설치하기
- [zulu8 오픈자바JDK](https://www.azul.com/downloads/?version=java-8-lts&os=windows&architecture=x86-64-bit&package=jdk#zulu)
- [오라클 / 유료](https://www.oracle.com/java/technologies/downloads/)
- [이클립스_2021-06 R](https://www.eclipse.org/downloads/packages/release/2021-06/r)
- [Apache Tomcat® - Apache Tomcat 8 Software Downloads](https://tomcat.apache.org/download-80.cgi)

## 환경변수 설정 : JAVA_HOME, Path
- 제어판 -> 시스템 환경변수 검색 -> 새로추가 

## [[이클립스]] 설정
## [[이클립스]] 메뉴바 편리기능


# 자바 기초 문법
```java
import java.util.Scanner;
public class HelloWorld{
    public static void main(String[] args){
        System.out.println("Hello World!");
    }
}
```
- 자바는 클래스가 기본 단위로 클래스 안에는 멤버변수(필드)와 메소드를 가지고 있음
- 클래스 :  멤버변수, 메소드, 생성자
- 코드 작성형식 : 람다식(객체지향의 단점을 극복하기 위해서 ) 등 #설명보완필요

## 데이터 타입
- 기본 데이터 타입 Primitive type
	- 정수형 : byte, short, int(기본), long
	- 실수형 : float, double(기본)
	- 논리형 : Boolean
	- 문자 : char(아스키 코드 값을 대입해서 문자를 처리)
	- 초기값 
		- 숫자 : 0
		- char : '\u0000'(공백)
		- boolean : false
	- 메모리 저장영역 : 스택
- 참조 데이터 타입 Reference type
	- String 같은 배열이나 객체 등 #자바VO
	- 초기값 : null
	- 메모리 저장영역 : 힙
		스택에서 힙영역에 저장된 참조 데이터 타입의 메모리 번지를 가지고 있음
### 각 데이터 타입간의 케스케이딩 방법
- 강제 형변환
	```java
	int num = (int)"10";
	```
- 기본 데이터타입의 레퍼클래스를 이용한 방법 #래퍼클래스
	```java
	Integer.praseInt(변환할 자료형);
	```



## 제어자
| 사용위치    | 제어자명                                     |
| ----------- | -------------------------------------------- |
| 클래스      | public, default, final, abstract, implements, extends |
| 메서드      | 접근제어자 모두, final, abstract, implements |
| 멤버변수    | 접근제어자 모두, final, static               |
| 지역변수    | final                                        |
| 초기화 블록 | static 등                                    |

### 접근 제어자
> #oop 의 #캡슐화 개념핵심
> public > protected > default > private / 하나만 사용가능 

| 키워드    | 접근 가능영역                        |
| --------- | ------------------------------------ |
| public    | 외부 클래스                          |
| protected | 같은 패키지 내부와 상속관계 클래스만 |
| default   | 같은 패키지 내부만                   |
| private   | 같은 클래스 안에서만, 외부 클래스에서 사용불가   |

### 이외의 제어자
| 키워드                                     | 설명                                                                                                         |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| final                                      | #상수, 재정의 불가                                                                                           |
| static | #정적메모리, #공용사용메모리, #클래스변수 프로그램 로드시 메모리에 올려두기 때문에 인스턴스 안해도 클래스이름과 점연산자를 통해서 접근가능             |
| abstract                                   | #추상화 클래스 를 정의할때 사용하는 키워드로, 메소드 선언부만 정의하고 상속받은 클래스에서 구현을 해서 사용함   |
| extends                            |   #상속 클래스에서만 사용할 수 있는 키워드로 부모 클래스를 상속받은 자식 클래스는 부모 클래스의 멤버변수와 메소드를 사용할 수 있음                                                                                                       |
| implemetns                                 | #interface 를 받아서 클래스에 상속시킨다고 생각하면 되지만, 상속과는 달리 여러 인터페이스를 연결시킬 수 있음 |




# 객체지향 개념

> 자세한 것은 : [[프로그래밍 언어론#객체지향 프로그래밍(objective programming) oop]]


## 객체 간의 협력
- StringBuffer를 사용해서 append 
- 필터링은 어떻게 하는거지?
- 메소드 호출호출





## 싱글톤 패턴



# 예외처리
- try~catch
	```java
	try {
		String[] sub = request.getParameterValues("subject");
		if (sub != null) {
			for (int i = 0; i < sub.length; i++) {
				System.out.println(sub[i]);
			}				
		}
	} catch (Exception e) {
		System.out.println("예외발생");
	}
	```

- throws : 호출하는 쪽으로 뒤에 있는 클래스를 넘겨줌


# JVM의 작동과정
- 다른 프로그래밍언어와 동일하게 컴파일과 해석과정을 거치지만 JVM(자바 버추얼머신)이 관여하는 점에서 다른 프로그래밍 언어와 다름
- JVM은 엔트리 포인트에서부터 클래스 코드를 읽고 작동


# 용어정리

## 레퍼 클래스(Wraper Class)
- 자바에서 자료형은 객체가 아니니까 객체지향에 위배되기에 자료형을 객체로 감싸는 느낌으로 만든 클래스를 레퍼 클래스라고 함

## 자바 JDK (Java Development Kit)
- 자바의 소프트웨어 개발키트( #SDK)
- **JDK 구성** #JDK 
	- apt : 어노테이션 툴
	- appletviewer : 웹 브라우저 없이 자바 애플릿을 실행하고 디버깅하기 위한 툴
	- javac : 자바 컴파일러
	- java : 컴파일한 클래스 파일을 해석 및 실행
	- jar : 서로 관련 있는 클래스 라이브러리들과 리소스를 하나의 파일로 묶어주는 툴
	- jdb : 자바 디버깅툴
	- JRE(Java Runtime Enviroment) : 자바가 동작하는데 필요한 JVM, 라이브러리 등 다양한 파일을 포함
	- JVM(Java Virtual Machine) : 자바가 실제로 동작하는 가상환경
		- 어느 운영체제에서도 원활하게 동작가능
## 자바간 패키지 설명
### Java SE 
- 표준 자바 플랫폼으로 표준적인 컴퓨팅 환경을 지원하기 위한 자바 가상머신 규격 및 API 집합을 포함
- `java.lang.*`, `java.util.*` `java.awt.*`, `javax.rmi.*`, `javax.net.*` 등

### Java EE
- Java SE에 웹APP 서버에서 동작하는 기능을 추가한 플랫폼
- 이 스펙에 따라 제품을 구현한 것을 웹APP 서버( #was)라고 함
- [[JSP]], [[Servlet]], [[JDBC]], JNDI, JTA, EJB 등