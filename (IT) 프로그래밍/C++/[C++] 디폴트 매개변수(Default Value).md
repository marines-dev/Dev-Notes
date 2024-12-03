# [C++] 디폴트 매개변수(Default Value)

# 디폴트 매개변수(Default Value)

C++ 함수의 매개변수는 디폴트 값을 설정할 수 있는데, 함수를 호출할 때 디폴트 매개변수에 인자를 작성하지 않으면 디폴트 값으로 초기화된다. 디폴트 매개변수 사용 시 주의할 점은 함수의 인자는 첫번째 값부터 순서대로 저장되기 때문에 디폴트 매개변수는 첫번째부터 순서대로 설정해야 한다. 함수 원형을 선언할 경우 디폴트 매개변수는 함수 원형에만 설정해야 한다.

함수 오버로딩과 디폴트 매개변수가 섞일 경우 호출이 모호해져 컴파일 에러가 발생할 수 있기 때문에 섞어서 사용하지 않도록 하자.

- 사용 형식 : *자료형 함수이름* (*자료형 변수이름* = *디폴트값*, *..*);

**예제1) 디폴트 매개변수 사용하기**

```cpp
#include <stdio.h>
int TestFuncOne(int _n = 5);
int TestFuncTwo(int _n1 = 3, int _n2 = 7);
 
int main()
{
    printf("TestFuncOne() = %d\n", TestFuncOne());
    printf("TestFuncTwo() = %d\n", TestFuncTwo());
    printf("TestFuncTwo(10) = %d\n", TestFuncTwo(10));
    printf("TestFuncTwo(20,30) = %d\n", TestFuncTwo(20,30));
    return 0;
}
 
int TestFuncOne(int _n)
{
    return _n;
}
 
int TestFuncTwo(int _n1, int _n2)
{
    return _n1 + _n2;
}
```

![https://blog.kakaocdn.net/dn/bnKNgV/btqxHsX0oTV/9YA3QNE19C9kglkXluZgj1/img.png](https://blog.kakaocdn.net/dn/bnKNgV/btqxHsX0oTV/9YA3QNE19C9kglkXluZgj1/img.png)

**예제2) 디폴트 매개변수 사용 시 주의할 점**

```cpp
#include <stdio.h>
int TestFunc(int _n1, int _n2 = 10, int _n3 = 10); //함수 호출 인자는 첫번째부터 설정해야 한다.
//int TestFunc(int _n1 = 10, int _n2 = 10, int _n3); //오버로딩된 함수 호출 시 디폴트 매개변수의 값이 모호해진다.
 
int main()
{
    printf("TestFunc(30, 30, 30) = %d\n",TestFunc(30,30,30));
    printf("TestFunc(20, 20, default) = %d\n", TestFunc(20, 20));
    printf("TestFunc(10, default, default) = %d\n", TestFunc(10));
    return 0;
}
 
int TestFunc(int _n1, int _n2, int _n3)
{
    return _n1 +_n2 +_n3 ;
}
```

![https://blog.kakaocdn.net/dn/I1ggA/btqxG77EVOk/IKaQXvdk8MkH2LiXCMzkx1/img.png](https://blog.kakaocdn.net/dn/I1ggA/btqxG77EVOk/IKaQXvdk8MkH2LiXCMzkx1/img.png)