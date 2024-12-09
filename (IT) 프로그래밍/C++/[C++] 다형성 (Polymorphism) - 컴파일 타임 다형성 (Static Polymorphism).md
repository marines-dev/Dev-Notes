# [C++] 다형성 (Polymorphism) : 컴파일 타임 다형성 (Static Polymorphism)

<br><br>

# 다형성 (Polymorphism)

다형성은 객체지향 프로그래밍에서 중요한 개념으로, 하나의 이름으로 여러 형태의 기능을 제공하는 것을 의미한다. 다형성을 통해 같은 이름의 메서드나 함수가 서로 다르게 동작하도록 만들 수 있으며, 이를 통해 유연하고 확장 가능한 코드를 작성할 수 있다.

C++에서는 다형성을 컴파일 타임 다형성과 런타임 다형성 두 가지 주요 형태로 구현한다.

<br><br>
<br><br>

# **컴파일 타임 다형성 (Static Polymorphism)**

컴파일 타임 다형성은 함수 오버로딩(Overloading), 연산자 오버로딩(Operator Overloading)을 통해 구현된다. 이 방식은 함수나 연산자의 호출이 컴파일 시점에 결정되는 다형성이다.

<br><br>

### **함수 오버로딩(Function Overloading)**

C++은 같은 이름의 함수 원형이 다른 동일한 이름의 함수를 다중 정의하여 사용할 수 있는데, 이때 주의할 점은 함수 원형의 매개변수(자료형, 개수)가 다를 경우에만 정의할 수 있으며, 함수의 반환형으로는 구분할 수 없다.

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

<br><br>
<br><br>

### **연산자 오버로딩 (Operator Overloading)**

C++에서 연산자 오버로딩은 기존 연산자의 동작을 사용자 정의 타입(ex. 클래스)에서도 적용할 수 있도록 새로운 기능을 추가하는 기능이다. 함수로 지원이 가능한 기존 연산자에 operator  키워드를 사용하여 함수에 다른 기능을 추가하여 다중 정의하면 연산자를 함수처럼 호출할 수 있다. 이를 통해 클래스와 같은 객체도 연산을 할 수 있게 된다. 

연산자 함수 정의 시 주의할 점은 기본 연산자의 기능을 변경하는 등의 본래의 의도를 벗어난 형태의 연산자 함수는 사용하지 않도록 하며, 연산자 함수를 만들어도 연산자의 우선순위와 결합성은 변하지 않는다. 또한 논리 연산자(&&, ||, !)는 심각한 논리적 오류를 발생시킬 수 있기 때문에 논리 연산자 함수를 사용해서는 안된다.

<br><br>

>[!note]
> **멤버 함수와 전역 함수로 연산자 오버로딩**
> 
> 멤버 함수는 직관적이며, 대부분의 경우 사용하기에 적합하며, 전역 함수는 객체가 연산자의 좌항이 아닐 수 있는 상황을 처리하거나, 교환 법칙을 지원하려는 경우에 유리하다.
> 
> - 멤버 함수로 연산자 오버로딩 : 대입 연산자(=), 함수 호출 연산자(()), 배열 접근 연산자([]), 멤버 접근 포인터 연산자(->)를 연산자 함수로 정의해 오버로딩할 수 있다.
>     - 사용 형식 : *객체이름* . operator *연산자* (*매개변수*);
>     
>     **예제2) 멤버 함수로 연산자 오버로딩하기**
>     
>     ```cpp
>     class MyClass 
>     {
>     public:
>         int value;
>         MyClass(int val) : value(val) {}
>         MyClass operator+(const MyClass& other) 
>         {
>             return MyClass(this->value + other.value);
>         }
>     };
>     
>     int main() 
>     {
>     		MyClass a(5), b(10);
>     		MyClass c = a + b; // a.operator+(b) 호출
>         return 0;
>     }
>     ```
>     
> - 전역 함수로 연산자 오버로딩 : 전역 함수로 연산자를 오버로딩할 수도 있다. 곱셈의 교환 법칙의 성립을 구현을 해야 하는 등의 전역 함수로 연산자 다중 정의를 해야하는 경우도 있는데, 클래스의 private 멤버에 접근하기 위해서 friend 키워드를 붙여준다.
>     - 사용 형식 : friend operator *연산자* (*매개객체*);
>     
>     ex) 전역 함수와 멤버 함수의 차이
>     
>     - 멤버 함수 (불가능) : 8.operator*(obj); // 문법 오류
>     - 전역 함수 (가능) : operator*(8, obj);
>     
>     **예제3) 전역 함수로 연산자 오버로딩 하기**
>     
>     ```cpp
>     class MyClass 
>     {
>         int value;
>     public:
>         MyClass(int val) : value(val) {}
>         friend MyClass operator*(int scalar, const MyClass& obj) 
>         {
>             return MyClass(scalar * obj.value);
>         }
>     };
>     
>     int main() 
>     {
>     		MyClass obj(10);
>     		MyClass result = 3 * obj; // operator*(3, obj) 호출
>         return 0;
>     }
>     ```

