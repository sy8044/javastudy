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

## JIT컴파일러란 무엇이며 어떻게 동작하는지
<img src="https://blog.kakaocdn.net/dn/cHjtfE/btqxxbXAtjD/Bmr5hhVZEzpkVDYfvcEu61/img.png" width="450px" height="300px"></img><br/>
JIT컴파일러는 바이트코드를 받아서 컴퓨터가 읽을 수 있는 머신코드로 바꾼다
바이트코드를 interpret 하는 것이 자바 프로그램의 실행 속도를 늦춘다라는 말이 있기에 JIT컴파일러는 실행 속도를 개선시켜줬다
메소드가 JIT컴파일러를 통해 컴파일되면 JVM이 컴파일된 코드를 interpret하지 않고 직접적으로 가져와 사용한다
JIT컴파일러는 바이트코드를 컴파일할 때 약간의 최적화를 해준다. 하지만 JIT컴파일러에서 최적화를 많이 할 수록 실행 단계에서 많은 시간이 소모되기에
모든 최적화를 해주지 않는다.
내부에 바이트코드를 머신코드로 컴파일을 해주는 임계값(threshold)가 존재하고 실제로 같은 코드를 임계값보다 많이 호출하게 되면 속도가 느려진다
JIT컴파일러와 인터프리터는 별개의 쓰레드에서 동시에 실행되고 인터프리터가 해석하다가 자주 사용되는 부분이라 판단되면 기계어로 캐싱해서
메모리에 넣어놓는다 캐싱된 코드가 나타나면 JIT컴파일러가 가져와서 실행을 한다

## JVM 구성 요소
JVM이 a computer inside a computer 즉 컴퓨터 내부에 있는 하나의 컴퓨터이기에 컴퓨터가 가지고 있는 기본적인 스택, 힙, PC 등을 가지고 있다
<br/><img src="https://blog.kakaocdn.net/dn/bCbjhU/btqP4lHUosS/BKeS6sZJxqSQlaCpRDr4kk/img.png"></img><br/>
컴파일된 클래스를 로드하는 클래스 로더, 코드를 실행하는 execution, 프로그램을 수행하기 위해 운영체제로부터 할당받은 runtime data area가 있다
컴파일된 .class파일을 JVM내로 load하고 link하는 과정이 클래스 로더에서 진행된다.
interperter는 바이트코드를 명령어 단위로 읽어서 실행한다. 파이썬이 대표적인 인터프리터 언어이고 인터프리터 방식은 한 줄씩 읽기에 속도가 느리다
따라서 JIT컴파일러가 등장을 하였고 JIT컴파일러가 컴파일하는 시간이 인터프리팅하는 시간보다 기므로 특정 메소드들이 일정 횟수를 넘어가면 JIT컴파일러에서 컴파일을 해준다
<br/><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FNRdcI%2FbtqQee8MSOa%2Fg0BkKjZ6hoQ4fv7obHVwm0%2Fimg.png"></img><br/>
다음 명령어가 실횡될 주소를 가지고 있는 PC레지스터, 메소드를 빠져나가면 소멸되는 데이터를 저장하기 위해 사용되는 JVM stack
native method stack에서는 실제 실행할 수 있는 기계어로 작성된 프로그램을 실행시키는 영역이다
<br/><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUmvqI%2FbtqP12u6HDs%2FiIVNG8q95U0299Dq0vRHOk%2Fimg.png"></img><br/>
힙은 다음과같이 3가지로 구성되어 있는데
permanent generation은 생성된 객체들의 주소값이 저장된다
new/young generation의 eden영역은 객체들이 최초로 생성되는 공간이고 이곳이 가득차게 된다면 첫 번째GC(minor GC)가 발생한다
이 minor GC가 일어나면 eden영역에 있던 객체들 중 살아남은 객체들은 survivor 영역에 복사가 되고 나머지 영역의 객체들은 삭제된다
Tenured Generation은 New Generation에서 일정 시간 참조되며 살아있는 객체들이 저장되는 공간이다. 
즉 minor GC를 일정 횟수 이상 버틴 객체들이 이동하는 곳이다

method area는 클래스 정보를 처음 메모리 공간에 올릴 때 초기화되는 대상을 저장하기 위한 메모리 공간이다.
method area가 클래스 데이터를 위한 공간이라면 heap은 객체를 위한 공간이다

## JDK와 JRE의 차이
java development kit의 줄임말인 jdk는 java플랫폼에서 java 응용 프로그램을 개발하는데 사용되는 소프트웨어 개발 환경이다
java runtime environment의 줄임말인 jre는 이미 컴파일 된 자바 어플리케이션을 실행한다
jdk는 자바 프로그램을 개발하고 실행할 수 있는 환경을 제공하지만 jre는 자바 프로그램을 실행하는 환경만을 제공한다.
jdk는 jde와 개발도구들이 있는 것이고, jre는 jvm과 라이브러리 파일들이 있는 것이다


#### 느낀점
사실 언어를 배울 때 단순히 코딩하는 방법에만 집중을 하지 이런 본론적인? 것들에 대해서는 깊게 생각하지도 않고 이것이 중요한가 싶었다
컴파일이나 실행도 그냥 간단하게 인텔리제이에서 실행버튼 누르면 뚝딱 해줘서 뭔 과정이 있는지 궁금하지도 않았는데
하나하나 찾아가다 보니 생각한 것보다 복잡하고 어려웠다
이해가 되지 않는 부분들에 대해서는 적지 않아서 내용이 매우 난잡한 것 같아 나중에 아는 것이 많아지면 좀 더 수정해야겠다
