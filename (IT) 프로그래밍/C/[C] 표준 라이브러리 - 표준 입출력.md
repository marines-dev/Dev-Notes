# [C] 표준 라이브러리 : 표준 입출력

<br><br>

## 표준 입출력 라이브러리(Standard I/O Library)

C언어는 운영체제와 보조기억 장치의 종류에 상관없이 보조기억 장치에 파일 입∙출력, 저장 등 사용할 수 있도록 파일 입출력 라이브러리를 제공하는데, 많은 운영체제에서 이 라이브러리를 호환한다. 

표준 입출력 라이브러리는 데이터 형식에 따라 다른 함수를 제공한다. 프로그램이 사용하는 데이터 형식은 텍스트와 바이너리로 나누어지는데, 데이터 형식에 따라 관련 함수를 사용해야 한다.

- 헤더 파일 : stdio.h

<br><br>
<br><br>

## 표준 출력 함수

표준 출력이란 가장 기본으로 사용하는 출력 방식으로, 시스템 마다 출력 장치의 표준 출력이 다르다. C언어에서는 가장 기본적으로 사용하는 표준 출력 함수를 제공한다.

ex) 컴퓨터의 표준 출력은 ‘모니터’이다.

<br><br>

**단일 문자 출력하기**

단일 문자를 작성하여 문자를 출력하고, 실패하면 -1을 반환한다. 이때, putc()는 여러 가지 형식을 출력할 수 있는데, stream 매개변수에 표준 출력을 의미하는 stdout 값을 사용해야 한다. putchar()은 putc()의 stdout을 생략하여 편리하게 사용할 수 있도록 만들어진 매크로 함수이다.

- 함수원형 : int putc( int ch, FILE *stream )
- 함수원형 : int putchar( int ch );

ex) putchar(’A’);

<br><br>
<br><br>

**단일 문자열 출력하기**

단일 문자열을 작성하여 문자열을 출력하는데, puts()는 문자열을 출력하고 줄 바꿈을 하기 때문에 캐럿이 다음 줄로 이동한다.

- 함수 원형 : int puts( const char *str );

<br><br>
<br><br>

**문자열 출력하기**

printf()는 문자열 뿐만 아니라 변수의 값을  원하는 형식으로 출력할 수 있으며, % 서식 지정 키워드를 사용하여 변수의 갯수의 짝을 맞춰서 원하는 개수만큼 명시할 수 있다.

- 함수 원형 : int printf( const char *format, ... );

<br><br>

>[!note]
> **% 서식 지정자 키워드**
> 
> - %d(정수), %f(실수), %c(문자), %s(문자열) 등
> - 서식 키워드 참고용 사이트
> [https://en.cppreference.com/w/c/io/fprintf](https://en.cppreference.com/w/c/io/fprintf)

<br><br>

>[!note]
> **제어 코드**
> 
> - \n(다음줄로 이동), \r(해당 줄 처음으로 이동), \t(한 탭 이동), \'(작은 따옴표), \"(큰 따옴표) 등

<br><br>
<br><br>

## 표준 입력 함수

표준 입력 장치는 시스템에서 가장 기본적인 입력 수단 장치이다. C언어는 표준 입력 장치로부터 데이터를 입력 받는 표준 입력 함수를 제공한다. 운영체제는 표준 입력을 사용하는 시스템을 위해 표준 입력 버퍼라는 별도의 메모리를 제공하는데, 입력되는 값들을 하나씩 처리하지 않고 입력 버퍼에 임시로 저장했다가 일정한 조건이 되면 처리하여 효과적으로 처리한다. 그런데 단일 문자를 입력 받는 표준 입력 함수는 여러 개의 값을 입력 후 특정키를 누르면 입력 버퍼에 문자가 남게되는데, 다음에 호출하는 표준 입력 함수에 영향을 미치므로 주의해야 한다. 그러므로 입력을 구별하고 싶다면 rewind()를 사용해 입력 버퍼를 초기화해야 안전하다.

ex) 컴퓨터의 키보드는 입력 완료를 의미하는 [Enter]키를 누를 때까지 해당 함수가 완료되지 않는다.

