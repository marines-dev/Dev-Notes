# [IDE] 디버깅(Debugging)

<br><br>

## **디버깅(Debugging)**

프로그램의 소스코드를 잘못 작성할 경우 문법적 오류(Syntax Error)와 논리적 오류(Semantic Error)가 발생할 수 있다. 

문법적 오류는 코드가 문법에 맞지 않아 발생하며, 컴파일 시점에 컴파일러가 이를 체크해주어 빌드가 되기 전에 쉽게 수정이 가능하다.

반면에, 논리적 오류는 프로그램에 버그(bug)가 있다는 의미다. 이 오류는 문법적으로는 문제가 없어서 빌드가 되지만, 논리적으로 문제가 되어 프로그램 실행 중에 오류가 발생하는 것이다. 이 경우 프로그래머는 소스코드를 일일이 검토하여 어느 부분에서 논리적 오류가 발생하고, 왜 잘못된 결과가 나오는지를 확인해야 하는데, 이 과정을 디버깅(Debugging)이라고 한다. 디버깅은 오류를 찾는 것 뿐만 아니라 프로그램이 올바르게 동작하는지 확인하는 용도로도 쓰인다.

※ 프로그램을 작성 혹은 실행하는 과정에서 오류가 발생한 경우 오류를 제거하기 위한 작업 과정을 디버깅(Debugging)이라고 한다.

<br><br>

## **디버거(Debugger)**

디버깅 작업은 어디서 잘못되었는지 코드를 하나하나 보면서 문제점을 찾아야하기 때문에 번거롭고 시간이 오래 걸린다. 

또한 프로그래머는 프로그램이 실행되면서 바뀌는 데이터 값을 전부 예상하고, 기억할 수 없기 때문에 코드만 보고 오류를 찾는 것은 쉽지 않다. 그래서 Visual studio 개발 도구는 디버깅을 좀더 편하게 할 수 있도록 ****디버거(Debugger)라는 도구를 추가로 제공한다.

<br><br>

## **디버거 사용법**

**디버그 모드와 릴리즈 모드**

- 디버그 모드 : 디버그 모드로 설정해야 디버그를 실행할 수 있다. 그래서 프로그래머는 디버그 모드인 상태에서 프로그램을 만든다.
- 릴리즈 모드 : 프로그램을 완성한 후 배포는 릴리즈 모드로 한다.