<br><br>

>[!note]
> **오버로딩 불가능한 연산자**
> 
> - . (멤버 접근 연산자)
> - .* (멤버 포인터 연산자)
> - :: (범위 지정 연산자)
> - ?: (조건 연산자, 3항 연산자)
> - typeid (RTTI 관련 연산자)
> - sizeof (바이트 단위 크기 연산자)
> - static_cast (형 변환 연산자)
> - dynamic_cast (형 변환 연산자)
> - const_cast (형 변환 연산자)
> - reinterpret_cast (형 변환 연산자)

<br><br>
<br><br>

**산술 연산자 오버로딩** 

+, -, *, / 등 산술 연산자들을 연산자 함수로 정의해 오버로딩할 수 있다.

산술 연산자는 멤버 함수와 전역 함수 모두로 오버로딩할 수 있다.

산술 연산자 오버로딩 시 주의할 점은 연산자의 본래 의미를 유지해야 하므로, 새로운 산술 연산자를 정의하기보다, 기존 연산자를 객체 간 동작에 맞게 확장하는 것이 목적이다.

<br><br>

**예제4) 멤버 함수로 산술 연산자 오버로딩 하기**

```cpp
class C_OVERLOAD 
{
    int value;
public:
    C_OVERLOAD(int val) : value(val) {}

    // 멤버 함수로 '+' 연산자 오버로딩
    C_OVERLOAD operator+(int nParam) const 
    {
        return C_OVERLOAD(value + nParam);
    }

    // 멤버 함수로 '-' 연산자 오버로딩
    C_OVERLOAD operator-(const C_OVERLOAD& other) const 
    
        return C_OVERLOAD(value - other.value);
    }

    // 결과 출력 함수
    void display() const 
    {
        std::cout << "Value: " << value << std::endl;
    }
};

int main()
{
		C_OVERLOAD obj1(10);
		C_OVERLOAD obj2(20);

		// 정수와의 '+' 연산
		C_OVERLOAD result1 = obj1 + 5;  // obj1.operator+(5)
		result1.display();              // 출력: Value: 15

		// 객체 간의 '-' 연산
		C_OVERLOAD result2 = obj2 - obj1;  // obj2.operator-(obj1)
		result2.display();                 // 출력: Value: 10

		return 0;
}
```

<br><br>

**예제5) 전역 함수로 산술 연산자 오버로딩 하기**

