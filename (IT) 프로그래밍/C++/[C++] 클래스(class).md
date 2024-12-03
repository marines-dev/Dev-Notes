# [C++] 클래스(class)

<br><br>

## 객체지향 프로그래밍

객체지향 프로그래밍에서 객체는 데이터(변수)와 기능(함수)으로 구성되는데, 대표적으로 클래스가 있다.

C언어는 작업 순서가 절차적으로 진행되는 절차지향 특징인 반면에 C++의 객체지향 특징은 객체를 실체화시켜서 제작자와 사용자를 분리하여 사용하는 형태의 프로그래밍이다.

<br><br>

**예제1) C++의 클래스를 이용한 객체지향 프로그래밍**

```cpp
#include <stdio.h>
struct INFORMATION
{
  char cName[50];
	int nAge = 0;
};
 
int main()
{
    INFORMATION information = { "Mrines", 26 };
    printf("My name is %s.\n", information.cName);
    printf("I'm %d years old.\n", information.nAge);
    return 0;
}
```

<br><br>
<br><br>

## 클래스(class)

클래스는 변수와 함수(메서드)를 하나의 틀로 모아 만든 새로운 자료형으로 객체지향의 캡슐화 특성이 있다. 

 C언어의 구조체 내부에 함수를 선언할 수 없다면 클래스는 내부에 함수를 선언할 수 있으며, 다양한 객체지향 특성의 기능들이 추가된 것이다.

<br><br>

**클래스 정의하기**

클래스를 정의하기 위한 클래스의 구성 요소이다.

- 접근 제어 지시자 : 클래스 멤버의 사용을 제한하는 기능이다.
    - public  : 멤버 객체에 대한 모든 외부 접근이 허용된다.
    - protected : 멤버객체에 관한 모든 외부 접근이 차단되는데, 상속한 자식 클래스에서의 접근은 허용한다.
    - private : 외부의 접근과 자식 클래스로부터의 접근까지 모두 차단되는데, 클래스에서 멤버를 선언할 때 별도로 접근 제어 지시자를 지정하지 않으면 기본적으로 private이다.
- 멤버 변수 : 클래스의 변수이다.
- 멤버 함수 : 클래스의 함수이다. 멤버 함수를 이용해 기능을 실행할 수 있으므로 메서드(방법)라고도 하며 사용자 코드에서 클래스 함수를 호출하여 내부의 기능을 연결하므로 인터페이스 함수라고도 한다.

>[!note]
> **상수형 멤버 함수**
>     
>     const 키워드를 이용하여 상수형 멤버 함수를 선언하면, 상수형 멤버 함수 내에서는 멤버 변수의 읽기만 가능하고, 상수화된 함수가 아니면 멤버 함수라도 호출할 수 없다.
>     
>     - 사용 형식 : *자료형 클래스이름*::*함수이름*() const;
>     
>     **예제2) 상수형 멤버 함수 사용하기**
>     
>     ```cpp
>     #include <stdio.h>
>     
>     class C_TEST
>     {
>     private:
>         int m_nData;
>         
>     public:
>         C_TEST():
>             m_nData(0)
>         {
>         }
>      
>         void SetData(int nParam)
>         {
>             m_nData = nParam;
>         }
>      
>         int GetData() const
>         {
>             //m_nData = 10; //오류 발생 : 'm_nData'는 const 객체를 통해 액세스되고 있으므로 수정할 수 없습니다.
>             //SetData(3); //오류 발생 : 'this' 포인터를 'const C_TEST'에서 'C_TEST &'(으)로 변환할 수 없습니다.
>      
>             return m_nData; //멤버 변수의 값을 읽을 수 있다.
>         }
>     };
>      
>     int main()
>     {
>         C_TEST cTest; 
>         printf("C_TEST::m_nData = %d\n", cTest.GetData());
>         return 0;
>     }
>     ```
>     
>     ![https://blog.kakaocdn.net/dn/ctsjPD/btqxF9E9iPo/DtwhsDSDBFneWlbi9Qnlr0/img.png](https://blog.kakaocdn.net/dn/ctsjPD/btqxF9E9iPo/DtwhsDSDBFneWlbi9Qnlr0/img.png)

<br><br>

>[!note]
> **멤버 함수의 명시적 삭제**
>     
>     멤버 함수 다중 정의 시 멤버 함수에 delete 키워드를 사용하면 명시적으로 삭제하기 때문에 사용자 쪽에서 해당 멤버 함수를 호출하면 컴파일 오류를 발생시킨다.
>     
>     ex) void SetData(int nParam);
>     
>     void SetData(float fParam) = delete; //인자로 float 자료형의 데이터를 받으면 컴파일 오류가 발생한다.
    
