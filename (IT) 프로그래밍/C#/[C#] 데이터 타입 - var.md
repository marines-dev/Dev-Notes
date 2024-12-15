# [C#] 데이터 타입 : var

# **var**

암시적 데이터 타입으로, 대입되는 값의 데이터 타입에 따라 컴파일러가 자동으로 해당 변수의 형식을 지정한다. var를 사용할 수 없는 경우는 매개변수, 클래스 멤버 변수, null 값으로 초기화, 연속적으로 초기화할 수 없으며, 지역변수로만 사용할 수 있다.

**var 선언하기**

```csharp
var *변수이름* = *값*;
```

**예제1) var 사용하기**

```csharp
using System;

class Program
{
    static void Main()
    {
        var number = 10;         // 컴파일러가 int로 추론
        var name = "John Doe";   // 컴파일러가 string으로 추론
        var isActive = true;     // 컴파일러가 bool로 추론

        Console.WriteLine($"Number: {number} ({number.GetType()})");
        Console.WriteLine($"Name: {name} ({name.GetType()})");
        Console.WriteLine($"Is Active: {isActive} ({isActive.GetType()})");
    }
}
```