```cpp
class C_OVERLOAD 
{
    int value;
public:
    C_OVERLOAD(int val) : value(val) {}

    friend C_OVERLOAD operator+(const C_OVERLOAD& lhs, int rhs) 
    {
        return C_OVERLOAD(lhs.value + rhs);
    }

    friend C_OVERLOAD operator*(int lhs, const C_OVERLOAD& rhs) 
    {
        return C_OVERLOAD(lhs * rhs.value);
    }

    void display() const 
    {
        std::cout << "Value: " << value << std::endl;
    }
};

int main()
{
		C_OVERLOAD obj(10);

		// 객체와 정수 간의 '+' 연산
		C_OVERLOAD result1 = obj + 15;  // operator+(obj, 15)
		result1.display();              // 출력: Value: 25

		// 정수와 객체 간의 '*' 연산
		C_OVERLOAD result2 = 3 * obj;   // operator*(3, obj)
		result2.display();              // 출력: Value: 30

		return 0;
}
```

<br><br>
<br><br>

**단항 연산자 오버로딩**

증감 연산자(++, --), 부호 연산자(+, -), 논리 NOT 연산자(!), 비트 NOT 연산자(~), 주소 연산자(&), 포인터 역참조 연산자(*)를 연산자 함수로 정의해 오버로딩할 수 있다. 

이때, 전위 연산자(++obj, -obj)는 일반적인 형태로 정의하며, 후위 연산자(obj++, obj--)는 int 타입의 더미 매개변수를 사용해 구분한다.

단항 연산자는 필요에 따라 전역 함수로 정의할 수도 있지만, 일반적으로 멤버 함수로 오버로딩한다. 왜냐하면 호출 객체를 암묵적으로 `this`를 통해 사용하므로 피연산자 전달이 필요 없다. 

<br><br>

**예제6) 전위 증감 연산자로 오버로딩하기**

```cpp
class Counter 
{
    int value;
public:
    Counter(int val = 0) : value(val) {}

    // 전위 증감 연산자 오버로딩
    Counter& operator++() 
    {
        ++value; // 객체 값 증가
        return *this; // 변경된 객체 반환
    }

    Counter& operator--() 
    {
        --value; // 객체 값 감소
        return *this;
    }

    void display() const 
    {
        std::cout << "Value: " << value << std::endl;
    }
};

int main()
{
		Counter c(10);
		++c;    // c.operator++()
		c.display();  // 출력: Value: 11
		
		--c;    // c.operator--()
		c.display();  // 출력: Value: 10
		
		return 0;
}
```

<br><br>

**예제7) 후위 증감 연산자로 오버로딩하기**

```cpp
class Counter 
{
    int value;
public:
    Counter(int val = 0) : value(val) {}

    // 후위 증감 연산자 오버로딩
    Counter operator++(int) 
    {
        Counter temp = *this; // 현재 상태 저장
        value++;              // 객체 값 증가
        return temp;          // 증가 전 상태 반환
    }

    Counter operator--(int) 
    {
        Counter temp = *this;
        value--;
        return temp;
    }

    void display() const 
    {
        std::cout << "Value: " << value << std::endl;
    }
};

int main()
{
		Counter c(10);
		c++;    // c.operator++(int)
		c.display();  // 출력: Value: 11

		c--;    // c.operator--(int)
		c.display();  // 출력: Value: 10

		return 0;
}
```

<br><br>

**예제8) 부호 연산자로 오버로딩하기**

```cpp
class Number 
{
    int value;
public:
    Number(int val = 0) : value(val) {}

    // 음수 부호 연산자 오버로딩
    Number operator-() const 
    {
        return Number(-value);
    }

    // 양수 부호 연산자 오버로딩
    Number operator+() const 
    {
        return Number(+value);
    }

    void display() const 
    {
        std::cout << "Value: " << value << std::endl;
    }
};

int main()
{
		Number n(5);
		Number neg = -n;  // n.operator-()
		neg.display();    // 출력: Value: -5
		
		Number pos = +n;  // n.operator+()
		pos.display();    // 출력: Value: 5
		
		return 0;
}
```

<br><br>

**예제9) 전역 함수로 단항 연산자 오버로딩하**

