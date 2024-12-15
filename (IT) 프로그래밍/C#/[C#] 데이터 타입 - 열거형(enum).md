# [C#] 데이터 타입 : 열거형(enum)

<br><br>

# 열거형(enum)

enum 키워드를 붙인 열거형 타입은 상수를 의미있는 문자열로 대치하는 사용자 정의 타입이다. 이때, 상수에 따로 값을 대입하지 않으면 첫번째 값은 0이고, 명시적으로 값을 대입할 경우 다음 값부터 순서대로 1씩 증가하며, enum은 네임스페이스, 클래스에서만 선언될 수 있다. C#에는 #define으로 값 치환이 안되기 때문에 enum, const를 적극 활용해야 한다.

<br><br>

**enum 정의하기**

```csharp
enum *이름*
{
	*변수이름*,
	*변수이름,*
	...
}
```

<br><br>

**예제1) enum 타입 정의하고 사용하기**

```csharp
class Program
{
    enum Color
    {
        Red,   // 0
        Green,  // 1
        Blue = 5,  // 5
        Yellow  // 6
    }

    static void Main(string[] args)
    {
        Color color;
        color= Color.Blue;
        Console.WriteLine((int)color); //5
    }
}
```

<br><br>
<br><br>

---

# **flag enum**

enum 위에 [Flags] 키워드를 붙인 플래그 열거형은 열거형의 값을 비트 단위로 ****조합하여 사용할 수 있다. 플래그 열거형의 멤버들은 각 비트별로 값을 갖을 수 있는데, OR 연산자를 이용하여 하나의 enum 변수에 여러 값을 가질 수 있으며, AND 연산자를 이용하여 enum 변수가 특정 멤버를 포함하고 있는지 체크할 수 있다.

<br><br>

**[Flags] 특성 사용**

플래그 열거형은 `System.FlagsAttribute`를 적용하여 정의한다. 이 특성이 없어도 동작은 가능하지만, 적용하면 더 직관적이고 올바르게 사용할 수 있다.

<br><br>
<br><br>

**비트 필드를 사용**

열거형 값은 2의 거듭제곱(1, 2, 4, 8 등)으로 정의된다. 이를 통해 값들을 비트 단위로 조합할 수 있다.

<br><br>
<br><br>

**비트 연산 사용**:

- OR 연산 (|): 여러 값을 결합.
- AND 연산 (&): 특정 값이 설정되었는지 확인.
- NOT 연산 (~): 값을 반전.

<br><br>

**예제2) flag enum 타입 정의하고 사용하기**

```csharp
using System;

[Flags]
enum Permissions
{
    None        = 0,   // 아무 권한 없음
    Read        = 1,   // 읽기 권한
    Write       = 2,   // 쓰기 권한
    Execute     = 4,   // 실행 권한
    Delete      = 8,   // 삭제 권한
    FullControl = Read | Write | Execute | Delete // 모든 권한
}

class Program
{
    static void Main()
    {
        // 권한 설정
        Permissions userPermissions = Permissions.Read | Permissions.Write;

        Console.WriteLine("User Permissions: " + userPermissions); // 출력: Read, Write

        // 권한 추가
        userPermissions |= Permissions.Execute; // OR 연산으로 Execute 추가
        Console.WriteLine("Updated Permissions: " + userPermissions); // 출력: Read, Write, Execute

        // 특정 권한 확인
        bool canWrite = (userPermissions & Permissions.Write) == Permissions.Write;
        Console.WriteLine("Can Write: " + canWrite); // 출력: True

        // 권한 제거
        userPermissions &= ~Permissions.Write; // NOT 연산으로 Write 제거
        Console.WriteLine("After Removing Write: " + userPermissions); // 출력: Read, Execute

        // 특정 권한만 설정
        userPermissions = Permissions.Delete; // 단일 권한 설정
        Console.WriteLine("Final Permissions: " + userPermissions); // 출력: Delete
    }
}
```
