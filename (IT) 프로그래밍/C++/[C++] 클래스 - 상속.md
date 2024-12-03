# [C++] 클래스 : 상속

<br><br>

# 상속

클래스(파생 클래스)가 다른 클래스(부모 클래스)를 물려받아 부모 클래스의 public과 protected의 멤버에 접근이 가능하여 클래스 간의 계층적인 구조를 갖게되는데, 상속은 프로그램의 변경 요구에 대처가 가능한 유연성과 필요한 기능을 추가하는 확장성을 가진다. 그리고 자식 클래스의 객체 생성 시 부모 클래스의 생성자가 호출된 후 자식클래스의 생성자가 호출된 다음 객체가 생성된다. 

<br><br>

### 기본 문법

 상속 시 접근 제어 지시자는 다중 상속과 같이 특별한 경우가 아니면 public 선언 이외에 잘 사용하지 않는다. 

```cpp
class *자식클래스이름* : *접근제어지시자 부모클래스이름*
{

};
```

<br><br>

**예제1) 클래스 상속하기**

```cpp
#include <stdio.h>

class C_PARENTS
{
private:
	int m_nData;

public:
	C_PARENTS() :
		m_nData(0)
	{
			printf("C_PARENTS()\n");
	}

voidSetData(int nParam)
	{
			m_nData = nParam;
	}

intGetData()const
	{
			return m_nData;
	}

protected:
	voidPrintData()
	{
			printf("C_PARENTS:: PrintData()\n");
	}
};

classC_CHILD :public C_PARENTS
{
public:
	C_CHILD()
	{
			printf("C_CHILD()\n");
	}

voidTestFunc()
	{
			PrintData();// 부모 클래스의 protected 멤버SetData(30);
			printf("%d\n", C_PARENTS::GetData());
	}

};

int main()
{
		C_CHILD cData;
		//부모 클래스 멤버 호출
		cData.SetData(15);
		printf("%d\n", cData.GetData());
	
		//자식 클래스 멤버 호출
		cData.TestFunc();
	
		return 0;
}
```

