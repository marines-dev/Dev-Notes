# [C++] 제어문 : 범위 기반 for문

# 범위 기반 for문

범위 기반 for문은 컨테이너의 요소를 반복 실행할 수 있는 반복문이다. 첫번째 요소부터 마지막 요소까지 요소의 변수를 통해 접근하여 순회한다.

- 기본 문법

```cpp
for(자료형 변수이름 : 컨테이너이름)
{
	// 반복 구문;
}
```

**예제1) 범위 기반 for문 사용하여 배열 순회하기**

```cpp
#include <iostream>

int main() {
    int numbers[] = {10, 20, 30, 40, 50};

    for (int num : numbers) 
    {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    for (int& num : numbers) 
    {
        num *= 2;
    }

    for (const int num : numbers) 
    {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```