```cpp
class MyClass {
    int value;
public:
    MyClass(int val = 0) : value(val) {}

    friend MyClass operator!(const MyClass& obj) {
        return MyClass(!obj.value); // 논리 NOT 연산
    }

    void display() const {
        std::cout << "Value: " << value << std::endl;
    }
};

int main()
{
		MyClass obj(0);
		MyClass result = !obj;  // operator!(obj)
		result.display();       // 출력: Value: 1

		return 0;
}
```

<br><br>
<br><br>

**디폴트 대입 연산자**

디폴트 대입 연산자는 C++ 컴파일러에 의해 자동으로 생성되며, 객체의 멤버 변수를 얕은 복사 방식으로 복사한다. 이는 복사 생성자와 유사하게 동작하지만, 객체가 생성된 이후에 기존 객체의 데이터를 새 객체로 대입하는 경우에 사용된다. 디폴트 대입 연산자는 멤버를 1:1로 복사하는 단순한 방식이므로, 동적 메모리나 파일 핸들처럼 자원을 관리하는 클래스에서는 동일한 메모리를 여러 객체가 공유하게 되어 메모리 누수나 예상치 못한 런타임 오류가 발생할 위험이 있다. 특히 상속 관계에서는 자식 클래스에서 대입 연산자를 정의할 경우 부모 클래스의 대입 연산자가 자동으로 호출되지 않으므로, 이를 명시적으로 호출해야 부모 클래스의 멤버 변수까지 제대로 복사할 수 있다. 이러한 한계를 해결하고 안전한 자원 관리를 보장하기 위해서는 사용자 정의 대입 연산자를 작성하여 얕은 복사로 인한 문제를 방지하고 자기 대입을 처리하는 것이 필수적이다.

<br><br>

**예제10) 디폴트 대입 연산자의 한계와 사용자 정의 대입 연산자의 필요성**

```cpp
#include <iostream>
#include <cstring>
using namespace std;

class String 
{
    char* data;
public:
    // 생성자
    String(const char* str = "") 
    {
        data = new char[strlen(str) + 1];
        strcpy(data, str);
        cout << "Constructor called: " << data << endl;
    }

    // 소멸자
    ~String() 
    {
        delete[] data;
        cout << "Destructor called" << endl;
    }

    // 디폴트 대입 연산자 사용
    // String& operator=(const String& rhs); // 컴파일러가 자동 생성

    // 사용자 정의 대입 연산자
    String& operator=(const String& rhs) 
    {
        if (this != &rhs) { // 자기 대입 방지
            delete[] data; // 기존 메모리 해제
            data = new char[strlen(rhs.data) + 1]; // 새 메모리 할당
            strcpy(data, rhs.data);
            cout << "Assignment operator called: " << data << endl;
        }
        return *this;
    }

    void display() const 
    {
        cout << "String: " << data << endl;
    }
};

int main() 
{
    String str1("Hello");
    String str2("World");

    str2 = str1; 
    // 디폴트 대입 연산자를 사용하면 얕은 복사가 발생한다.
		//사용자 정의 대입 연산자가 호출되어 str2가 str1의 데이터를 복사받고, 기존의 동적 메모리를 해제한다.
		
    str1.display();
    str2.display();

    return 0;
}
```

<br><br>
<br><br>

**관계 연산자 오버로딩**

상등 연산자(==), 부등 연산자(!=), 비교 연산자(>, <, >=, <=)로, 이 연산자들은 두 피연산자의 관계를 참 또는 거짓으로 평가하여 bool형을 반환한다. 이 연산자를 오버로딩하여 사용자의 요구에 맞는 비교 동작을 정의할 수 있다. 
관계 연산자는 멤버 함수와 전역 함수로 모두 오버로딩이 가능하며, 멤버 함수로 정의할 경우, 좌측 피연산자가 항상 객체 자신(this)이어야 하므로, 좌항이 다른 타입인 경우 전역 함수로 정의해야 한다.상등 연산자(==)와 부등 연산자(!=)는 동일한 기준으로 구현하지 않으면 논리적 불일치가 발생할 수 있기 때문에 함께 오버로딩하는 것을 권장한다.

