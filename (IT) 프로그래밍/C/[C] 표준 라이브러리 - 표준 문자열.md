# [C] 표준 라이브러리 : 표준 문자열

<br><br>

## **표준 문자열**

문자열은 프로그램에서 자주 사용되기 때문에 C언어에서 표준 문자열 라이브러리를 헤더 파일로 제공하며 자주 사용하는 표준 문자열 함수로는 strlen(), strcpy(), strcat() 등이 있다.

- 헤더 파일 : string.h

<br><br>
<br><br>

## 자주 사용하는 문자열 함수

**문자열 길이 구하기**

- [size_t](https://en.cppreference.com/w/c/types/size_t) strlen( const char *str );

<br><br>

**예제1) strlen() 함수 사용하여 문자열 길이 구하기**

```c
#include <stdio.h>
#include <string.h>
 
int main()
{
    const char *str = "banana"; //포인터 문자열 선언 시 const 필수
    printf("banana의 길이 = %d\n", strlen(str));
 
    return 0;
}
```

<br><br>

**예제2) ‘문자열 길이 구하기’ 함수 직접 구현하기**

```c

int Strlen(const char * str)
{
    int count = 0;
 
    while (str[count ] != 0)
    {
        count ++;
    }
    return count ;
}
```

<br><br>

**문자열 복사하기**

- char *strncpy( char *dest, const char *src, [size_t](https://en.cppreference.com/w/c/types/size_t) count );

<br><br>

**예제3) strSrc() 함수 사용하여 문자열 복사하기**

```c
#include <stdio.h>
#include <string.h>
 
int main()
{
    char strDest[20];
    char strSrc[20] = "pineapple";
    strcpy(strDest, strSrc, 20);
    printf("%s\n", cDest);
 
    return 0;
}
```

<br><br>

**예제4) ‘문자열 복사하기’ 함수 직접 구현하기**

```c
//함수 만들기 : 문자열 복사하기
char *Strcpy(char *strDest, const char *strSrc, size_t strDestsz)
{
    char *p = strDest;
    while (*strSrc && (--strDestsz> 0)) 
        *strDest++ = *strSrc++; 
    *strDest= 0;

    return p;
}
```

<br><br>

**문자열 연결하기**

- char *strcat( char *dest, const char *src );

<br><br>

**예제5) strDest() 함수 사용하여 문자열 연결하기**

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char strDest[10] = "Nice to ";
    const char *strSrc = "meet you";
    strcat(strDest, strSrc); 
    printf("%s\n", cDest);
    
    return 0;
}
```

<br><br>

**예제6) ‘문자열 연결하기’ 함수 직접 구현하기**

```c
//함수 만들기 : 문자열 연결하기
char * Strcat(char *strDest, const char *strSrc, size_t strDestsz)
{
    char *pDest = strDest;
    while (*strDest&& (--strDestsz> 0))
        strDest++;
    while (*strSrc&& (--strDestsz> 0))
        *strDest++ = *strSrc++;
    *strDest = 0;

    return pDest;
}
```

<br><br>

>[!note]
> **문자열을 정수로 변환하기**
> 
> atoi() 함수를 사용하여 숫자형 문자를 정수로 변환할 수 있다.
> 
> - 헤더 파일 : stdlib.h
> - 함수 원형 : int atoi( const char *str );
