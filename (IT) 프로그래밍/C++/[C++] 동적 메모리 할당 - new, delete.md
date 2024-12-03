# [C++] 동적 메모리 할당 : new, delete

# 동적 메모리 할당

프로그램 실행 중에 필요한 데이터를 힙 메모리에 할당하고 해제할 수 있다.

C++의 new, delete 연산자는 C언어의 malloc(), free() 함수가 보완되서 나온 동적 할당 방법이다.

new, delet 연산자로 동적 할당 시 사용 시 C++에서 직접 연산을 하기 때문에 C언어처럼 헤더 파일을 추가할 필요가 없으며, 메모리 크기가 자료형으로 결정되므로 메모리의 크기를 직접 전달하지 않아도 되고, 형 변환을 하지 않아도 되며, 메모리 할당과 동시에 초기화도 가능하여 전체적으로 C언어 동적 할당 함수보다 사용하기가 편리하다. 그리고 C++에서 new, delete 연산자를 사용해야만 하는 이유는 클래스로 동적 할당하여 객체를 생성할 경우 new는 자동으로 생성자를 호출하고, 객체를 해제할 경우 delete는 자동으로 소멸자를 호출하기 때문이다. 그러므로 클래스로 동적 할당하여 객체를 생성할 경우에는 new, delete 연산자를 사용해야만 한다.

### **new, delete**

- 사용 방법

```cpp
*자료형* * *변수이름* = new *자료형*; //동적 할당
delete *변수이름*; //해제
```

- 배열 사용 방법

```cpp
*자료형* * *포인터* = new *자료형* [*요소개수*] //배열로 동적 할당
delete [] *포인터*; //해제
```

**예제1) new, delete 연산자로 동적 할당하기**

```cpp
#include <stdio.h>
 
int main()
{
    int *p = new int(0); //int형 메모리를 동적 할당하고 0으로 초기화함.
    *p = 30;
 
    delete p ; //new로 동적 할당한 메모리는 반드시 delete로 해제해야 한다.
    
    return 0;
}
```

**예제2) new, delete 연산자로 동적 할당하여 배열로 생성하기**

```cpp
#include <stdio.h>
 
int main()
{
    int *p_arr = new int[10]{}; //int형 메모리 10개를 동적 할당하고 0으로 초기화'{}'함.
    for (int i = 0; i < 10; ++i)
        p_arr[i] = i + 1;
 
    delete[] p_arr; //배열 형태로 생성한 메모리는 배열 형태로 해제해야 한다.
    
    return 0;
}
```

**예제3) new, delete 연산자로 동적 할당하여 객체 생성하기**

```cpp
#include <stdio.h>
#include <stdlib.h>

class C_DYNAMIC_ALLOCATION
{
public:
    C_DYNAMIC_ALLOCATION()
    {
        printf(" → [Constructor] : Dynamic memory allocation\n");
    }
 
    ~C_DYNAMIC_ALLOCATION()
    {
        printf(" → [Destructor] : Dynamic memory deleting\n");
    }
};
 
int main()
{
    printf("(1) Dynamic memory allocation of object witn new\n");
    C_DYNAMIC_ALLOCATION * cpDynamicAllocation1 = new C_DYNAMIC_ALLOCATION; //new를 사용하여 객체를 동적 할당함.
    printf("----------------------------------------------------- \n");
 
    printf("(2) Dynamic memory allocation of object witn malloc()\n");
    C_DYNAMIC_ALLOCATION * cpDynamicAllocation2 = (C_DYNAMIC_ALLOCATION *)malloc(sizeof(C_DYNAMIC_ALLOCATION) * 1); //malloc()을 사용하여 객체를 동적 할당함.
    printf("----------------------------------------------------- \n");
 
    printf("(3) Dynamic memory deleting of object witn delete\n");
    delete cpDynamicAllocation1; //delete를 사용하여 객체를 해제함.
    printf("----------------------------------------------------- \n");
 
    printf("(4) Dynamic memory deleting of object witn free()\n");
    free(cpDynamicAllocation2); //free()를 사용하여 객체를 해제함.
    printf("----------------------------------------------------- \n");
 
    return 0;
}
```

![https://blog.kakaocdn.net/dn/bfZzEp/btqxHswYxp5/N8kAjCI2uQnK21keiu1p70/img.png](https://blog.kakaocdn.net/dn/bfZzEp/btqxHswYxp5/N8kAjCI2uQnK21keiu1p70/img.png)