- 상등 연산자 오버로딩 형식

```cpp
bool *클래스이름*::operator==(const *클래스이름*& *other*) const 
{
    // 비교 조건 정의
}
```

- 부등 연산자 오버로딩 형식

```cpp
bool *클래스이름*::operator!=(const *클래스이름*& *other*) const 
{
    // 상등 연산자를 활용하여 구현하는 것이 일반적
    return !(*this == *other*);
}
```

- 비교 연산자 오버로딩 형식

```cpp
bool 클래스이름::operator<(const 클래스이름& other) const 
{
    // 비교 조건 구현
}
```

<br><br>

**예제11) 관계 연산자 오버로딩하기**

```cpp
#include <iostream>
using namespace std;

class Point 
{
    int x, y;
public:
    // 생성자
    Point(int x = 0, int y = 0) : x(x), y(y) {}

    // 상등 연산자 오버로딩
    bool operator==(const Point& other) const 
    {
        return x == other.x && y == other.y;
    }

    // 부등 연산자 오버로딩
    bool operator!=(const Point& other) const 
    {
        return !(*this == other); // 상등 연산자를 기반으로 구현
    }

    // 비교 연산자(<) 오버로딩
    bool operator<(const Point& other) const 
    {
        // x 좌표 기준으로 비교, 같으면 y 좌표 비교
        return (x < other.x) || (x == other.x && y < other.y);
    }
    
    void display() const 
    {
        cout << "(" << x << ", " << y << ")";
    }
};

int main() 
{
    Point p1(1, 2);
    Point p2(3, 4);
    Point p3(1, 2);

    // 상등 연산자 사용
    cout << "p1 == p2: " << (p1 == p2 ? "true" : "false") << endl;
    cout << "p1 == p3: " << (p1 == p3 ? "true" : "false") << endl;

    // 부등 연산자 사용
    cout << "p1 != p2: " << (p1 != p2 ? "true" : "false") << endl;

    // 비교 연산자 사용
    cout << "p1 < p2: " << (p1 < p2 ? "true" : "false") << endl;
    cout << "p2 < p1: " << (p2 < p1 ? "true" : "false") << endl;

    return 0;
}
```

<br><br>
<br><br>

**배열 연산자 오버로딩**

배열 접근 연산자([])는 멤버 함수로만 오버로딩할 수 있다.

배열 연산자 오버로딩은 클래스 내부 데이터를 배열처럼 접근할 수 있도록 하기 위해 사용된다.

예를 들어, 벡터, 행렬, 동적 배열 등을 다룰 때 자주 활용된다.

반환 타입은 일반적으로 객체의 멤버 변수 중 하나의 참조(reference)를 반환하며, 이를 통해 배열 연산자 결과를 수정할 수도 있다. 

const 객체에서 호출할 수 있도록 상수형 참는의 배열 연산자 오버로딩도 제공해야 하며, 수정이 불가능한 읽기 전용 접근을 제공합니다.

- 배연 연산자 오버로딩 형식 : *자료형* & *클래스이름*::operator[](int *index*);
- 상수형 참조 배열 연산자 오버로딩 형식 : const *자료형*& *클래스이름*::operator[](int index) const;

<br><br>

**예제12) 배열 연산자 오버로딩하기**

