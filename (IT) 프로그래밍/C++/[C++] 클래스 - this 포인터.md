# [C++] 클래스 : this 포인터

# this 포인터

클래스 객체를 생성하면 객체의 메모리가 할당되고 주소가 주어지는데, this 포인터를 사용해서 객체 자신의 주소를 가리킬 수 있으며, 클래스의 멤버 함수에서만 사용할 수 있다. 자신의 주소를 갖고 있는 포인터이기 때문에 멤버의 접근은 -> 연산자를 사용한다.

- 사용 형식 : this->*멤버변수∙멤버함수*

**예제1) this 포인터를 이용하여 클래스 자신 참조하기**

```cpp
#include <stdio.h>
class C_THIS_TEST
{
private:
    int m_nData;
public:
    C_THIS_TEST(int nParam) :
        m_nData(nParam)
    {
    }
 
    void PrintData()
    {
        printf("m_nData = %d\n", m_nData);
        printf("C_THIS_TEST::m_nData = %d\n", C_THIS_TEST::m_nData);
        printf("this->m_nData = %d\n", this->m_nData);
    }
};
 
int main()
{
    C_THIS_TEST cThisTest1(30);
    C_THIS_TEST cThisTest2(50);
 
    cThisTest1.PrintData();
    printf("\n");
    cThisTest2.PrintData();

    return 0;
}
```

![https://blog.kakaocdn.net/dn/bgzYKJ/btqxHtv2OPn/qfJWRnvG4klsn6MlCEUWbK/img.png](https://blog.kakaocdn.net/dn/bgzYKJ/btqxHtv2OPn/qfJWRnvG4klsn6MlCEUWbK/img.png)

<aside>
💡

***this 포인터**

클래스 멤버 함수에 *this 포인터를 이용해 객체 자신을 반환해서 다른 객체가 참조해서 사용할 수도 있다.

**예제2) *this 포인터로 셀프 참조하기**

```cpp
#include <stdio.h>

class C_THIS_TEST
{
private:
    int m_nData;
    
public:
    C_THIS_TEST(int nParam):
        m_nData(nParam)
    {
    }
 
    C_THIS_TEST GetThis()
    {
        return *this; //객체 자신의 주소를 반환한다.
    }
 
    C_THIS_TEST PrintThis()
    {
        printf("m_nData = %d\n", m_nData);
        return *this;
    }
};
 
int main()
{
    C_THIS_TEST cThisTest(30);
    C_THIS_TEST &&rcThisTest = cThisTest.GetThis();
    cThisTest.PrintThis();
    rcThisTest.PrintThis();
    rcThisTest.GetThis().PrintThis();
 
    return 0;
}
```

![https://blog.kakaocdn.net/dn/cEuMXE/btqxEPAvoWC/Pd61MW43FV5tmU0wA8cjzk/img.png](https://blog.kakaocdn.net/dn/cEuMXE/btqxEPAvoWC/Pd61MW43FV5tmU0wA8cjzk/img.png)

</aside>