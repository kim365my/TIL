---
tag : 웹서버 데이터분석
aliases : 파이썬
---

# 개요
>[!info] 프로그래밍 언어 학습이나 웹서버, 데이터 분석 분야에서 자주 사용되는 언어
>>[!warning] 다른 프로그래밍 언어와 다른 점
>> - 주석기호 : `#`
>>	- 구글 코랩에서 마크 다운과 호환됨(다른 IDE는 잘 모르겠음)
>> - 프로그램은 대비가 안되어있으면 에러를 내뱉고 그 에러를 셉션이라고 함 
>> - 들여쓰기에 의미를 부여?
>>	- 파이썬은 C와 다르게 {}에 따라 블럭을 정의하지 않고 띄어쓰기에 따라 블럭을 정의
>
>- `<run selection/line in python terminal>` : 단축기는 <Shift + Enter>마우스 오른쪽 버튼 클릭시 나옴. 선택한 코드 부분만 터니멀에서 실행하겠다는 의미로  코딩하다가 잘못 눌러 문장이 실행되면 SyntaxError: invalid syntax 오류가 콘솔창에 난다. 콘솔창에 >>>exit를 작성해 나가거나 쓰레기통 모양을 클릭해 나갈 수 있음
> - 에코잉(메아리) 기법 : 어떤 데이터 값만 집어넣으면 해당 데이터를 그대로 콘솔에 출력하는 것을 말함