```cpp
#include <iostream>
using namespace std;

class Array 
{
    int* data;
    int size;
public:
    // 생성자
    Array(int size) : size(size) 
    {
        data = new int[size];
        for (int i = 0; i < size; i++) 
        {
            data[i] = 0; // 초기화
        }
    }

    // 소멸자
    ~Array() 
    {
        delete[] data;
    }

    // 배열 연산자 오버로딩 (비상수 버전)
    int& operator[](int index) 
    {
        if (index < 0 || index >= size) 
        {
            throw out_of_range("Index out of range");
        }
        return data[index];
    }

    // 배열 연산자 오버로딩 (상수 버전)
    const int& operator[](int index) const 
    {
        if (index < 0 || index >= size) 
        {
            throw out_of_range("Index out of range");
        }
        return data[index];
    }

    // 배열 크기 반환
    int getSize() const 
    {
        return size;
    }
};

int main() 
{
    Array arr(5);

    // 배열 요소에 접근 및 수정
    for (int i = 0; i < arr.getSize(); i++) 
    {
        arr[i] = i * 10;  // 비상수 버전 호출
    }

    // 배열 요소 출력
    for (int i = 0; i < arr.getSize(); i++) 
    {
        cout << arr[i] << " ";  // 상수 버전 호출
    }
    cout << endl;

    // 잘못된 인덱스 접근
    try 
    {
        arr[10] = 100;  // 예외 발생
    } catch (const out_of_range& e) 
    {
        cout << "Exception: " << e.what() << endl;
    }

    return 0;
}
```

<br><br>
<br><br>

**포인터 연산자 오버로딩**

C++에서 포인터와 관련된 연산자인 멤버 접근 포인터 연산자(->)와 역참조 연산자(*)는 객체를 포인터처럼 사용할 수 있도록 오버로딩할 수 있다. 이를 통해 사용자 정의 클래스에서도 포인터와 유사한 동작을 구현할 수 있다. 

- 멤버 접근 포인터 연산자 오버로딩 형식

```cpp
*반환타입* * *클래스이름*::operator->();
```

- 역참조 연산자 오버로딩 형식

```cpp
*반환타입* & *클래스이름*::operator*();
```

<br><br>

**예제13) 멤버 접근 포인터 연산자 오버로딩기**

```cpp
#include <iostream>
using namespace std;

class IntWrapper 
{
    int value;
public:
    IntWrapper(int val) : value(val) {}
    
    // 역참조 연산자 오버로딩
    int& operator*() 
    {
        return value;
    }
};

int main() 
{
    IntWrapper obj(10);
    cout << "Value through operator*: " << *obj << endl; // obj를 역참조하여 값 출력
    return 0;
}
```

<br><br>

**예제14) 역참조 연산자 오버로딩하기**

```cpp
#include <iostream>
using namespace std;

class IntWrapper 
{
    int value;
public:
    IntWrapper(int val) : value(val) {}
    
    // 역참조 연산자 오버로딩
    int& operator*() 
    {
        return value;
    }
};

int main() 
{
    IntWrapper obj(10);
    cout << "Value through operator*: " << *obj << endl; // obj를 역참조하여 값 출력
    return 0;
}
```

<br><br>
<br><br>

**형 변환 연산자 오버로딩**

C++에서 형 변환 연산자 오버로딩은 객체를 특정 타입으로 변환할 때 사용된다. 사용자 정의 클래스에서도 특정 타입으로의 변환이 필요할 때, 형 변환 연산자를 오버로딩하여 원하는 동작을 구현할 수 있다. 이를 통해 객체를 다양한 타입으로 변환할 수 있으며, 사용자가 정의한 클래스가 기본 데이터 타입처럼 동작하도록 할 수 있다.
형 변환 연산자는 반드시 멤버 함수로 정의해야 하며, 반환 타입을 명시하지 않고 변환하려는 타입을 함수 이름처럼 작성하며, 반환값은 변환하고자 하는 타입의 객체나 값을 반환해야 한다.

형 변환 연산자는 암시적 변환과 명시적 변환 모두 지원하며, 암시적 변환은 자동으로 호출되며, 명시적 변환은 static_cast 또는 C 스타일 캐스트 등을 통해 호출된다. (C++11 이후, 불필요한 암시적 호출을 방지하기 위해 **`explicit` 키워드**를 사용하여 명시적 변환만 허용할 수 있다.)

