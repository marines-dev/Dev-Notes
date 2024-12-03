# [C++] 연산자 다중 정의(Operator Overloading)

# 연산자 다중 정의

연산자 함수로 지원 가능한 기존 연산자에 operator  키워드를 붙여 연산자 함수를 다중 정의하면 다른 기능을 추가하여 연산자를 이용하듯이 호출할 수 있으며, 클래스와 같은 객체도 연산을 할 수 있게 된다. 연산자 함수 정의 시 주의할 점은 기본 연산자의 기능을 변경하는 등의 본래의 의도를 벗어난 형태의 연산자 함수는 사용하지 않도록 하며, 연산자 함수를 만들어도 연산자의 우선순위와 결합성은 변하지 않는다. 또한 논리 연산자는 심각한 논리적 오류를 발생시킬 수 있기 때문에 논리 연산자 함수를 사용해서는 안된다.

### **연산자 다중 정의하기**

**멤버 함수로 연산자 다중 정의하기**

멤버함수로만 다중 정의가 가능한 연산자는 =(대입 연산자), ()(함수 호출 연산자). [](배열 접근 연산자). →(멤버 접근 포인터 연산자)이다.

- 사용 형식 : *객체이름* . operator *연산자* (*매개객체*);

**전역함수로 연산자 다중 정의하기**

곱셈의 교환 법칙의 성립을 구현을 해야 하는 등의 전역 함수로 연산자 다중 정의를 해야하는 경우도 있는데, 클래스의 private 멤버에 접근하기 위해서 friend 키워드를 붙여준다.

- 사용 형식 : friend operator *연산자* (*매개객체*);

ex) C cCpy= 8*cPos ;

- 멤버함수의 경우 불가능 : 8.operator*(cPos) //이러한 특별한 경우가 아니라면 멤버함수로 연산자 오버로딩을 하는 것이 좋다.
- 전역함수의 경우 가능 : operator*(8, cPos)

<aside>
💡 **다중 정의가 불가능한 연산자**

- . (멤버 접근 연산자)
- .* (멤버 포인터 연산자)
- :: (범위 지정 연산자)
- ?: (조건 연산자, 3항 연산자)
- typeid (RTTI 관련 연산자)
- sizeof (바이트 단위 크기 연산자)
- static_cast (형 변환 연산자)
- dynamic_cast (형 변환 연산자)
- const_cast (형 변환 연산자)
- reinterpret_cast (형 변환 연산자)
</aside>

**산술 연산자로 다중 정의하기**

+, -, *, / 등 산술 연산자들을 다양한 형식에 맞는 연산자 함수를 정의해 오버로딩할 수 있다.

ex) C_OVERLOAD + int 형식

C_OVERLOAD operator+ (int nParam);

**예제1) 연산자 다중 정의와 이동 생성자 호출 시점**

```arduino
#include "stdafx.h"

classC_TEST
{
	private:
		int m_nData = 0;
	public:
		//변환 생성자C_TEST(int nParam) :
		m_nData(nParam)
		{
				printf("C_TEST(int)\n");
		}

		//복사 생성자C_TEST(const C_TEST &rParam) :
		m_nData(rParam.m_nData)
		{
				printf("C_TEST(const C_TEST &)\n");
		}

		//이동 생성자C_TEST(const C_TEST &&rParam) :
		m_nData(rParam.m_nData)
		{
				printf("C_TEST(const C_TEST &&)\n");
		}

		//형 변환operatorint()
		{
				return m_nData;
		}

		//+
		C_TESToperator+(const C_TEST &rParam)//C_TEST형식을 반환하므로 이동 생성자가 호출된다.
		{
				printf("operator+\n");
				C_TESTcResult(0);
				cResult.m_nData =this->m_nData + rParam.m_nData;

				return cResult;
		}

		//=
		C_TEST&operator=(const C_TEST &rParam)
		{
				printf("operator=\n");
				m_nData = rParam.m_nData;

				return *this;
		}
};

int main()
{
		printf("*****Begin*****\n");
		C_TESTcA(0);
		C_TESTcB(3);
		C_TESTcC(4);

		//cB+cC 연산을 실행하면 이름 없는 임시 객체가 만들어지며 a에 대입하는 것은 임시 객체이다.
		cA = cB + cC;
		printf("%d\n", cA);
		printf("*****End*****\n");

		return 0;
}
```

![https://blog.kakaocdn.net/dn/earzkv/btqxJlRCwCx/g0Eks9ctwRpv4MIgp0U9C1/img.png](https://blog.kakaocdn.net/dn/earzkv/btqxJlRCwCx/g0Eks9ctwRpv4MIgp0U9C1/img.png)

cA = cB + cC;

//이 임시객체는 대입 연산 직후 소멸한다.

cA.operator = cB.operator(cC); //C_TEST& operator=(const C_TEST &rParam)가 호출된다.

### 단항 연산자 다중 정의

대표적으로 증감 연산자(++,--) 가 있다.

· 전위 연산자 사용 형식 : const 클래스형 & operator 증감연산자 ();

않은 멤버함수의 호출이 불가능하다.

ex) (cPos++)++;

(cPos--)--;

//후위증가 및 후위 감소 연산에 대해서의 컴파일 에러를 일으키기 위함이다.

++(++cPos);

- -(--cPos);

//가능

**대입 연산자 다중 정의**