<br><br>
    
>[!note]
> **정적 멤버 변수와 정적 멤버 함수**
>     
>     static 키워드를 사용한 클래스 멤버를  정적 멤버 변수와 정적 멤버 함수는 전역 변수나 전역 함수와 마찬가지이기 때문에 객체를 생성하지 않고 호출이 가능하다. 정적 멤버 변수는 반드시 선언과 정의를 분리해야 한다. 소속 객체가 없는 전역 변수나 전역 함수를 많이 사용하면 객체지향 특성이 퇴화되기 때문에 되도록 정적 멤버를 사용하는 것이 좋다. this 포인터를 사용할 수 없다. 
>     
>     - 정적 멤버 변수 : *자료형 클래스이름* :: *변수이름* = *값*; //클래스 외부에 정의해야 한다.
>     - 정적 멤버 함수 : static *자료형 클래스이름* :: *함수이름*();

<br><br>
    
- 생성자 : 생성자는 객체 생성 시 자동 호출되는 멤버 함수로, 클래스의 객체는 반드시 한 개 이상의 생성자가 호출되어야 하기 때문에 클래스 내부에 생성자를 정의하지 않으면 디폴트 생성자가 자동으로 호출된다. 클래스 멤버 변수의 접근 제어 지시자를 private 멤버 변수로 선언하여 외부에서 초기화를 할 수 없거나, 사용자가 멤버 변수의 값을 별도로 지정하지 않아도 생성자에서 멤버 변수 초기화를 할 수 있기 때문에 초깃값을 대입해 오류를 차단할 수 있다. 이렇게 클래스의 멤버에 대한 초기화를 위해 생성자를 제공하는 것이다. 클래스 이름과 생성자 이름이 동일하며 반환형이 없다. 또한 생성자는 함수 원형의 종류가 다양하여 다중 정의가 가능하다.
    