<br><br>

>[!note]
> **rewind()**
> 
> 입력 버퍼에 남아있는 입력 정보를 모두 지우고 싶을 때 입력 버퍼의 데이터를 초기화하는 함수이다. *stream 매개변수로 stdin 포인터를 넣으면 장치에서 입력한 값을 얻을 수 있다.
> 
> - 함수 원형 : void rewind( [FILE](http://en.cppreference.com/w/c/io) *stream );

<br><br>

**단일 문자 입력하기**

단일 문자를 입력 받는다.  확장키 값(F1이나 특수키 등)을 받기 위해서 int형식으로 데이터를 반환하는게 일반적이지만 char형 변수로 받을 수 있다. getc()는 stream 매개변수에 표준 입력을 의미하는 stdin 값을 사용하면 입력 장치에서 입력을 받아 문자를 한 개씩 출력할 수 있다. 이렇게 getc()에 stdin을 계속 인자로 넘기는 것이 불편하기 때문에 매크로 함수로 getchar()을 재정의 해놓은 것이다.

- 함수 원형 : int getchar(void);
- 함수 원형 : int getc( [FILE](https://en.cppreference.com/w/c/io/FILE) *stream );

<br><br>

**예제1) getchar() 함수를 사용하여 문자 입력 받기**

```c
#include <stdio.h>
 
int main()
{
    int c = 0;
    c = getchar();
    printf("Input : %c\n", c);
    return 0;
}
```

![https://blog.kakaocdn.net/dn/bANX2y/btqxC5CCaH6/Kel6L7umjsY5QG7LvEbSOK/img.png](https://blog.kakaocdn.net/dn/bANX2y/btqxC5CCaH6/Kel6L7umjsY5QG7LvEbSOK/img.png)

<br><br>

**예제2) getchar() 함수를 사용하여 문자 두번 입력 받기**

```c
//'a'만 입력하고 [Enter]키를 눌렀을 때 첫번째 입력 받을 때
//함께 입력된 [Enter]키의 값을 문자(아스키코드:10, '\n')로 받게되어
//getchar()이 한꺼번에 동작해 두번 째 입력에서 줄바꿈을 하게 되고 입력 값을 받지 못하고 종료하게 된다.
#include <stdio.h>
 
int main()
{
    int c = 0;
    c = getchar();
    printf("First input : %c\n", c);
    c = getchar();
    printf("Second input : %c\n", c);
 
    return 0;
}
```
![%5BC%5D%20표준%20라이브러리%20-%20표준%20입출력](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BC%5D%20표준%20라이브러리%20-%20표준%20입출력.png)

<br><br>

**예제3) getchar() 함수로 문자를 입력 받고 표준 입력 버퍼 초기화하기**

```c
#include <stdio.h>
 
int main()
{
    int c = getchar(); 
    rewind(stdin);
    printf("First input : %c\n", c);
    c = getchar();
    rewind(stdin);
    printf("Second input : %c\n", c);

    return 0;
}
```

![https://blog.kakaocdn.net/dn/sshIy/btqxBQ0t9HM/K14182IE0JmsUFnIsM2IW1/img.png](https://blog.kakaocdn.net/dn/sshIy/btqxBQ0t9HM/K14182IE0JmsUFnIsM2IW1/img.png)

<br><br>
<br><br>

**단일 문자열 입력받기**

단일 문자열을 입력 받는다. 한번에 여러 개의 문자를 입력 받을 수 있으며 [Enter]키를 입력할 때까지 입력한 모든 문자를 하나의 문자열로 간주한다. gets()는 [Enter]키는 입력 완료의 기준으로만 사용하기 때문에 문자열에 포함시키지 않고 [Enter]키를 입력한 위치에 0(NULL문자)이 들어간다. fgets()는 파일에서 데이터를 읽어오는데, *stream 매개변수의 표준 입력 장치인 stdin을 사용하면 입력 버퍼에서 문자열을 받아올 수 있게 되는데, gets()와 함께 동작하게 된다. gets()가 정의되지 않다는 컴파일 오류가 발생하면 fgets()을 사용하면 된다.

- 함수 원형 : char *gets( char *str );
- 함수 원형 : char *fgets( char *str, int count, [FILE](https://en.cppreference.com/w/c/io/FILE) *stream );

<br><br>

>[!note]
> **gets() 사용시 주의점**
> 
> 입력을 받는 중에 [Ctrl] + [C]키를 누르면 표준 입력이 취소되고 프로그램이 중지되는데, 이때, 입력 취소를 처리하지 않을 경우 문자열에 복사되지 않은 상태로 gets()가 종료되어 이상한 값이 출력된다. 그러므로 gets()의 반환 값은 사용자 입력이 정상적으로 완료되지 않으면 null값을 반환하기 때문에 사용자가 정상적으로 입력을 완료하지 않은 상황에 대처하는 코드를 구성할 수 있어야 한다.

<br><br>

**예제4) fgets() 함수로 문자열을 입력 받다가 입력 취소 처리하기**

```c
#include <stdio.h>
 
int main()
{
    char str[10] = {};
    
    if (null != fgets(str,10,stdin)) 
    {
        printf("input : %s\n", str);
    }
    else
    {   
        printf("\ninput -> Canceled\n");
    }

    return 0;
}
```

![https://blog.kakaocdn.net/dn/wEbwV/btqxDtwsXPD/KRSnjOECSyFuU6iHrfMTYk/img.png](https://blog.kakaocdn.net/dn/wEbwV/btqxDtwsXPD/KRSnjOECSyFuU6iHrfMTYk/img.png)

<br><br>

**예제5) gets() 함수 직접 구현하기**

```c
#include <stdio.h>

bool GetString(char * cBuffer, int nLimit)
{
    int i = 0;
    for (i = 0; i < nLimit; ++i) 
    {
        cBuffer[i] = getchar(); 
        if (cBuffer[i] == '\n')
        {
            cBuffer[i] = '\0'; 
            return true; 
        }
    }
    cBuffer[i] = '\0'; 
    rewind(stdin); 
    return false;
}
```

<br><br>
<br><br>

**문자열 입력하기**

scanf()는 서식 지정자 키워드를 사용하여 문자, 문자열 뿐만 아니라 모든 형식을 받을 수 있도록 입력을 제공한다. 

한 번의 함수 호출로 여러 개의 값을 동시에 입력 받기 위해서 포인터에 &연산자로 변수의 주소를 저장하여 입력 값을 받는다. 서식 키워드(%)에 맞게 변수의 주소를 넘겨주어 입력 후 [Enter]키를 누르면  해당 변수에 입력 값을 저장한다. 한 번에 여러 개의 데이터를 입력할 때도 [Enter], [spase] (공백) 키로도 입력의 구별이 가능한데, 주의할 점은 %s키워드를 사용하여 문자열을 입력할 때 중간에 공백이 들어가면, 첫 번째 공백까지만 출력하고 나머지는 문자들은 입력 버퍼에 그대로 남게 되어 다음 표준 입력 함수에 영향을 주게 된다. 그러므로 입력할 문자열에 공백이 포함된다면 scanf() 대신에 gets()를 사용하자. 또한 잘못된 입력으로 scanf()가 실패했을 때 입력 버퍼에 저장되어 있는 값들은 rewind()로 입력 버퍼를 비워야 무한 출력이 되지 않는다. 입력 오류를 정확하게 처리하기 위해서 데이터를 입력 받기 전, 후에 rewind() 함수를 적절하게 사용하여 표준 입력 버퍼를 비우는 것이 좋다.

- 함수원형 : int scanf( const char *format, ... );

<br><br>

**예제6) scanf() 함수로 값 입력하기**

```c
#include <stdio.h>

int main()
{
    int nData = 0;
    float fData = 0;
 
    scanf_s("%d %f", &nData, &fdata);
    scanf_s("%f", &fData);
 
    printf("input : %d, %f\n", nData, fData);
    return 0;
}
```
