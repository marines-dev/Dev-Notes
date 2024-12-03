# [C++] 네임스페이스(namespace)

<br><br>

# 네임스페이스(namespace)

프로그램의 규모가 커지고 변수, 함수, 클래스 등의 이름 중복이 발생할 확률이 잦아졌다. 이러한 이름의 중복을 막기 위해 namespace 키워드로 새로운 이름을 붙여서 한 소속으로 사용할 수 있도록 이름 공간이라는 네임스페이스 기능을 제공한다. 또한 네임스페이스 안에 또 다른 네임스페이스를 중첩할 수도 있다.

<br><br>

### **네임스페이스 정의하기**

```cpp
namespace 네임스페이스이름
{
	…
}
```

<br><br>
<br><br>

### **네임스페이스 사용하기**

:: 범위 지정 연산자를 이용하여 네임스페이스를 지정한다. 또한 직역 변수와 전역 변수의 이름이 동일할 때 전역 변수 이름 앞에 범위지정 연산자를 사용하면 지역 변수와 전역 변수를 구분해서 사용할 수 있다.

```cpp
네임스페이스이름::네임스페이스이름:: ... ::변수∙함수∙클래스이름;
```

<br><br>

**예제1) 네임스페이스로 지역 변수와 전역 변수 구별하기**

```cpp
#include<stdio.h>
int nNum=100; //전역 변수

int main()
{
	int nNum = 50; //지역 변수
	printf("%d\n",nNum); //지역 변수 50 출력
	printf("%d\n",::nNum); //전역 변수 100 출력

	return 0;
}
```

<br><br>

>[!tip]
> **네임스페이스 중첩**
> 
> 네임스페이스의 중첩이 많을 경우 또다시 하나의 새로운 네임스페이스로 만들 수도 있다.
> 
> - namespace *네임스페이스이름* = *기존네임스페이스*::*기존네임스페이스* … ;
> 
> ex) namespace Namespace123 = Namespace1::Namespace2::Namespace3;

<br><br>

>[!note]
> **using**
> 
> namespace를 지정한 변수, 함수, 클래스 등을 자주 사용할 경우 using 키워드를 사용해 네임스페이스를 미리 선언하면 네임스페이스를 생략할 수 있다. 주의할 점은 using을 사용할 경우 또 다시 상대적으로 이름 중복이 발생할 확률이 높아지기 때문에 적절하게 판단하여 사용해야 한다.
> 
> - using namespace *네임스페이스이름*;
> 
> **예제2) using으로 네임스페이스 생략하기**
> 
> ```cpp
> #include<stdio.h>
> 
> namespace SkipTest
> {
>     void TestFunc(); //함수 선언
> }
>  
> int main()
> {
>     using namespace SkipTest;
>  
>     TestFunc();
>     return 0;
> }
>  
> void SkipTest::TestFunc() //함수 정의
> {
>     printf("SkipTest::TestFunc()\n");
> }
> ```
> 
> ![https://blog.kakaocdn.net/dn/dPGlcX/btqxHC0sY3v/jIxjIVDQAYCAZcM4vqFyKK/img.png](https://blog.kakaocdn.net/dn/dPGlcX/btqxHC0sY3v/jIxjIVDQAYCAZcM4vqFyKK/img.png)