>[!note]
> **멤버 변수의 초기화 방법**
>     
>     - C 방식 초기화 : *자료형 변수이름* = *값*;
>         
>         ex) int a = 10;
>         
>     - C++ 방식 초기화 : *자료형 변수이름*(*값*);
>         
>         ex) int a(10);
>         
>     - 생성자 초기화 목록 : 생성자 내부에서 대입 연산자를 이용해 멤버 변수의 값을 초기화할 수 있지만 클래스 객체의 선언 후에 초기화를 진행한다. 그러면 선언과 동시에 초기화를 해야만 하는 참조자 멤버 변수, const 멤버 변수는 대입 연산자로 초기화할 수 없게 된다. 이러한 문제를 해결하기 위해 생성자 초기화 목록을 이용해서 초기화를 하면, 클래스 객체의 선언과 동시에 멤버변수가 초기화가 되어 클래스가 생성되기 때문에 모든 멤버 변수를 초기화할 수 있게 된다.
>     
>     **예제3) 생성자 초기화 목록을 이용해 멤버 변수 초기화하기**
>     
>     ```cpp
>     #include <stdio.h>
>     
>     class C_REFTEST
>     {
>     private:
>         int &m_rData; //참조자 멤버 변수 : 객체가 생성될 때 반드시 초기화해야 하므로 생성자 초기화 목록을 사용해야 한다.
>      
>         public:
>         C_REFTEST(int & rParam) :
>             m_rData(rParam)
>         {
>      
>         }
>      
>         int GetData()
>         {
>             return m_rData;
>         }
>     };
>      
>     int main()
>     {
>         int nData = 30;
>         C_REFTEST cRefTest(nData);
>         printf("C_REFTEST::m_rData = %d\n", cRefTest.GetData());
>      
>         nData = 50;
>         printf("C_REFTEST::m_rData = %d\n", cRefTest.GetData());
>         return 0;
>     }
>     ```
>     
>     ![https://blog.kakaocdn.net/dn/eajTXC/btqxHSILDru/JBBeEYCDMao5OaNZak8Ds1/img.png](https://blog.kakaocdn.net/dn/eajTXC/btqxHSILDru/JBBeEYCDMao5OaNZak8Ds1/img.png)
    
<br><br>
    
>[!note]
> **생성자 종류**
>     
>     - 기본 생성자: 객체 생성 시 클래스 내부에 생성자를 정의하지 않으면 이 생성자가 자동 호출된다. 매개 변수가 없는 생성자이기 때문에 인자를 받지 않는다.
>         - 사용 형식 : *클래스이름*();
>     - 사용자 정의 생성자 : 사용자가 정의한 생성자로 매개변수로 인자 값을 받을 수 있는 생성자이다.
>         - 사용 형식 : *클래스이름* (*자료형 매개변수*, ...);
>     - 복사 생성자 : 클래스의 생성자의 매개변수를 같은 클래스 자료형으로 선언하는 생성자이다. 기본 생성자 대신에 복사 생성자가 호출되려면 사용자가 클래스 객체에 다른 클래스 객체에 대입할 경우 복사 생성자가 자동으로 호출되고 생성자의 멤버 변수 대 멤버 변수의 복사가 일어나게 된다.
>         - 사용 형식 : 클래스이름 ( const *클래스이름* &*매개변수* );

<br><br>
    
- 소멸자 : 객체 소멸 시 자동으로 호출되는 멤버 함수이며, 디폴트 함수이다. 하나만 존재하기 때문에 다중 정의를 할 수 없다.
    - 사용 형식 : ~ *클래스이름* ();

<br><br>
    **예제4) 클래스의 생성자와 소멸자 호출하기**
    
    ```cpp
    #include <stdio.h>
    class C_TEST
    {
    public:
        C_TEST() //디폴트 생성자는 선언하지 않아도 자동으로 호출된다.
        {
            printf("C_TEST::C_TEST()\n");
        }    
     
        ~C_TEST() //디폴트 소멸자는 선언하지 않아도 자동으로 호출된다.
        {
            printf("C_TEST::~C_TEST()\n");
        }
    };
     
    int main()
    {
        printf("main() : Begin\n");
     
        C_TEST cTest; //객체를 생성한 시점에서 생성자가 호출된다.(클래스의 객체를 전역으로 선언할 경우 객체의 생성자가 main() 함수보다 먼저 호출된다.)
     
        printf("main() : End\n");
     
        return 0; //main()이 끝난 후에 객체가 소멸되면서 소멸자가 호출된다.(클래스의 객체를 전역으로 선언할 경우 main()이 끝나면 소멸자가 호출된다.)
    }
    ```
    
    ![https://blog.kakaocdn.net/dn/SdFgA/btqxGxevvhv/PDNLUGkeyEtpxKDtCY6kKK/img.png](https://blog.kakaocdn.net/dn/SdFgA/btqxGxevvhv/PDNLUGkeyEtpxKDtCY6kKK/img.png)
    
<br><br>

**예제5) 클래스의 생성자를 다중 정의하여 사용자 정의 생성자 사용하기**

```cpp
#include <stdio.h>

class C_OVERLOADING_TEST
{
private:
    int m_nData;
 
public:
    C_OVERLOADING_TEST(int nParam)
    {
        m_nData = nParam;
    }
 
    C_OVERLOADING_TEST(int nParam1, int nParam2)
    {
        m_nData = nParam1 + nParam2;
    }
 
    int GetData()
    {
        return m_nData;
    }
};
 
int main()
{
    C_OVERLOADING_TEST cTest1(10);
    C_OVERLOADING_TEST cTest2(20, 30);
 
    printf("C_OVERLOADING_TEST(int nParam) = %d\n", cTest1.GetData());
    printf("C_OVERLOADING_TEST(int nParam1, int nParam2) = %d\n", cTest2.GetData());
    return 0;
}
```

