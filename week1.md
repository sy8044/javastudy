* JVM이란 무엇인가
* 컴파일 하는 방법
* 실행하는 방법
* 바이트코드란 무엇인가
* JIT 컴파일러란 무엇이며 어떻게 동작하는지
* JVM 구성 요소
* JDK와 JRE의 차이
__________

## JVM이란 무엇인가
The JVM is a program that provides the runtime environment necessary for Java programs to execute
JVM은 자바 프로그램이 실행할 수 있는 환경을 제공해준다. JVM이 없으면 자바 프로그램은 실행될 수 없다.

## 컴파일 하는 방법
.java파일로 부터 자바의 컴파일이 시작된다. javac 프로그램에 자바 소스코드가 들어가면 클래스 파일인 .class가 생성된다
.class파일은 자바 바이트코드로 구성되어있다. 클래스 파일은 기능적으로 작동하는 가장 작은 단위이다.
이 클래스 파일은 클래스로딩 메커니즘에 의해 jvm으로 들어가게되고 jvm 내부의 interpreter에서 코드가 실행된다
```
javac 소스파일명.java
```
위와 같이 입력하게 되면 소스파일명.class파일이 해당경로에 생성된다

## 실행하는 방법
```
java 소스파일명 // 확장자는 붙이지 않는다
```
위와 같이 입력하게 되면 자바파일이 실행된다 정확히 말하면 바이트코드로 변환된 .class파일이 jvm으로 들어가 실행된다

## 바이트코드란 무엇인가
"a computer inside a computer" JVM이 처음 소개되었을 때 개발자들이 했던 말이다.
바이트코드는 "machine code for the CPU of the internal computer"라고 볼 수 있다.
JVM이 하나의 컴퓨터이고 바이트코드는 JVM에 사용되는 기계언어가 되는 것이다.
바이트코드 자체는 진짜 하드웨어에 사용되는 머신코드와는 차이가 있고 소스코드와 머신코드 중간 그 어딘가이다..
바이트코드의 존재 목적은 JVM의 interpreter에서 효율적으로 실행되는 것에 있다
바이트코드는 opcode가 single byte로 구성되어 있어 바이트 코드라 불린다. 따라서 최대 256개의 명령어가 가능하지만 실제로 약 200개 정도가 사용된다
초기에는 바이트코드의 최적화가 중요하다고 생각해서 javac에서 heavily optimized된 바이트코드를 만들었지만 JIT compilation의 등장으로
JIT compiler가 해야할 일을 줄이는 것이 더 중요하다는 쪽으로 결론이 나게 되었다(바이트코드는 interpreted까지 되야 한다)

## JIT컴파일러란 무잇이며 어떻게 동작하는지
<img src="https://blog.kakaocdn.net/dn/cHjtfE/btqxxbXAtjD/Bmr5hhVZEzpkVDYfvcEu61/img.png" width="450px" height="300px"></img><br/>
JIT컴파일러는 바이트코드를 받아서 컴퓨터가 읽을 수 있는 머신코드로 바꾼다
바이트코드를 interpret 하는 것이 자바 프로그램의 실행 속도를 늦춘다라는 말이 있기에 JIT컴파일러는 실행 속도를 개선시켜줬다
메소드가 JIT컴파일러를 통해 컴파일되면 JVM이 컴파일된 코드를 interpret하지 않고 직접적으로 가져와 사용한다
JIT컴파일러는 바이트코드를 컴파일할 때 약간의 최적화를 해준다. 하지만 JIT컴파일러에서 최적화를 많이 할 수록 실행 단계에서 많은 시간이 소모되기에
모든 최적화를 해주지 않는다.
내부에 바이트코드를 머신코드로 컴파일을 해주는 임계값(threshold)가 존재하고 실제로 같은 코드를 임계값보다 많이 호출하게 되면 속도가 느려진다

## JVM 구성 요소
JVM이 a computer inside a computer 즉 컴퓨터 내부에 있는 하나의 컴퓨터이기에 컴퓨터가 가지고 있는 기본적인 스택, 힙, PC 등을 가지고 있다
<br/><img src="https://blog.kakaocdn.net/dn/bCbjhU/btqP4lHUosS/BKeS6sZJxqSQlaCpRDr4kk/img.png"></img><br/>
컴파일된 클래스를 로드하는 클래스 로더, 코드를 실행하는 execution, 프로그램을 수행하기 위해 운영체제로부터 할당받은 runtime data area가 있다
컴파일된 .class파일을 JVM내로 load하고 link하는 과정이 클래스 로더에서 진행된다.
interperter는 바이트코드를 명령어 단위로 읽어서 실행한다. 파이썬이 대표적인 인터프리터 언어이고 인터프리터 방식은 한 줄씩 읽기에 속도가 느리다
따라서 JIT컴파일러가 등장을 하였고 JIT컴파일러가 컴파일하는 시간이 인터프리팅하는 시간보다 기므로 특정 메소드들이 일정 횟수를 넘어가면 JIT컴파일러에서 컴파일을 해준다
<br/><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FNRdcI%2FbtqQee8MSOa%2Fg0BkKjZ6hoQ4fv7obHVwm0%2Fimg.png"></img><br/>