>[!quote]- 참고문서
> - 파이썬 홈페이지 : [Welcome to Python.org](https://www.python.org/)
> - 파이썬 자습서
> 	- [8. Errors and Exceptions - Python 3.9.5 documentation](https://docs.python.org/ko/3/tutorial/errors.html)
> 	- [사장님 몰래하는 업무 자동화](https://wikidocs.net/135796)
> - 파이썬 강의 북마크 해놓은 것 
> 	- ['파이썬 강의/기본편' 카테고리의 글 목록](https://nadocoding.tistory.com/category/%ED%8C%8C%EC%9D%B4%EC%8D%AC%20%EA%B0%95%EC%9D%98/%EA%B8%B0%EB%B3%B8%ED%8E%B8)
> 	- [9.1 오류의 종류 | 연오의 파이썬 프로그래밍 입문서](https://python.bakyeono.net/chapter-9-1.html)
> 	- [위키독스](https://wikidocs.net/20343)
> 	- [파이썬(Python) - 예외사항 처리](https://truman.tistory.com/109)
> 	- https://github.com/jaehwachung/Python-Programming



# 파이썬 환경설정
- IDE 선정
	- [구글 코랩](https://colab.research.google.com/?hl=ko) : 온라인
	- [[VSC]] : 파이썬 익스텐션 설치하면 좋음
- 파이썬 설치
	- 코어 파이썬
	- [아나콘다 파이썬](https://www.anaconda.com/download)


# 기본 문법
## 예약어 : 언어에 미리 정의된 단어

- 탈출문자(이스케이프 문자, 다른 프로그래밍 언어에서도 동)
	- `\n` : 줄바꿈
	- `\"` : 따옴표를 표시하고 싶을 때
	- `\\` : 문장 내에서 \를 표시하는 경우 \는 탈출문자로 사용되기에 \\두번 표시해야 \로 정상적으로 출력됨
	- `\r` : 커서를 맨 앞으로 이동
	- `\b` : 백스페이스(한 글자 삭제)
	- `\t` : 탭(Tab)

## 자료처리형
>[!warning] 언어의 내장된 함수와 동일한 이름은 사용할 수 없다. 또한 메모리 주소값이 변경되는 것이지 값이 변하는 것은 아니다.

- 상수(constant) : 값이 불변인 자료
- 변수(variable) : 값이 변할 수 있는 자료

### 자료구조의 변경
- 자료구조 타입 확인 : print(변수명, type(변수명)) 
- 사용법 : 변수명 = 자료구조명(변수명)
- 자료구조 종류
	1. list : 순서를 가지는 객체의 집합
	2. tuple : 리스트와 다르게 내용의 변경이나 추가를 할 수 없지만 속도가 리스트보다 빠름.
	3. set : 중복이 안되고 순서가 없음

>[!example]- 리스트[]
> ```python
> subway = [10, 20, 30]
> print(subway)
> 
> subway = ["유재석", "조세호", "박명수"]
> print(subway)
> 
> # 조세호씨가 몇번째 칸에 타고 있는가
> print(subway.index("조세호"))
> 
> # 하하씨가 다음 정류장에서 다음 칸에 탐
> subway.append("하하")
> print(subway)
> # 뒤에 삽입
> 
> # 정형돈씨를 유재석 / 조세호 사이에 태워봄
> subway.insert(1, "정형돈")
> print(subway)
> 
> # 지하철에 있는 사람을 한 명씩 뒤에서 꺼냄
> print(subway.pop())
> print(subway)
> 
> # 같은 이름의 사람이 몇 명 있는지 확인
> subway.append("유재석")
> print(subway)
> print(subway.count("유재석"))
> 
> # 정렬도 가능
> num_list = [5,2,6,2,1]
> num_list.sort()
> print(num_list)
> 
> # 순서 뒤집기도 가능
> num_list.reverse()
> print(num_list)
> 
> # 모두 지우기
> num_list.clear()
> print(num_list)
> 
> # 다양한 자료형과 함께 사용
> num_list = [5,2,6,2,1]
> mix_list = ["조세호", 20, True]
> print(mix_list)
> 
> # 리스트 확장
> num_list.extend(mix_list)
> print(num_list)
> ```
> 

>[!example]- 사전
> ```python
> cabinet = {3:"유재석", 100:"김태호"}
> print(cabinet[3])
> print(cabinet[100])
> 
> # []로 열고 닫거나 .get()으로 사전에 있는 걸 불러올 수 있다.
> print(cabinet.get(3))
> # print(cabinet[5]) # 5에는 할당된 값이 없기에 오류가 나고 끝남 
> print(cabinet.get(5)) # get을 이용했을 경우 값이 없으면 none이라고 출력되고 뒤의 Hi도 나옴
> print(cabinet.get(5, "사용 가능")) # none 말고 다른 것을 기본으로 출력하고 싶은 경우
> print("hi")
> 
> print(3 in cabinet) # 3이라는 키가 있으면 True
> print(5 in cabinet) # 5이라는 키가 없으므로 False
> 
> # 정수형이 아닌 다른 형식으로 키를 정할 수 있음
> cabinet = {"A-3":"유재석", "B-100":"김태호"}
> print(cabinet["A-3"])
> print(cabinet["B-100"])
> 
> # 새 손님
> print(cabinet)
> cabinet["A-3"] = "김종국" # 유재석이라는 값이 빠지고 김종국이 들어감
> cabinet["C-20"] = "조세호" # 새로운 키 추가
> print(cabinet)
> 
> # 간 손님
> del cabinet["A-3"] # A-3의 데이터 삭제
> print(cabinet)
> 
> # key만 출력
> print(cabinet.keys())
> 
> # value 만 출력
> print(cabinet.values())
> 
> # key, value 쌍으로 출력
> print(cabinet.items())
> 
> # 목욕탕 폐점
> cabinet.clear() # 안의 모든 값을 싹 지움
> print(cabinet)
> ```

>[!example]- 튜플
> ```python
> menu = "돈가스", "치즈까스"
> # 괄호를 열고 닫고 보다는 콤마로 구분
> print(menu[0])
> print(menu[1])
> 
> # menu.add("생선까스") 오류남, 튜플은 추가나 변경을 할 수 없음
> # 튜플의 활용, 밑에 처럼 변수로 각각 선언할 수 있지만 튜플을 이용하면 코드가 깔끔해짐
> name = "김종국"
> age = 20
> hobby = "코딩"
> print(name, age, hobby)
> 
> (name, age, hobby) = ("김종국", 20, "코딩")
> print(name, age, hobby)
> ```

>[!example]- 집합(set)
> ```python
> my_set = {1,2,3,3,3}
> print(my_set) # {1,2,3} 중복을 허용하지 않음
> 
> java = {"유재석", "김태호", "양세형"}
> python = set(["유재석", "박명수"])
> 
> # 교집합 (java와 python을 모두 할 수 있는 개발자)
> print(java & python) #{'유재석'}
> print(java.intersection(python))
> 
> # 합집합 (java나 python을 할 수 있는 개발자)
> print(java | python)
> print(java.union(python))
> 
> # 차집합 (java는 할 수 있지만 python은 할 줄 모르는 개발자)
> print(java - python)
> print(java.difference(python))
> 
> # python을 할 줄 아는 사람이 늘어남
> python.add("김태호")
> print(python)
> 
> # java를 잊었어요
> java.remove("김태호")
> print(java)
> ```

>[!example]- 자료구조의 변경
> ```python
> menu - {"커피", "우유", "주스"} # 맨 처음 set로 자료를 만듬
> print(menu, type(menu)) 
> 
> menu = list(menu) # 리스트로 변경
> print(menu, type(menu))
> 
> menu = tuple(menu) # 튜플로 변경
> print(menu, type(menu))
> 
> menu = set(menu) # 다시 세트로 변경
> print(menu, type(menu))
> ```

>[!example]- 퀴즈 4
> ```python
> from random import *
> users = range(1, 21) # 1부터 20까지 숫자를 생성
> # print(type(users))
> users = list(users) # range 타입이므로 list로 바꾼다.
> shuffle(users) # shuffle을 통해 users를 섞는다.
> 
> winners = sample(users, 4) # 한명은 치킨, 3명은 커피
> 
> print("-- 당첨자 발표 --")
> print("치킨 당첨자 : {0}".format(winners[0]))
> print("커피 당첨자 : {0}".format(winners[1:]))
> print("-- 축하합니다 --")
> ```




## 연산자
- 비교연산(>,<)
- 앞과 뒤의 값이 똑같다를 확인하는 연산자 `(==)`
- 앞과 뒤의 값이 다르다고 표시하는 연산자(not, !)
- 두개이상의 항의 값이 모두 True일때 True(and, &)
- 두개이상의 항의 값 중 하나만 이라도 True이면 True라고 표시(or, |(키보드 백스페이스 바로 아래나 왼쪽))
- 두 숫자를 나눈 후 나머지 값을 구하는 연산자(//, %)
- 제곱근 연산자(**, ^)

## 주석(#, ''', ctrl+/)
- 단일주석 : `#`
- 복수주석 : 작은따옴표 3개('''), 큰따옴표도 됨
- 단축키 : ctrl+/
- 세미콜론(;)
	- 파이썬은 c언어와 다르게 코드 끝에 세미콜론을 붙이지 않아도 됨 붙여서 사용해도 문제 없음
	- 보통 파이썬에서 세미콜론은 문장이 끝나고 붙여놓을때 사용한다고함
	- 이런식으로 → `(print('예'); print('시'))`


## 자료형
- 출력가능한 자료형
	- 숫자 자료형
	- 문자열 자료형
	- boolean 자료형
- 정수형 출력시 str()함수를 사용해 주어야 함

>[!example] 
> ```python
> print("가나나다라마바사")
> print(5)
> ```
>
> ```python
> from random import *
> 
> date = randint(4,28)
> print("오프라인 스터디 모임 날짜는 매월 " + str(date) +"일로 선정되었습니다.")
> ```
- 따옴표 3개(""")를 통해 위처럼 길게 글을 표시할 수 있음
>[!example]- 문자열 출력 예시
> ```python
> sentence = '나는 소년입니다'
> print(sentence)
> 
> sentence2 = "파이썬은 쉬워요"
> print(sentence2)
> 
> sentence3 = """
> 			나는 소년이고,
> 			파이썬은 쉬워요
> 			"""
> print(sentence3) # 따옴표
> ```

## 변수와 주석
- 단일 주석은 `#`으로 하면 된다.
- 여러문장을 주석처리할 때 작은따옴표 3개(''')로 시작하고 작은따옴표 3개(''')로 닫으면 된다.
- 주석처리하고 싶은 문장을 드래그해서 `ctrl+/`를 하면 일괄적으로 `#`이 앞에 나오게 된다.

>[!example]- 변수 선언 및 출력예시
> ```python
> # 애완동물을 소개해 주세요
> animal = "강아지"
> name = "연탄이"
> age = 4
> hobby = "산책"
> is_adult = age >= 3
> 
> '''
> 한번에 주석처리
> '''
> 
> print("우리집의 "+ animal +" 이름은 "+ name +"에요")
> 
> hobby = "공놀이"
> 
> # print(name +"는 "+ str(age) +"살이며 "+ hobby +"을 아주 좋아해요")
> # ,(콤마)가 들어가게 되면 띄어쓰기가 됨
> 
> print(name +"는 ", age,"살이며 ", hobby,"을 아주 좋아해요")
> print(name +"는 어른일까요?" + str(is_adult))
> ```

>[!example]-  ,(콤마)가 들어가게 되면 띄어쓰기가 됨
> ```python
> # 변수를 이용하여 문장을 출력하기
> station = "사당", "신도림", "인천공항"
> print(station, "행 열차가 들어오고 있습니다.")
> ```

## 연산자
- 비교연산(>,<)
- 앞과 뒤의 값이 똑같다를 확인하는 연산자 (==)
- 앞과 뒤의 값이 다르다고 표시하는 연산자(not, !)
- 두개이상의 항의 값이 모두 True일때 True(and, &)
- 두개이상의 항의 값 중 하나만 이라도 True이면 True라고 표시(or, |(키보드 백스페이스 바로 아래나 왼쪽))
- 두 숫자를 나눈 후 나머지 값을 구하는 연산자(//, %)
- 제곱근 연산자(**, ^)

> [!example]- 연산자 예시
> ```python
> # 비교연산(>,<)
> print(3>1) # 3보다 1이 큰게 옳으므로 True
> print(1<3) # False
> print(3>=3) #True
> 
> # 앞과 뒤의 값이 다르다고 표시하는 연산자(not, !)
> print(1!=3) # != 는 앞과 뒤가 다르다는 의미 !과 =는 붙여서 사용해야함, 실행시 값은 Truw
> print(not(1!=3)) # not은 !과 같은 의미로 사용됨, 실행시 값은 False
> 
> # 두개이상의 항의 값이 모두 True일때 True(and, &)
> print((3>5) and (3<8)) 
> print((3>5) & (3<8)) 
> 
> # 두개이상의 항의 값 중 하나만 이라도 True이면 True라고 표시(or, |)
> print((3>5) or (3<8)) 
> print((3>5) | (3<8)) 
> 
> # 나머지 값을 구하는 연산자(//, %)
> print(10//3) # 나머지 몫 구하기
> print(5 % 3) #5나누기 3을 하면 2가 남으니까 표시되는 건 2
> 
> # 제곱근 연산자(**, ^)
> print(2**3) # 2^3(2의 3제곱) = 8
> print(2^3) # 2^3(2의 3제곱) = 8
> ```

> [!example]- 간단한 함수
> ```python
> print(2+3*4) #14
> 
> number = 2+3*4 # 변수선언 
> print(number) #14 number 변수표시
> 
> number = number + 2 #number변수의 값에 2를 더하고 그 값을 number에 재정의
> print(number) #16
> 
> number += 2 #number 값에 2를 더함
> print(number) #18 
> 
> number -= 2 #number 값에 2를 뺌
> print(number) #16
> 
> number /= 2 #number 값에 2를 나눔
> print(number) #8
> 
> number *= 2 #number 값에 2를 곱함
> print(number) #16
> 
> number %= 2 #number 값에 2를 나눈 값의 나머지
> print(number) #0
> ```

## 숫자처리함수
- abs : 절댓값을 표시하는 함수
- pow : 앞의 숫자의 제곱 pow(4, 2)는 4^2이다. 표시되는 값은 4*4니까 16으로 표시됨
- max : 두개 이상의 값이 있을 경우 최댓값을 찾아 표시해주는 함수
- min : 두개 이상의 값이 있을 경우 최솟값을 찾아 표시해주는 함수
- round : 반올림

>[!example]
> ```python
> #절댓값을 표시하는 함수
> print(abs(-5)) #5
> 
> #앞의 숫자의 제곱
> print(pow(4,2)) #4^2, 4*4 = 16
> 
> #두개 이상의 값이 있을 경우 최댓값을 찾아 표시해주는 함수
> print(max(5,12)) #12
> #두개 이상의 값이 있을 경우 최솟값을 찾아 표시해주는 함수
> print(min(5,12)) #5
> 
> #반올림
> print(round(3.14)) #3
> print(round(4.99)) #5
> ```

- from math import * 를 사용한 뒤 쓸 수 있는 함수
- floor : 내림
- ceil : 올림
- sqrt : 제곱근

>[!example]
> ```python
> from math import * #C언어의 #include와 비슷한 기능을 하는 듯??
> print(floor(4.19)) #내림
> print(ceil(4.19)) #올림
> print(sqrt(4)) #제곱근
> ```

## 랜덤함수
- from random import * 함수를 통해 파이썬 내부 함수를 불러옴
	- random
	- randrange
	- randint

>[!example]- 랜덤함수
> ```python
> from random import *
> 
> print(random()) #0.0이상 ~ 1.0미만의 임의의 값을 생성
> print(random()*10) #0.0이상 ~ 10.0미만의 임의의 값을 생성
> print(int(random()*10)) #int를 넣음으로써 정수값 0.0이상 ~ 10 미만의 임의의 값을 생성
> print(int(random()*10+1)) # +1 했으므로 정수값 1 ~ 11 미만의 임의의 값을 생성
> print(int(random()*45) + 1) # 1~46 미만의 임의의 값을 생성
> 
> #randrang와 randint함수
> print(randrange(1,46)) #1이상 46미만의 임의의 값 생성
> print(randint(1,45)) # 1이상 45이하의 임의의 값 생성
> ```

>[!example]- 슬라이싱
> ```python
> #위의 숫자를 잘라서 사용하는 걸 슬라이싱이라고 함
> #컴퓨터에서는 인덱스가 0부터 시작을 함
> jumin = "990120-1234567"
> 
> print("성별 : " + jumin[7])
> print("연 : " + jumin[0:2]) #0부터 2직전 값까지 (0~1를 표시)
> print("월 : " + jumin[2:4])
> print("일 : " + jumin[4:6])
> 
> print("생년월일 : " + jumin[:6]) #처음부터 6 직전까지의 값을 가져온다
> print("뒤 7자리 : " + jumin[7:]) #7부터 끝까지
> print("뒤 7자리 : (뒤에서부터)" + jumin[-7:]) #맨 뒤에서 7번째부터 끝까지
> ```

>[!example]- 문자열 처리함수
> ```python
> python = "Python is Amazing"
> 
> print(python.lower()) #python 변수에 부여된 문자열을 모두 소문자로 변경
> print(python.upper()) #python 변수에 부여된 문자열을 모두 대문자로 변경
> 
> print(python[0].isupper()) #python 변수의 0번째(P)가 대문자라면 True, 아니라면 False
> 
> print(len(python)) #글자수를 나타내는 함수
> 
> print(python.replace("Python", "Java")) #replace를 활용해서 문장 안의 값을 바꿀 수 있음
> 
> index = python.index("n") #index 함수를 활용해서 n이라는 글자가 몇번째 있는지 확인가능
> print(index)
> index = python. index("n", index + 1) #+1으로 아까 구한 5번째 n 위치에서 두번째 n위치를 찾을 수 있음
> print(index)
> 
> print(python.find("n")) # find함수도 비슷하게 n의 위치를 찾을 수 있음
> print(python.find("Java")) #-1 반환
> # print(python.index("Java")) 
> print("Hi")
> '''find는 내가 원하는 값이 포함되지 않을 경우 -1의 값을 반환하지만
> index로 Java를 찾으면 오류를 내면서 프로그램을 종료해버려 
> 그 뒤의 Hi가 표시되지 않음
> '''
> 
> print(python.count("n")) #python이라는 함수에서 n이 몇번 나왔는지 알려줌
> ```

>[!example]- 문자열 포멧
> ```python
> print("a"+"b")
> print("a", "b")
> # 이 방법외에도 "a"와 "b"문자열을 표시하는 게 가능하다.
> 
> '''방법 1 앞에 %d같은 걸 적은 후 뒤에 그곳에 들어갈 값을 적는다.'''
> print("나는 %d살입니다." % 20) # %d는 정수값만 받아들임.
> print("나는 %s을 좋아해요." % "파이썬") # %s는 문자열만 받아들임.
> print("Apple은 %c로 시작해요" % "A") # %c는 캐릭터라서 한 글자만 받겠다는 소리.
> 
> # %s로만 쓰면 정수건 문자건 상관없이 다 출력을 제어 할 수 있음
> print("나는 %s살입니다." % 20) # %d는 정수값만 받아들임.
> print("나는 %s색과 %s색을 좋아해요." % ("파란", "빨간")) #괄호 안에 있는 것들이 순서대로 들어감
> 
> '''방법 2 format() 사용'''
> print("나는 {}살입니다.".format(20))
> print("나는 {}색과 {}색을 좋아해요.".format("파란", "빨간"))
> print("나는 {0}색과 {1}색을 좋아해요.".format("파란", "빨간"))
> print("나는 {1}색과 {0}색을 좋아해요.".format("파란", "빨간"))
> 
> '''방법 3 format() 사용'''
> print("나는 {age}살이며, {color}색을 좋아해요.".format(age = 20, color ="빨간"))
> print("나는 {age}살이며, {color}색을 좋아해요.".format(color ="빨간", age = 20))
> 
> '''방법 4(v3.6이상부터 사용가능)'''
> # 중괄호 안에 있는 값을 실제 변수에서 가져와 사용할 수 있음
> age = 20
> color = "빨간"
> print(f"나는 {age}살이며, {color}색을 좋아해요.")
> ```

>[!example]- 익스케이프 문자 예시
> ```python
> # \n : 줄바꿈
> print("백분이 불여일견 \n백견이 불여일타")
> 
> # \" : 따옴표를 표시하고 싶을 때
> print("저는 \"나도 코딩\" 입니다.")
> print("저는 \'나도 코딩\' 입니다.")
> 
> # \\ : 문장 내에서 \를 표시하는 경우 \는 탈출문자로 사용되기에 
> # \\두번 표시해야 \로 정상적으로 출력됨
> print("C:\\Users\\kim365my\\Desktop\\파이썬 연습>")
> 
> # \r : 커서를 맨 앞으로 이동
> print("Red Apple\rpine")
> 
> # \b : 백스페이스(한 글자 삭제)
> print("Red \b Apple")
> 
> # \t : 탭(Tab)
> print("Red Apple\tpine")
> ```

- 어떻게해야 구동되는 건지 모르겠어
>[!example]
> ```python
> n = input() # n변수에 사용자가 입력하는 값을 대입
> # print( n + "이 홀수 인지 검사한다.")
> 
> def is_add(n) : #n은 매개 변수
> """n이 홀수 인지 검사한다."""
> return n % 2 != 0 
> 
> # is_add(0) 
> # print( n + "은 홀수가 아니다.")
> # is_add(1)
> # print( n + "은 홀수다.")
> # is_add(2)
> # print( n + "은 홀수가 아닌 데.")
> ```

>[!example]- 퀴즈 3
> ```python
> print("# 방법 1")
> naver = "http://naver.com"
> naver = naver.replace("http://", "")
> print(f"http:// 부분 제외 : {naver}")
> naver = naver.replace(".com", "")
> print(f".com 부분 제외 : {naver}")
> index = naver.index("n")
> 
> print("남은 글자 중 처음 세자리 : " + naver[index:3]) #nav
> print("글자 개수 : " + str(len(naver))) #5
> 
> count1 = naver.count("e") 
> print("글자 내 \"e\" 개수 : " + str(count1)) #1
> 
> print("생성된 비밀번호 : " + naver[index:3] + str(len(naver)) + str(count1) + "!") #nav51!
> 
> # 방법 2
> print("# 방법 2")
> url = "http://naver.com"
> my_str = url.replace("http://","") # 규칙1
> my_str = my_str[:my_str.index(".")] # 규칙 2
> # my_str[0:5] -> 0~5직전까지 (0,102,3,4)
> # print(my_str) 
> 
> password = my_str[:3] + str(len(my_str)) + str(my_str.count("e")) + "!"
> print("{0} 의 비밀번호는 {1}입니다.".format(url, password))
> ```



## 조건문
>[!example]- 분기(if문)
> ```python
> weather = input("오늘 날씨는 어때요? ")
> # input으로 사용자가 입력하는 것을 받아 들여서 weather에 저장
> 
> # 처음 if문에서 조건을 비교하고 맞으면 바로 밑으로 빠져나가고 아니면 다음 조건문으로 넘어거고
> # 다른 조건문의 조건도 맞지 않으면 else로 넘어감 else를 적음으로써 이도저도 아닐때 이걸 출력해라고
> # 명시해줄 수 있음
> if weather == "비" or weather == "눈": 
> 	print("우산을 챙기세요")
> elif weather == "미세먼지": 
> 	print("마스크를 챙기세요")
> else :
> 	print("준비물이 필요없어요")
> 
> temp = int(input("기온은 어때요 ? "))
> if 30 <= temp :
> 	print("너무 더워요. 나가지 마세요")
> elif 10 <= temp and temp < 30:
> 	print("괜찮은 날씨에요")
> elif 0 <= temp < 10:
> 	print("외투를 챙기세요")
> else:
> 	print("너무 추워요. 나가지 마세요")
> ```






# 데이터 분석
>[!quote]- 데이터 분석이란
> ![[데이터 분석]]

# 연관 문서