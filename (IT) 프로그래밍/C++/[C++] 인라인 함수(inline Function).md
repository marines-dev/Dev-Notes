# [C++] 인라인 함수(inline Function)

<br><br>

# 인라인 함수(inline)

일반 함수 호출 시 스택 메모리에 저장되고, 해당 함수의 메모리 주소로 이동하여 함수 내부에서 많은 연산이 발생한다.

그러나 함수의 정의는 짧은데 자주 사용되는 함수는 성능 저하에 있어 손실이 크기 때문에 이를 극복하고자 인라인 함수를 사용한다.

인라인 함수는 함수 앞에 inline 키워드를 붙이며, 메모리 주소를 따로 저장하지 않고 컴파일 시 함수 호출 위치에서 함수의 정의를 복사하기 때문에 성능이 향상될 수 있다. 

그러나 함수의 코드 길이가 일정 수준 이상 길어지면 오히려 사용하지 않는 것이 좋을 수도 있으며, 직접 인라인 함수로 정의하지 않아도 기본값으로 설정되어 있기 때문에 컴파일러가 자동으로 인라인 함수로 최적화하여 호출한다. 

이밖에 C언어의 매크로 함수도 일반 함수보다 성능이 좋지만 실질적으로 함수가 아니기 때문에 자료형도 지정할 수 없고, 복잡한 함수를 정의하는데 한계가 있다.

- 사용 형식 : inline *자료형 함수이름* (*매개변수*, *..*);

<br><br>

**예제1) inline 함수 사용하기**

```cpp
#include <stdio.h>
 
inline int AddFunc(int nNum)
{
    return nNum + nNum;
}

int main()
{
    printf("AddFunc(3) = %d\n", AddFunc(3)); //((3)+(3))으로 대체됨.
    printf("AddFunc(10) = %d\n", AddFunc(10)); //((10)+(10))으로 대체됨.
    return 0;
}
```

![https://blog.kakaocdn.net/dn/znbva/btqxG7Nlu1W/qHZsYPCvhqGC663LIbs4Vk/img.png](https://blog.kakaocdn.net/dn/znbva/btqxG7Nlu1W/qHZsYPCvhqGC663LIbs4Vk/img.png)

<br><br>

>[!note]
> **C++ 템플릿을 이용한 인라인 함수**
> 
> - 매크로 함수는 자료형에 의존적이지 않아 어떤 자료형의 데이터를 자유롭게 대입해도 데이터 손실이 발생하지 않는다.
> - 반면, 인라인 함수는 선언한 매개변수의 자료형과 함수 호출의 인수가 다를 경우 데이터 손실이 발생한다. 만약 함수의 오버로딩을 통해서 해결하게 되면 여러 개의 함수를 추가로 정의하게 되어 한번만 정의하면 되는 매크로 함수의 장점을 보안하지 못하게 된다. 이러한 문제를 보안하기 위해서 C++ 템플릿을 이용하여 자료형에 의존적이지 않은 인라인 함수를 선언하여 해결할 수 있다.
> 
> **예제2) 템플릿을 이용한 인라인 함수 사용하기**
> 
> ```cpp
> #include <stdio.h>
>  
> template <typename T>
> inline T AddFunc(T nNum)
> {
>     return nNum + nNum;
> }
>  
> int main()
> {
>     printf("((10) + (10)) = %d\n", AddFunc(10)); //int
>     printf("((12.3) + (12.3)) = %f\n", AddFunc(12.3f)); //float
>     return 0;
> }
> ```
> 
> ![https://blog.kakaocdn.net/dn/dnWH3z/btqxFTicQzh/xRTrBaBPKN4DyYHBFK4kpk/img.png](https://blog.kakaocdn.net/dn/dnWH3z/btqxFTicQzh/xRTrBaBPKN4DyYHBFK4kpk/img.png)
