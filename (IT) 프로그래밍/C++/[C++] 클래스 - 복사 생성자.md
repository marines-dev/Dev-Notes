# [C++] 클래스 : 복사 생성자

# 복사 생성자

복사 생성자는 기존 C++ 동작 원리에서 객체에 객체를 대입하여 복사하면서 발생하는 문제를 해결하기 위해 만들어졌다.

사용자가 클래스 객체 선언 시 객체에 대입 연산자(=)를 이용하여 같은 객체로 초기화를 하면 자동으로 =가 ()로 변경된다. 그러면 복사된 객체의 생성자가 호출되어 복사 객체가 원본 객체의 매개변수로 전달되는 형태가 된다. 그리고 복사 객체가 사용 완료된 후에 소멸되면서 소멸자가 호출되고, 원본 객체의 멤버 변수가 소멸되면서 원본 객체의 소멸자도 호출된다.

문제는 이때, 객체의 생성자의 매개변수가 참조자 형태(&)가 아닌 Call by value 형태라면, 매개변수의 초기화 과정에서 객체가 계속 생성되어 생성자가 반복적으로 호출되는 문제가 발생한다. 이러한 문제를 해결하기 위해서 객체를 복사할 경우 C++ 내부에서 기본 복사 생성자가 자동으로 호출되며, 기본 복사 생성자의 매개변수는 & 참조 형태이며, 복사 객체에서 원본 객체의 값을 변경하지 않도록 const 키워드도 추가된다.

만약 객체를 복사해야 하고, 멤버 변수도 직접 초기화해야 한다면 이때는 복사 생성자를 직접 정의해야 한다.

- 함수 원형 : *클래스형* (const *클래스형* &*매개변수*);

**예제1) 기본 복사 생성자를 자동 호출하여 객체 복사하기**

```cpp
#include <stdio.h>
class C
{
public:
		C()
		{
    		printf("Called Constructor\n");
		}
 
		~C()
		{
    		printf("Called Destructor\n");
		}
};
 
int main()
{
    C cScr;
    C cDest = cScr; //C cDest(cSrc)로 변경되고, 복사 객체는 복사 생성자가 호출되어 내부에서 원본 객체를 복사하게 된다.
    
    return 0;
}
 

```

![https://blog.kakaocdn.net/dn/cgcQ2d/btqxECagpzC/TAPFWgkbgqu2ujx4Q234U1/img.png](https://blog.kakaocdn.net/dn/cgcQ2d/btqxECagpzC/TAPFWgkbgqu2ujx4Q234U1/img.png)

**예제2) 복사 생성자를 직접 정의하여 객체의 멤버 복사하기**

```cpp
#include <stdio.h>
class C
{
private:
    int m_nData;
 
public:
		C(int nParam) :
    		m_nData(nParam)
		{
    		printf("Called Constructor\n");
		}
 
		C(const C & rc) :
    		m_nData(rc.m_nData) //원본객체의 멤버를 초기화한다.
		{
    		printf("Called Copy Cestructor\n");
		}
 
		~C()
		{
    		printf("Called Destructor\n");
		}
 
		int GetData() const
		{
    		return m_nData;
		}
};
 
int main()
{
    C cTest1(30);
    C cTest2(cTest1);
 
    printf("cTest1 = %d\n", cTest1.GetData());
    printf("cTest2 = %d\n", cTest2.GetData());
 
    return 0;
}
```

![https://blog.kakaocdn.net/dn/m5FQo/btqxG8r5v9K/mspP9vwP6RJpd43fcYX1Sk/img.png](https://blog.kakaocdn.net/dn/m5FQo/btqxG8r5v9K/mspP9vwP6RJpd43fcYX1Sk/img.png)

### 클래스의 얕은 복사와 깊은 복사

객체의 복사가 일어날 때 클래스의 멤버 변수가 포인터이고, 동적 할당할 경우 복사 객체는 원본 객체의 힙 메모리를 공유하게 된다. 그렇기 때문에 복사 객체에서 동적 할당한 멤버 변수를 해제할 경우 이미 해제를 한 메모리를 원본 객체에서 다시 해제하는 얕은 복사의 문제가 발생한다. 이러한 문제를 해결하기 위해서 원본 객체의 포인터 멤버 변수의 메모리를 복사 객체가 공유하지 않도록 복사 생성자를 직접 정의해서 내부에서 포인터 멤버 변수를 동적 할당하여 다른 메모리를 구성한 후 원본 객체의 멤버 포인터 변수의 값을 대입하는 형태로 구성해야 한다. 그러면 각각 다른 메모리 공간을 참조하기 때문에 동적 할당한 멤버 변수를 해제해도 문제가 발생하지 않는다. 이렇게 객체의 멤버의 포인터까지 깊게 복사한다는 뜻으로 깊은 복사라고 한다.

**예제3) 클래스의 얕은 복사의 문제점**