![https://blog.kakaocdn.net/dn/smGAH/btqxHThMhOw/JTk9Ur8kGG3a8bdkoMj6Dk/img.png](https://blog.kakaocdn.net/dn/smGAH/btqxHThMhOw/JTk9Ur8kGG3a8bdkoMj6Dk/img.png)

<br><br>
<br><br>

### **함수 재정의(Function Overriding)**

자식 클래스는 상속한 부모 클래스의 메서드를 동일한 이름으로 재정의할 수 있는데, 자식 클래스의 객체를 사용할 때 별다른 언급을 하지 않으면 재정의된 메서드가 기존 메서드를 대체하여 호출된다. 주의할 점은 부모 클래스의 메서드가 자식 클래스에 재정의하면 부모 클래스에서 사용하는 메서드도  자식 클래스에 재정의해야 한다. 또한 추상 자료형으로 포인터 변수를 선언해서 추상 자료형에 따라서 호출되는 메서드의 종류가 달라지면 메서드 재정의에 의미가 없어지기 때문에 가상 함수를 사용해야 한다.

<br><br>
<br><br>

### 가상 함수(virtual)

부모 클래스의 함수에 virtual 키워드를 붙이면 가상 함수로 선언이 되고, 자식 클래스에서 재정의한 함수도 가상 함수가 된다. (자식 클래스에는 virtual 선언을 추가하지 않아도 가상 함수가 되지만 virtual 선언을 넣어서 함수가 가상 함수임을 알리는 것이 좋다.)

- 사용 형식 : virtual *자료형 함수이름*;

<br><br>

>[!note]
> **final 키워드**
> 
> 상속에서 부모 클래스의 가상 함수가 재정의 되는 것을 막아야할 경우 가상 함수 뒤에 final 키워드를 붙이면 자식 클래스에서 해당 함수를 재정의할 수 없게 된다.
> 
> - 사용 형식 : virtual *자료형 함수이름*() final;

<br><br>

>[!note]
> **가상 소멸자**
> 
> 부모 클래스로 추상 자료형의 객체를 생성하여 동적 할당한 자식 객체를 참조할 경우 가상 함수는 자식 클래스에서 할당받지만 소멸자는 부모 클래스 소멸자가 호출되어 메모리 누수가 발생하게 된다. 자식 클래스의 가상 함수를 해제를 하기 위해서 부모 클래스의 소멸자도 virtual 키워드를 붙여서 가상 소멸자로 선언해서 해제할 수 있도록 한다. 이렇게 가상 소멸자가 호출되면 상속의 계층 구조상 맨 아래에 존재하는 유도 클래스의 소멸자가 대신 호출되면서 부모 클래스의 소멸자가 순차적으로 호출된다. 그러므로 부모 클래스에서 가상 함수로 선언하면 사용자 코드에서 추상 자료형 사용을 대비하여 소멸자도 가상 소멸자로 선언해야 한다.
> 
> **예제2) 가상 소멸자 사용하기**
> 
> ```cpp
> #include <stdio.h>
> #include <cstring>
> 
> classC_FIRST
> {
> private:
> char * m_pstrOne;
> 
> public:
> 	C_FIRST(constchar * pstrOne)
> 	{
> 			m_pstrOne =newchar [strlen(pstrOne) + 1];
> 	}
> virtual ~C_FIRST()
> 	{
> 			printf("~C_FIRST()\n");
> 			delete[] m_pstrOne;
> 	}
> 
> };
> 
> classC_SECOND :public C_FIRST
> {
> private:
> 	char * m_pstrTwo;
> 
> public:
> 	C_SECOND(constchar * cstrOne,constchar * cstrTwo) :
> 		C_FIRST(cstrOne)
> 	{
> 			m_pstrTwo =newchar[strlen(cstrTwo) + 1];
> 	}
> 
> virtual ~C_SECOND()
> 	{
> 			printf("~C_SECOND()\n");
> 			delete[] m_pstrTwo;
> 	}
> };
> intmain()
> {
> 		C_FIRST * c_pFirst =new C_SECOND("simple", "complex");
> 
> 		delete c_pFirst;
> 
> 		return 0;
> }
> ```
> 
> ![https://blog.kakaocdn.net/dn/NBLkr/btqxNVr4bAf/E1nENGhfekCGW7FvcbL9bK/img.png](https://blog.kakaocdn.net/dn/NBLkr/btqxNVr4bAf/E1nENGhfekCGW7FvcbL9bK/img.png)

<br><br>
<br><br>

### 순수 가상 함수

부모 클래스에서 순수 가상 함수로 선언하면 객체의 사용을 막을 수 있으며, 자식 클래스는 부모 클래스의 가상 함수를 정의하지 않아도 된다.

- 사용 형식 : virtual *자료형 함수이름* = 0;

<br><br>
<br><br>

### 순수 가상 클래스

부모 클래스가 멤버 함수를 하나 이상의 순수 가상 함수로 가지면 순수 가상 클래스 또는 추상 클래스라고 하며, 추상 클래스의 자식 클래스는 반드시 순수 가상 함수를 재정의 해야한다. 추상 클래스는 객체 생성과 동적 할당이 불가능하며, 추상 자료형으로만 선언할 수 있다. 

<br><br>

>[!note]
> **순수 가상 클래스의 효율성**
> 
> 빠른 연산이 필요한 경우 switch 문, if 문을 사용하는 것은 매우 비효율적이다.
> 
> 상대적으로 여유로운 순간은 '사용자 입력'의 순간인데 switch 문 같은 느린 연산을 사용자 입력 시점에서 분류해 적절한 객체를 생성하여 수행하는 것이 좋고 출력하는 부분은 추상 자료형으로 순수 가상 함수를 호출하여 즉시 실행할 수 있어 최적화할 수 있다. 그래서 할 수 있다면 중첩 if문이나 switch문은 'Lookup 배열' 혹은 추상 자료형을 이용한 방법으로 변경해야 한다.
> 
> **예제3) 추상 자료형의 효율성**
> 
> ```cpp
> #include <stdio.h>
> #define DEFAULT_FALE	1000
> 
> class C_PERSON
> {
> protected:
> 	unsigned int m_nFare = 0;
> 
> public:
> 	C_PERSON()
> 	{
> 
> 	}
> 
> 	virtual ~C_PERSON()
> 	{
> 		printf("virtual ~C_PERSON()\n");
> 	}
> 
> 	//요금 계산 인터페이스
> 	virtual void CalcFare() = 0;
> 
> 	virtual unsigned int GetFare()
> 	{
> 		return m_nFare;
> 	}
> };
> 
> //초기 혹은 후기 제작자
> class C_BABY : public C_PERSON
> {
> public:
> 		//영유야(0~7세) 요금 계산
> 		virtual void CalcFare()
> 	{
> 		m_nFare = 0; //0%
> 	}
> 		
> };
> 
> class C_CHILD : public C_PERSON
> {
> public:
> 	// 어린이(8~13세) 요금 계산
> 	virtual void CalcFare()
> 	{
> 		m_nFare = DEFAULT_FALE * 50 / 100; //50%
> 	}
> };
> 
> class C_TEEN : public C_PERSON
> {
> public:
> 	//청소년(14~19세) 요금 계산
> 	virtual void CalcFare()
> 	{
> 		m_nFare = DEFAULT_FALE * 75 / 100; //75%
> 	}
> };
> 
> class C_ADULT : public C_PERSON
> {
> 	//성인(20세 이상) 요금 계산
> 	virtual void CalcFare()
> 	{
> 		m_nFare = DEFAULT_FALE; //100%
> 	}
> };
> 
> int main()
> {
> 	C_PERSON * carList[3] = {};//추상 클래스는 추상 자료형으로 선언이 가능하다.
> 	int nAge = 0;
> 
> 	//1. 자료 입력 : 사용자 입력에 따라서 생성할 객체 선택
> 	for (auto &C_PERSON : carList)
> 	{
> 		printf("나이를 입력하세요 : ");
> 		scanf_s("%d", &nAge);
> 
> 		if (nAge < 8)
> 		{
> 			C_PERSON = new C_BABY;
> 		}
> 
> 		else if (nAge < 14)
> 		{
> 			C_PERSON = new C_CHILD;
> 		}
> 
> 		else if (nAge < 20)
> 		{
> 			C_PERSON = new C_TEEN;
> 		}
> 		else
> 		{
> 			C_PERSON = new C_ADULT;
> 		}
> 
> 		C_PERSON->CalcFare();
> 	}
> 
> 	//2.자료 출력 : 계산한 요금을 활용하는 부분
> 	for (auto C_PERSON : carList)
> 	{
> 		printf("%d원\n", C_PERSON->GetFare());
> 	}
> 
> 	//3.자료 삭제 및 종료
> 	for (auto C_PERSON : carList)
> 	{
> 		delete C_PERSON;
> 	}
>     return 0;
> }
> //객체에 맞는 함수를 호출하여 생성된 객체가 무엇인지에 따라 요금을 계산한다. 왜냐하면 가상함수는 사용자 입력에 따라 실제로 생성된 실형식의 함수가 호출되기 때문이다. 따라서 추상 자료형을 이용하면 경우의 수가 아무리 늘어난다 하더라도 똑같은 부하 수준으로 모두 대응할 수 있어 한 줄의 코드가 다중 if문이나 switch문을 대체하게 된다.
> ```
> 
> ![https://blog.kakaocdn.net/dn/cbzbNM/btqxLcBAEz1/oZgQBF0neuzgZpMwLYw5P1/img.png](https://blog.kakaocdn.net/dn/cbzbNM/btqxLcBAEz1/oZgQBF0neuzgZpMwLYw5P1/img.png)

<br><br>
<br><br>

### 가상 함수 테이블

객체 지향 특징에 객체 내에 멤버 함수가 존재하지만 실제 메모리의 한 공간에 별도로 위치하고 이 함수가 정의된 클래스의 모든 객체가 이를 함수 포인터로 공유하는 형태이다. 그리고 객체의 멤버 변수 연산이 진행되도록 함수를 호츨한다. 가상 함수가 한 개 이상 포함하는 클래스에서는 컴파일러가 가상 함수 테이블을 생성한다. 이러한 가상 함수 테이블은 V table이라고도 한다. 이는 실제 호출되어야할 가상 함수의 주소를 저장하고 있는 테이블로 배열 형태로 이루어져 있다. 가상 함수를 선언하면 객체의 생성과 상관없이 가상 함수 테이블 메모리 공간에 할당되는데 이는 가상 함수 테이블이 멤버 함수의 호출에 사용되는 데이터이기 때문이다. 그리고 객체가 생성되면 부모 클래스 객체에는 부모 클래스의 V table 포인터에 주소값이 저장되고 자식 클래스 객체에는 자식 클래스의 V table 포인터에 주소값이 저장된다. 이렇게 되면 가상 함수 테이블의 포인터가 가상 함수 주소에 배열 형태로 접근할 수 있는데 이 포인터의 주소는 자식 클래스 생성자가 호출되면 자식 클래스의 V table로 변경된다. 그렇기 때문에 오버라이딩된 가상 함수를 호출하면 가장 마지막에 오버라이딩한 자식클래스의 멤버 함수가 호출되는 것이다.

<br><br>
<br><br>

### 다중 상속

둘 이상의 부모 클래스를 동시에 상속하여 쉽게 부모 클래스의 멤버를 자식 클래스에 모아 새로운 객체를 정의할 수도 있다.

그러나 자식 클래스에서 상속하고 있는 여러 부모 클래스에 동일한 형태의 멤버가 존재하는 경우 자식 클래스에서 부모 클래스의 이름을 명시하여 호출하여야 한다. 이밖에도 다중 상속은 심각한 설계 오류와 다양한 문제를 발생시킬 수 있기 때문에 굳이 사용하지 말자.

ex) cChild.C_PARENTA::PrintData();

