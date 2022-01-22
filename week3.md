* 산술 연산자
* 비트 연산자
* 관계 연산자
* 논리 연산자
* instanceof
* assignment(=) operator
* 화살표(->) 연산자
* 3항 연산자
* 연산자 우선 순위
* (optional) Java 13. switch 연산자

## 산술 연산자
1. + : 두개의 숫자를 더한다
2. - : 첫번째 피연산자 - 두번째 피연산자
3. * : 두개의 숫자를 곱한다
4. / : 첫번째 피연산자 / 두번째 피연산자
<br/>int / int -> return int, 나머지는 출력 x
<br/>ex) 7 / 3 return 2
<br/>두 피연산자 중 하나가 floating-point value이면 floating-point value로 return
<br/>ex) 7/ 3.0f return 2.33333f
5. % : 첫번째 피연산자 / 두번째 피연산자를 한 후 나머지 출력
<br/> 7 % 3 return 1

## 비트 연산자
1. ~ : 단항 연산자 ~는 bitwise complement(not) 1 -> 0, 0 -> 1
ex) ~12 : 00001100 -> 11110011
2. & : 각자 비트에 대해 boolean and
3. | : 각자 비트에 대해 boolean or
4. ^ : 각자 비트에 대해 boolean xor 같으면 0 다르면 1
5. << : left shift 숫자 * 2, 왼쪽으로 1칸씩 이동
6. '>>' : signed right shift 숫자 / 2, 오른쪽으로 1칸씩 이동 

## 관계 연산자
1. == : equals 두 피연산자가 같으면 true 다르면 false
<br/> primitive operand끼리는 서로 값이 같은지를 비교
<br/> reference type operand끼리는 same object or array를 가르키는지를 비교, 단순히 값이 같은가를 비교하는것이 아님
2. != : not equals
3. < : less than
4. <= : less than or equal
5. > : greater than
6. >= greater than or equal

## 논리 연산자
1. && : conditional and 두 operand가 모두 true이면 return true, 나머지 경우는 return false
<br/> 첫번째 opernad를 계산했을 때 false가 나오면 두번째 operand의 값에 관계없이 false이므로
<br/> 두번째 operand를 계산하지않고 넘어간다 따라서 side effect가 있는 식을 두번째 operand에 사용했으면 신경을 써야한다
2. || : conditional or 두 operand중 하나라도 true이면 return true, 둘 다 false이면 return false
<br/> &&와 마찬가지로 첫번째 operand 값이 true가 나오면 두번째 operand의 값에 상관없이 true이므로
<br/> 두번째 operand를 계산하지 않고 넘어간다
3. ! : boolean not true -> false, false -> true

## instanceof
left operand : object or array value, right operand : name of a reference type
<br/> object or array value가 오른쪽에 적힌 type과 일치하면 true, 다르면 false
<br/> left operand가 null이면 항상 false
## assignment(=) operator

## 화살표(->) 연산자
-> : lambda expression
<br/> (paramlist) -> {statenebts}

## 3항 연산자
( 조건문 ) ? 참 : 거짓 

## 연산자 우선 순위

## java 13 switch 연산자
자바 13 의 switch문에서는 기존의 case, break문을 case -> 문으로 작성할 수 있다
<br/> 또한 break대신 yield가 사용된다
```
public enum Day { SUNDAY, MONDAY, TUESDAY,
    WEDNESDAY, THURSDAY, FRIDAY, SATURDAY; }

// ... 변수 선언 + 변수 할당

    int numLetters = 0;
    Day day = Day.WEDNESDAY;
    switch (day) {
        case MONDAY:
        case FRIDAY:
        case SUNDAY:
            numLetters = 6;
            break;
        case TUESDAY:
            numLetters = 7;
            break;
        case THURSDAY:
        case SATURDAY:
            numLetters = 8;
            break;
        case WEDNESDAY:
            numLetters = 9;
            break;
        default:
            throw new IllegalStateException("Invalid day: " + day);
    }
    System.out.println(numLetters);
```
```
    Day day = Day.WEDNESDAY;    
    System.out.println(
        switch (day) {
            case MONDAY, FRIDAY, SUNDAY -> 6;
            case TUESDAY                -> 7;
            case THURSDAY, SATURDAY     -> 8;
            case WEDNESDAY              -> 9;
            default -> throw new IllegalStateException("Invalid day: " + day);
        }
    );    
```
``` 
// yield를 통해 선언과 할당을 한번에
    Day day = Day.WEDNESDAY;
    int numLetters = switch (day) {
        case MONDAY:
        case FRIDAY:
        case SUNDAY:
            System.out.println(6);
            yield 6;
        case TUESDAY:
            System.out.println(7);
            yield 7;
        case THURSDAY:
        case SATURDAY:
            System.out.println(8);
            yield 8;
        case WEDNESDAY:
            System.out.println(9);
            yield 9;
        default:
            throw new IllegalStateException("Invalid day: " + day);
    };
    System.out.println(numLetters);
 ```
 yield를 사용하게 switch문 자체에서 return이 가능해진다
 <br/> 기존의 break문을 사용하는 경우에는 먼저 변수를 설정하고 값을 할당하고 break를 해야했지만
 <br/> yield를 사용하게 되면 간단하게 처리를 할 수 있다
 
## side effects
일부 연산자들은 계산을 하게 되면 기존과 다른 결과를 가지게 되는 상태 변화를 일으킨다.
<br/> 이것을 side effect를 가지고 있다고 표현한다
<br/> 예를 들자면 ++ 연산자의 경우 ++a와 같이 사용되면 기존 a 의 값에 1을 더한 값을 가지게 된다