```cpp
#include <stdio.h>

class C
{
private:
    int *m_pData;
 
public:
    C(int pParam)
    {
        m_pData = new int; //동적 할당
        *m_pData = pParam;
    }
 
    ~C()
    {
        delete m_pData; //동적 할당한 메모리 해제할 경우 오류가 발생한다.
 
    int GetData() const
    {
        return *m_pData;
    }
};

int main()
{
    C cTest1(30);
    C cTest2 = cTest1; //객체의 복사 : 복사 생성자가 호출되고 m_pData의 힙 메모리를 공유하게 된다.
    printf("cTest1 = %d\n", cTest1.GetData());
    printf("cTest2 = %d\n", cTest2.GetData());
 
    return 0;
}
```

![https://blog.kakaocdn.net/dn/YBqPU/btqxGvgIMWu/PK02tteQw1ET536Y4UxDH1/img.png](https://blog.kakaocdn.net/dn/YBqPU/btqxGvgIMWu/PK02tteQw1ET536Y4UxDH1/img.png)

**예제4) 클래스의 깊은 복사 수행하기**

```cpp
#include <stdio.h>

class C
{
private:
    int *m_pData;
 
public:
    C(const C& rParam) //복사 생성자
    {
        printf("Called Copy Constructor\n");
        m_pData = new int; //복사 객체의 m_pData를 동적 할당한다.
        *m_pData = *rParam.m_pData; // 원본 객체의 m_pData 값을 복사 객체의 m_pData에 복사한다.
    }
 
    ~C()
    {
        printf("Called Destructor\n");
        delete m_pData; //복사생 성자에 따로 멤버포인터를 동적할당함으로 서 원본객체와 복사객체의 멤버포인터가 각각 할당되고 해제된다.
    }
 
    int GetData() const
    {
        return *m_pData;
    }
};

int main()
{
    C cTest1(30);
    C cTest2 = cTest1; //객체의 복사 : 복사생성자가 호출되고 m_pData의 힙 메모리를 공유하게 된다.
    printf("cTest1 = %d\n", cTest1.GetData());
    printf("cTest2 = %d\n", cTest2.GetData());
 
    return 0;
}
```

![https://blog.kakaocdn.net/dn/BzKeI/btqxF9yqPUc/5w183IdvWMrszZKrAbzhAk/img.png](https://blog.kakaocdn.net/dn/BzKeI/btqxF9yqPUc/5w183IdvWMrszZKrAbzhAk/img.png)

<aside>
💡 **복사 생성자가 호출되는 시점**

- 복사 객체에 원본 객체를 대입할 경우 : 복사 객체에 원본 객체를 대입하여 초기화하면 복사 객체의 복사 생성자가 호출되며 복사 생성자에서 원본 객체의 멤버 복사가 일어난다.
    
    ex) C cSrc;
    
    C cDest = cSrc; //복사객체의 복사생성자가 호출된다.
    

- Call by value 방식으로 함수의 매개변수를 객체를 전달하는 경우 : Call by value 방식으로 함수의 매개변수를 객체로 받으면 매개변수의 객체가 할당되고 동시에 복사 생성자가 호출되어 원본객체를 복사하여 초기화한다. 이때, 함수가 매개변수의 객체를 반환하지 않으면 함수가 끝나는 동시에 소멸된다.
    
    ex) C cSrc(10, 20);
    
    void TestFunc(cSrc); //매개변수가 복사객체가 되고 복사생성자를 호출하여 원본객체의 멤버를 복사하게 된다.
    

- 함수가 일반 객체를 반환하는 경우 : 매개변수인 복사 객체를 반환하면 임시 객체가 생성되고 임시 객체의 복사 생성자가 호출되어 객체를 복사하게 되는데, 이때, 반환된 객체를 받을 변수가 존재하지 않는다면 임시 객체는 소멸된다.
    
    ex) C cSrc;
    
    C TestFunc(cSrc); //객체가 반환되면서 임시객체가 생성되고 복사생성자가 호출되어 매개변수가 복사된다.
    
</aside>

<aside>
💡 **객체의 복사를 막는 방법**

객체를 복사하여 복사 생성자까지 호출되다 보면 프로그램 성능이 떨어지게 될 수 있으므로 복사 생성자를 사용할 필요가 없는 경우에는 안전하게 delete 키워드를 이용하여 복사 생성자를 사용할 수 없도록 하자.

- 사용 형식 : *클래스형* (const *클래스형* &*매개변수*) = delete;

ex) C(const C &rParam) = delete;

</aside>