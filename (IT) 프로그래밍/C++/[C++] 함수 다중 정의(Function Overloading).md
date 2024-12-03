# [C++] 함수 다중 정의(Function Overloading)

<br><br>

# 함수 다중 정의(Function Overloading)

C++은 함수 원형이 다른 동일한 이름의 함수를 다중으로 정의하여 사용할 수 있는데, 이때 주의할 점은 함수 원형의 매개변수(자료형, 개수)가 다를 경우에만 정의할 수 있으며, 함수의 반환형으로는 구분할 수 없다.

ex) int OverloadFunc (int nParam);

int OverloadFunc (int nParam1, int nParam2 );

int OverloadFunc (char cParam);

int OverloadFunc (char cParam1, char cParam2);

int OverloadFunc (int nParam, char cParam);

void OverloadFunc (int nParam);  //(X)

int OverloadFunc (int nParam);  //(X)

char OverloadFunc (int nParam); //(X)

<br><br>

**예제1) 함수 다중 정의하기**

```cpp
#include <stdio.h>

void OverloadFunc()
{
    printf("void OverloadFunc();\n");
}
 
void OverloadFunc(int _n)
{
    printf("void OverloadFunc(%d);\n",_n);
}
 
void OverloadFunc(int _n1, int _n2)
{
    printf("void OverloadFunc(%d, %d);\n", _n1, _n2);
}

void OverloadFunc(char _c)
{
    printf("void OverloadFunc(%c);\n", _c);
}

int main()
{
    OverloadFunc(); //void OverloadFunc()
    OverloadFunc('a'); //void OverloadFunc(char) 
    OverloadFunc(8); //void OverloadFunc(int)
    OverloadFunc(20,35); //void OverloadFunc(int, int)
    return 0;
}
```

![https://blog.kakaocdn.net/dn/b9PaMn/btqxHAVPJC5/5umAFoZVUByHswktrvFoj1/img.png](https://blog.kakaocdn.net/dn/b9PaMn/btqxHAVPJC5/5umAFoZVUByHswktrvFoj1/img.png)