![https://blog.kakaocdn.net/dn/zx9Qm/btqxEPUHp5m/dJXxHbuhYM5skMhbiac3S1/img.png](https://blog.kakaocdn.net/dn/zx9Qm/btqxEPUHp5m/dJXxHbuhYM5skMhbiac3S1/img.png)

<br><br>
<br><br>

**클래스 사용하기**

- 객체 선언하기 : *클래스형 객체이름*;
    
    ex) C_NAME cName;
    
- 객체 배열 선언하기 : *클래스형 객체이름*[];
    
    ex) C_NAME cName[30];
    
- 동적 할당 객체 선언하기 : *클래스형* **객체이름* = new *클래스형*;
    
    ex) C_NAME *p_cName = new C_NAME;
    
    delete [] C_NAME;
    
<br><br>

**예제6) 클래스 정의하고 사용하기**

```cpp
#include <stdio.h>

class C_DYNAMIC_ALLOCATION
{
private:
    int m_nData;
 
public:
    C_DYNAMIC_ALLOCATION();
    ~C_DYNAMIC_ALLOCATION();
};
 
int main()
{
    printf("main() : Begine\n");
    C_DYNAMIC_ALLOCATION *pcData = new C_DYNAMIC_ALLOCATION; //동적으로 객체를 생성한다.
 
    delete pcData; // 동적 할당한 객체를 해제한다.
    printf("main() : End\n");
 
    return 0;
}
 
C_DYNAMIC_ALLOCATION::C_DYNAMIC_ALLOCATION()
{
    printf("C_DYNAMIC_ALLOCATION::C_DYNAMIC_ALLOCATION()\n");
}
 
C_DYNAMIC_ALLOCATION::~C_DYNAMIC_ALLOCATION()
{
    printf("C_DYNAMIC_ALLOCATION::~C_DYNAMIC_ALLOCATION()\n");
}
```

![https://blog.kakaocdn.net/dn/XQG2V/btqxGi9KRHf/sxhugBtnFVYLe8Dm8K52Nk/img.png](https://blog.kakaocdn.net/dn/XQG2V/btqxGi9KRHf/sxhugBtnFVYLe8Dm8K52Nk/img.png)

<br><br>

**예제7) 클래스를 정의하고 배열로 사용하기**

```cpp
#include <stdio.h>
class C_DYNAMIC_ALLOCATION
{
private:
    int m_nData;
 
public:
    C_DYNAMIC_ALLOCATION();
    ~C_DYNAMIC_ALLOCATION();
};
 
int main()
{
    printf("main() : Begine\n");
    C_DYNAMIC_ALLOCATION *pcData = new C_DYNAMIC_ALLOCATION[5]; //동적으로 객체를 배열로 생성한다.
 
    delete[] pcData; // 배열로 동적 할당한 객체는 배열로 해제한다.
    printf("main() : End\n");
 
    return 0;
}
 
C_DYNAMIC_ALLOCATION::C_DYNAMIC_ALLOCATION()
{
    printf("C_DYNAMIC_ALLOCATION::C_DYNAMIC_ALLOCATION()\n");
}
 
C_DYNAMIC_ALLOCATION::~C_DYNAMIC_ALLOCATION()
{
    printf("C_DYNAMIC_ALLOCATION::~C_DYNAMIC_ALLOCATION()\n");
}
```

![https://blog.kakaocdn.net/dn/dc1cY3/btqxEOVMpKz/6fV97yx4GkwNNdzSfLXttk/img.png](https://blog.kakaocdn.net/dn/dc1cY3/btqxEOVMpKz/6fV97yx4GkwNNdzSfLXttk/img.png)