- 형 변환 연산자 오버로딩 형식

```cpp
operator *변환타입*() const;
```

<br><br>

**예제15) 객체를 기본 타입으로 변환하기**

```cpp
#include <iostream>
using namespace std;

class Distance 
{
    double meters;
public:
    Distance(double m) : meters(m) {}

    // 형 변환 연산자: Distance 객체를 double로 변환
    operator double() const 
    {
        return meters;
    }

    void display() const 
    {
        cout << meters << " meters" << endl;
    }
};

int main() 
{
    Distance d(12.34);

    // 암시적 변환
    double value = d; // operator double() 호출
    cout << "Distance as double: " << value << endl;

    // 명시적 변환
    cout << "Explicit cast: " << static_cast<double>(d) << endl;

    return 0;
}
```

<br><br>

**예제16) 객체를 사용자 정의 타입으로 변환하기**

```cpp
#include <iostream>
#include <string>
using namespace std;

class Person 
{
    string name;
public:
    Person(string n) : name(n) {}

    // 형 변환 연산자: Person 객체를 string으로 변환
    operator string() const 
    {
        return name;
    }
};

int main() 
{
    Person p("John Doe");

    // 암시적 변환
    string name = p; // operator string() 호출
    cout << "Person's name: " << name << endl;

    // 명시적 변환
    cout << "Explicit cast: " << static_cast<string>(p) << endl;

    return 0;
}
```

<br><br>

**예제17) explicit 키워드를 사용한 제어**

```cpp
class Distance 
{
    double meters;
public:
    Distance(double m) : meters(m) {}

    // 명시적 변환만 허용
    explicit operator double() const 
    {
        return meters;
    }
};

int main() 
{
    Distance d(10.5);

    // double value = d; // 컴파일 에러 (암시적 변환 불가)
    double value = static_cast<double>(d); // 명시적 변환만 가능
    cout << "Explicit cast: " << value << endl;

    return 0;
}
```

<br><br>
<br><br>

**new & delete 연산자 오버로딩**

C++에서 new와 delete는 각각 동적 메모리를 할당하고 해제하는 연산자이다. 기본적으로 이들은 C++ 표준 라이브러리에서 제공하는 힙 메모리를 사용하지만, 특정 클래스나 응용 프로그램의 요구에 맞게 메모리 관리 방식을 커스터마이징할 수 있도록 new와 delete 연산자를 다중 정의할 수 있다.

- new와  delete연산자 오버로딩 형식

```cpp
void* operator new(size_t size);
void operator delete(void* ptr);
```

- new[]와 delete[] 연산자 오버로딩 형식

```cpp
void* operator new[](size_t size);
void operator delete[](void* ptr);
```

<br><br>

**예제18) new & delete 연산자 오버로딩하기**

```cpp
#include <iostream>
#include <cstdlib> // for malloc and free
using namespace std;

class MyClass 
{
public:
    int value;

    // 사용자 정의 new 연산자
    void* operator new(size_t size) 
    {
        cout << "Custom new for size: " << size << endl;
        void* ptr = malloc(size); // 메모리 할당
        if (!ptr) throw bad_alloc(); // 할당 실패 시 예외 발생
        return ptr;
    }

    // 사용자 정의 delete 연산자
    void operator delete(void* ptr) 
    {
        cout << "Custom delete" << endl;
        free(ptr); // 메모리 해제
    }

    // 생성자
    MyClass(int val) : value(val) 
    {
        cout << "Constructor called with value: " << value << endl;
    }

    // 소멸자
    ~MyClass() 
    {
        cout << "Destructor called for value: " << value << endl;
    }
};

int main() 
{
    // 동적 객체 생성
    MyClass* obj = new MyClass(42);

    // 동적 객체 삭제
    delete obj;

    return 0;
}
```