cChild.C_PARENTB::PrintData();

<br><br>

>[!note]
> **인터페이스 클래스**
> 
> 인터페이스 클래스는 말 그대로 인터페이스만 갖는 클래스이다. 자식 클래스는 부모 클래스를 다중 상속하여 부모 클래스가 선언한 순수 가상함수들을 모두 재정의할 수 있다. 이렇게 하면 자식 클래스의 인스턴스는 부모 클래스가 가진 인터페이스를 모두 제공하하게 된다. 사용자는 이 인터페이스들을 활용해 좀 더 쉽게 객체를 사용할 수 있다. 이 경우가 다중 상속을 사용해도 되는 유일한 상황이지만 다중 상속은 좋지 않다. (제작자는 연산자 다중정의와 마찬가지로 다양한 인터페이스에 맞추어 모든 메서드를 다 정의해야만 한다.)

<br><br>
<br><br>

### 가상 상속

다중 상속한 부모 클래스들이 동시에 상위 클래스를 상속할 경우 부모클래스의 자식 클래스는 최종 상위 클래스를 간접적으로 두 번 상속하게 되면서 최종 상위 클래스의 멤버를 동시에 두 개를 갖는형태가 되어 모호성이 발생한다. 그래서 부모 클래스에 virtual 예약어로 가상 상속을 적용하여 해결할 수 있다. 이렇게 하게되면 자식클래스에는 최종 클래스의 멤버가 하나씩만 존재하게 된다. 그래서 부모클래스의 이름을 명시하지 않고도 멤버 함수 이름만 가지고 호출할 수 있으며 최종 클래스의 생성자는 한번만 호출된다. 그러나 만약 A부모클래스에서 상위 클래스 멤버 값을 변경했는데 그것을 B 부모 클래에서 접근해 수정한다면 문제는 해결되지 않는다. 그러므로 다중 상속은 사용하지 않는 것이 좋다.

ex)

class C_PARENTB : virtual public C_PARENTA

class C_PARENTC : virtual public C_PARENTA

class C_CHIRD : public C_PARENTB, public C_PARENTC