![https://blog.kakaocdn.net/dn/dcTImt/btqxPd1mhEF/wi3j49rKp1Z5TjmM0HudV1/img.png](https://blog.kakaocdn.net/dn/dcTImt/btqxPd1mhEF/wi3j49rKp1Z5TjmM0HudV1/img.png)

<br><br>
<br><br>

**디버깅 단축키**

1. 중단점 (Break pointer)

디버그 모드에서 실행을 시작할 할 라인을 선택 후 [F9]를 누르면 중단점이 걸리게 된다.

아니면 해당 라인 앞부분을 클릭을 해서 중단점을 설정할 수도 있다.

![https://blog.kakaocdn.net/dn/zeNKr/btqxM6a6fDD/Kkxib9s2BfKoCJ0ihz77Nk/img.png](https://blog.kakaocdn.net/dn/zeNKr/btqxM6a6fDD/Kkxib9s2BfKoCJ0ihz77Nk/img.png)

<br><br>

2. 디버그 모드 시작

중단점이 걸려 있으면 [F5]를 눌러 중단점 라인부터 디버그 모드를 실행한다. 이때 중단점 라인이 실행하기 전 대기 상태로 시작하게 되는 것이다. [F10]과  [F11]로도 디버깅 모드를 시작할 수 있다. 이때는 코드에 중단점이 걸려 있어도 무조건 프로그램 시작 단계부터 실행된다.

<br><br>

3. 디버깅 실행

디버그 모드 상태에서 [F10]은 프로시저 단위(함수 단위)로 실행 하고, [F11]은 한 단계씩 코드(명령문 단위)를 실행한다.  함수 단위가 없을 경우에는 [F10]으로도 한 단계씩 이동할 수 있다.

![https://blog.kakaocdn.net/dn/bJjRVn/btqxPSpmiqq/7xBSK5nufU2TcEREP1kR6k/img.png](https://blog.kakaocdn.net/dn/bJjRVn/btqxPSpmiqq/7xBSK5nufU2TcEREP1kR6k/img.png)

<br><br>

4. [Shift]+[F11]

콘솔에 소스코드를 출력한다.

<br><br>

5. 디버깅 모드 종료

디버깅 모드에서 [F5]나 [Shift] + [F5]를 눌러 중지할 수 있으며, 코드를 끝까지 실행하면 자동으로 종료된다.

<br><br>

> **디버그 모드시 주의점**
> 
> - 작성한 프로젝트의 빌드가 무조건 성공을 해야 디버깅 모드를 실행할 수 있다.
> - 디버그 모드 실행 중에 내용을 편집하지 않는다.
>     - 디버그 모드 실행 중에 내용을 편집하면 실행한 빌드와 내용이 달라지기 때문에 처음부터 다시 빌드를 하게 되어 큰 프로그램 일 경우 엄청 느리게 빌드가 된다. 만약 코드를 수정할 경우 디버그 모드를 멈추고 다시 빌드해야 하며, 코드를 실수로 편집할 경우에는 ****[Ctrl] + Z ****로 돌려준다.
> - 중단점 위치를 되돌리지 않는다.
>     - 디버그 모드는 되돌리는 기능이 없기 때문에 중단점 위치를 이전으로 변경해도 실행을 되돌아가는 것이 아니라 다시 재실행되어 값이 변하게 된다.

<br><br>

**예제1) 디버깅하기**

1. 논리적 오류 발생

원치않는 값이 출력된다.

![https://blog.kakaocdn.net/dn/G1z0u/btqxPc89UWC/j2mZdMAvAyVz0KFXcNTHq0/img.png](https://blog.kakaocdn.net/dn/G1z0u/btqxPc89UWC/j2mZdMAvAyVz0KFXcNTHq0/img.png)

![https://blog.kakaocdn.net/dn/blN5uE/btqxMtK3y3Q/YzLFp5ybL6Rm6yAYa03fW0/img.png](https://blog.kakaocdn.net/dn/blN5uE/btqxMtK3y3Q/YzLFp5ybL6Rm6yAYa03fW0/img.png)

<br><br>

2. 디버그 모드 시작 : [F10] or [F11]

디버그 모드에서 ****[F11]을 눌러서 한 단계씩 중단점 이동을 시작한다.

![https://blog.kakaocdn.net/dn/viQcg/btqxShuJ3s9/jPrpgMo8bDEX8CYRaimIHK/img.png](https://blog.kakaocdn.net/dn/viQcg/btqxShuJ3s9/jPrpgMo8bDEX8CYRaimIHK/img.png)

<br><br>

3. 중단점 이동

중단점을 한 단계 이동하면 **nData = 5;** 라인에 중단점이 오게 된다.

이때 아래의 자동 페이지를 보면 nData의 초기값이 **쓰레기 값**인 것을 알 수 있다.

왜냐하면 아직 중단점 라인이 실행된 것이 아니라 nData의 변수만 선언되어 있는 상태이기 때문이다.

![https://blog.kakaocdn.net/dn/KqeQm/btqxNVAn3qh/nemZBMj2szYK0jZAh4x1TK/img.png](https://blog.kakaocdn.net/dn/KqeQm/btqxNVAn3qh/nemZBMj2szYK0jZAh4x1TK/img.png)

<br><br>

4. 자동 페이지에서 실행된 변수의 값 확인하기

자동 페이지는 **실행되는** 변수의 값을 확인할 수 있는 페이지다.

다음 라인으로 중단점을 이동했더니 그때서야 nData값이 **5**로 초기화되는 것을 확인할 수 있다.

![https://blog.kakaocdn.net/dn/bcevlY/btqxN4RpkgO/KgJZlSb9R7tknVkswaK7uK/img.png](https://blog.kakaocdn.net/dn/bcevlY/btqxN4RpkgO/KgJZlSb9R7tknVkswaK7uK/img.png)

<br><br>

5. 논리적 오류가 발생한 이유를 확인할 수 있다.

프로그래머는 if문을 실행시키지 않을 의도 였는데 중단점이 if문 안으로 이동한 것을 확인할 수 있다.

뿐만 아니라 자동 페이지를 보면 if 조건문이 실행되면서 nData 값이 **10**으로 변경되는 것을 알 수 있다.

여기서 if 조건문이 nData 값을 비교하는 것이 아닌 **대입**이 되었다는 것을 알 수 있어야 한다.

![https://blog.kakaocdn.net/dn/cilgbg/btqxQTgRerU/n9dnPb7ZiexIuKf4CjJ5b1/img.png](https://blog.kakaocdn.net/dn/cilgbg/btqxQTgRerU/n9dnPb7ZiexIuKf4CjJ5b1/img.png)

<br><br>

6. 콘솔에 값 출력

중단점을 다음 단계로 이동하고 if문의 printf() 구문이 실행되어 이때 콘솔에 값이 출력되는 것을 확인할 수 있다.

![https://blog.kakaocdn.net/dn/bZHvTt/btqxNUasbZF/TcE8fSKRExdpWiPKdV18dk/img.png](https://blog.kakaocdn.net/dn/bZHvTt/btqxNUasbZF/TcE8fSKRExdpWiPKdV18dk/img.png)

![https://blog.kakaocdn.net/dn/mGJvE/btqxNUO5yzk/V80cfKRFKUZx2JnrYWPM9K/img.png](https://blog.kakaocdn.net/dn/mGJvE/btqxNUO5yzk/V80cfKRFKUZx2JnrYWPM9K/img.png)

<br><br>

7. 디버그 모드 종료

중단점을 다음 단계로 이동하여 마지막 라인에 대기하게 되고 다시 한번 더 이동하면 자동으로 디버그 모드가

종료된다.

![https://blog.kakaocdn.net/dn/bpX71n/btqxQU1eMPX/5BVKKbdCZwbqF32RDoK3UK/img.png](https://blog.kakaocdn.net/dn/bpX71n/btqxQU1eMPX/5BVKKbdCZwbqF32RDoK3UK/img.png)

![https://blog.kakaocdn.net/dn/3TGrM/btqxSgWYAYM/N2WWlpJHVBfWO46Ia1BUQ0/img.png](https://blog.kakaocdn.net/dn/3TGrM/btqxSgWYAYM/N2WWlpJHVBfWO46Ia1BUQ0/img.png)

<br><br>
<br><br>

**변수 값 확인하기**

- 자동 : 데이터가 실행되면 자동으로 데이터 값이 나온다. 점검을 자세하게 하기 위해서 자동은 거의 사용하지 않는다.

![https://blog.kakaocdn.net/dn/biUsHD/btqxNUuQ7cw/fpOI9ua6F5RSOnQKsB0c7K/img.png](https://blog.kakaocdn.net/dn/biUsHD/btqxNUuQ7cw/fpOI9ua6F5RSOnQKsB0c7K/img.png)

- 조사식 : 변수가 많거나 특정 변수를 확인하고 싶을 경우 자동으로는 변수를 일일이 확인하기 어렵기 때문에 원하는 변수를 조사식에 추가해서 조사식 페이지에서 실행 값을 확인할 수 있다.

![https://blog.kakaocdn.net/dn/6LiOm/btqxOIAFiYM/pC6Z3bMjK7IdvKUY1rMchk/img.png](https://blog.kakaocdn.net/dn/6LiOm/btqxOIAFiYM/pC6Z3bMjK7IdvKUY1rMchk/img.png)

<br><br>
<br><br>

**중단점 세부 설정**

중단점을 세부 설정해서 좀 더 간편하게 디버깅하는 방법도 있다.

![https://blog.kakaocdn.net/dn/UWu0s/btqxQqe1P7q/MX8mbJkjKkEPA44he6Qqp1/img.png](https://blog.kakaocdn.net/dn/UWu0s/btqxQqe1P7q/MX8mbJkjKkEPA44he6Qqp1/img.png)

디버그 모드를 실행한 후 for반복문에서 **i**를 0부터 50까지 한 단계 한 단계식 실행하는 것은 번거롭고 시간이 오래

걸린다.

![https://blog.kakaocdn.net/dn/pHcBA/btqxPdf8U09/oWVAdIfgL46KFHMNcnJv21/img.png](https://blog.kakaocdn.net/dn/pHcBA/btqxPdf8U09/oWVAdIfgL46KFHMNcnJv21/img.png)

이렇게 중단점을 한 번씩 이동하기 불편할 경우 중단점에 조건을 설정할 수 있다.

그러면 i == 40인 조건에서부터 실행할 수 있다.

![https://blog.kakaocdn.net/dn/5RU4l/btqxPc2CNxj/YKNb98E2SG9WNj4j0s5850/img.png](https://blog.kakaocdn.net/dn/5RU4l/btqxPc2CNxj/YKNb98E2SG9WNj4j0s5850/img.png)

![https://blog.kakaocdn.net/dn/dJjTPc/btqxOH9Fmzo/Tuqx9lWWv3oXzZCX2DO8xK/img.png](https://blog.kakaocdn.net/dn/dJjTPc/btqxOH9Fmzo/Tuqx9lWWv3oXzZCX2DO8xK/img.png)

<br><br>
<br><br>

**호출 스택**

호출 스택에서는 중단점이 함수 안으로 들어왔을 때 어느 위치에서 어떤 함수가 호출된 것인지 알 수 있다.

![https://blog.kakaocdn.net/dn/WJ82E/btqxQp8eVjd/LrSNfUk7gVOu0LDw84yWgK/img.png](https://blog.kakaocdn.net/dn/WJ82E/btqxQp8eVjd/LrSNfUk7gVOu0LDw84yWgK/img.png)

![https://blog.kakaocdn.net/dn/92d2Q/btqxRuuuQsm/SPbIKGhVeSlGC3pntjCGu0/img.png](https://blog.kakaocdn.net/dn/92d2Q/btqxRuuuQsm/SPbIKGhVeSlGC3pntjCGu0/img.png)

---