디폴트 대입 연산자

· 디폴트 대입연산자는 멤버 대 멤버 복사(얕은 복사)를 진행한다.

· 복사생성자와 많이 유사하다. 차이점은 객체의 생성 및 초기화가 진행이 된 후 두 객체 간의 대입연산 시에는

(ex) 복사생성자

C_TEST cTest2 = cTest1;

(ex) 대입연산자

C_TEST cTest2(7, 9);

- 디폴트 대입연산자의 문제점은 디폴트 복사생성자의 문제와 동일하다.

(ex)

{

int nLen = strlen(rPara[m_cName)+1;](http://m.name%29+1%3B/)

strcpy(name, rPara[m.m_cName);](http://m.m_cname%29%3B/)

return *this;

- 또한 자식 클래스의 대입연산자 정의에서 명시적으로 부모클래스의 대입연산자 호출문을 삽입하지 않으면 부모클래스의 대입연산자는 호출되지 않아 부모클래스의 멤버변수는 멤버 대 멤버의 복사 대상에서 제외된다.

(ex)

{

m_nNum3 = rPara[m.m_nNum3;](http://m.m_nnum3%3B/)

return *this;

//rParam은 C_SECOND 참조형이지만 C_FIRST형 참조자로 매개변수의 인자로 전달이 가능한 이유는 부모형 참조자는 부모 객체 또는 부모를 직접 또는 간접적으로 상속하는 모든 객체를 참조할 수 있기 때문이다.

### 관계 연산자 다중 정의

상등 및 부등 연산자와 비교 연산자를 관계 연산자라고 한다. 이 연산자들의 연산 결과로 생성되는 값의 형식은 int형

이다. //참이면 1 거짓이면 0

- 상등 연산자 오버로딩 형식 : int 클래스이름 :: operator== (const 클래스이름 &);
- 부등 연산자 오버로딩 형식 : int 클래스이름 :: operator!= (const 클래스이름 &);

### 배열 연산자 다중 정의

[]연산자 오버로딩은 연산의 기본 특성상 멤버함수 기반으로만 오버로딩하도록 제한되어 있다.

- 배열 클래스

ex) C_ARRAY cArray[2]; //cArray.operator[ ] (2);

클래스 배열의 길이를 반환하는 함수를 추가할 경우 배열의 값을 변경하지 못하도록 매개변수 형이 const로 선언된다. 그러나 operator[] 함수는 const 함수가 아니기 때문에 컴파일 에러가 발생한다.

- 상수형 참조(r-value로만 사용됨) 배열 연산자 오버로딩 형식 : 자료형 operator[] (자료형 배열개수) const;

new & delete 연산자 다중 정의

- new 연산자 다중 정의

ex)

{

return pData;

//new 연산자 오버로딩에서 할당된 객체의 주소 값을 클래스의 포인터형으로 형 변환해서 반환을 한다.

- delete 연산자 다중 정의
- delete 연산자 오버로딩 형식 : void operator delete (void * 객체);
- 소멸자는 오버로딩 된 함수가 호출되기 전에 호출이 되니 오버로딩 된 함수에서는 메모리 공간의 소멸을 책임져야한다.

void operator delete (void * adr)

delete [] adr;

### **포인터 연산자  다중 정의**

대표적인 포인터 연산은 ->(포인터가 가리키는 객체의 멤버에 접근), *(포인터가 가리키는 객체에 접근)이다.

일반적인 연산자 오버로딩과 차이가 없지만 피 연산자가 하나인 단항 연산자의 형태로 오버로딩 된다는 특징이 있다.

ex)

C_NUMBER cNum(20);

cNum.ShowData();

(*cNum) = 30; //(cNum.operator*())=30;

cNum->ShowData(); //(cNum.operator*()).ShowData();

(*cNum).showData(); //cNu[m.operator->()->ShowData();](http://m.operator-%3E%28%29-%3Eshowdata%28%29%3B/)

//[operator->](http://m.operator-%3E%28%29-%3Eshowdata%28%29%3B/)가 반환하는 것은 주소 값이니 이를 통한 멤버의 접근을 위해서 -> 연산자를 하나 더 추가시켜 해석한 것이다.

※ operator-> 함수는 클래스의 private로 선언된 변수의 주소 값을 반환하기 때문에 값을 변경할 수 있어 operator-> 함수로 구현해서는 안된다. 그렇기 때문에 스마트 포인터는 이 멤버함수를 const로 선언해서 참조는 가능하되 변경은 불가능하도록 해야 한다.

### **형 변환 연산자  다중 정의**

C++에서는 형 변환 연산자를 오버로딩하여 객체와 기본 자료형간의 대입이 가능하다.

ex) 기본 자료형 데이터를 객체로 형 변환

cNum = 30; //cNum = C_NUMBER(30); //임시 객체의 생성

cNum.operator=(C_NUMBER(30)); //임시 객체를 대상으로 대입 연산자의 호출

ex)객체를 기본 자료형으로 형 변환

operator int()

{

return m_nNum; //형 변환 연산자는 반환형을 명시하지 않는다. 하지만 return문에 의한 값의 반환은 가능하다.

}

C_NUMBER cNum2 = cNum1 +20;

//cNum1의 operator int 함수가 호출되어 반환되는 값 30과 20의 덧셈 연산이 진행되고 이 연산의 결과로 cNum2가

생성된다.