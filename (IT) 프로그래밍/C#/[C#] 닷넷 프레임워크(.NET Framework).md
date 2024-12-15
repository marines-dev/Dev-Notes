# [C#] 닷넷 프레임워크(.NET Framework)

Status: Done

# **닷넷 프레임워크(.NET Framework)**

마이크로소프트에서 개발한 윈도우 프로그램 개발 환경으로, 많은 작업을 캡슐화하여 클래스 라이브러리를 제공한다. CLR에서 작동하며 부가적인 실행 파일로는 C#, VB.NET 컴파일러, 유틸리티의 실행 파일이 있다. 마이크로소프트는 이렇게 여러가지의 클래스 라이브러리를 하나의 패키지로 묶어 배포한다. 또한, 닷넷 프레임워크가 운영체제 안으로 들어가 한 부분으로 자리 잡으면서 C# 프로그래밍을 이용해 운영체제하고 긴밀하게 데이터를 주고 받아 결과를 얻어낼 수 있다.

### **클래스 라이브러리 종류**

닷넷의 클레스 라이브러리에는 BCL, Window Form, ASP.NET, ADO.NET, CLR, CTS, CLS, CLI, CIL이 있다.

**BCL(Basic Class Library)**

마이크로소프트는 특정 기능을 수행하는 타입을 미리 만들어 놓은 기본 클래스를 제공한다.

**Window Form**

윈도우 응용 프로그램 제작을 위한 클래스 라이브러리이다.

**ASP.NET**

웹 클래스 라이브러리이다.

**ADO.NET**

데이터베이스 클래스 라이브러리이다.

**CLR(Common Language Runtime)**

닷넷 프레임워크의 하나의 모듈인 공용 언어 런타임이다.

클래스 라이브러리를 이용해 비주얼스튜디오에서 컴파일한 파일을 빌드해서 CLR에 보내주면 코드를 다시 운영체제에 맞게끔 재컴파일해서 C# 코드를 실행하는 역할을 한다. 그러면 운영체제에서 하드웨어를 다루기 때문에 하드웨어와 상관없이 접근이 가능하다. 

CLR에는 두 가지 큰 기능이 있는데, 가비지 수집기(Garbage Collector)를 제공해 동적 메모리 할당, 회수를 지원하고, 중간 언어를 JIT 컴파일러를 이용해 기계어로 변환한다.

![https://blog.kakaocdn.net/dn/cyX5dH/btq11LBG29X/rOz4Zukjyev8WDqtak2RP1/img.png](https://blog.kakaocdn.net/dn/cyX5dH/btq11LBG29X/rOz4Zukjyev8WDqtak2RP1/img.png)

**CTS(Common Type System)**

- 닷넷 호환 언어가 지켜야 할 타입의 표준 규격을 정의한 공용 타입 시스템이다.
- 만약에 새로운 언어를 만들어 닷넷 프레임워크 상에서 실행하고 싶다면 CTS 규약을 만족하는 한도 내에서만 구현할 수 있다.

**CLS(Common Language Specification)**

- 닷넷 호환 언어가 지켜야 할 최소한의 언어 사양으 정의한 공용 언어 사양이다.

ex) int -> System.Int32

float -> System.Single

**CLI(Common Languge Infracstructure)**

- 마이크로소프트에서 ECMA 표준의 공용 언어 기반 구조로 제출한 공개 규약이다.
- CLI는 CTS 명세를 포함하며, 중간 언어에 대한 코드 정의와 메타 데이터를 포함하는 이진 파일의 구조까지 표준 사양으로 기술하고 있다.

<aside>
💡 **메타 데이터**

- 프로그래밍 언어에서는 코드가 데이터에 해당하고, 해당 코드의 성격을 설명해 주는 별도의 데이터가 메타 데이터이다.
- CLR에서 동작하는 실행 파일은 완전하게 자기 서술적인 메타 데이터를 제공하며, 외부에서는 이런 정보를 리플렉션(Reflectiom)이라는 기술을 통해 사용할 수 있다.
- 따라서 직접 닷넷 호환 언어를 만들어 컴파일러를 제공한다면 중간 언어 코드와 함께 메타 데이터도 생성해야 한다. 마찬가지로 C#언어로 컴파일된 EXE/DLL 파일에도 메타 데이터가 담겨 있다.
</aside>

ex) 닷넷 프레임워크 구조

![[https://ko.wikipedia.org/wiki/닷넷_프레임워크](https://ko.wikipedia.org/wiki/%EB%8B%B7%EB%84%B7_%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC)](https://blog.kakaocdn.net/dn/lOyAc/btq11AAk0xu/gkL5TiUYXovmxXxR2oAN5k/img.png)

[https://ko.wikipedia.org/wiki/닷넷_프레임워크](https://ko.wikipedia.org/wiki/%EB%8B%B7%EB%84%B7_%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC)

**CIL(Common Intermediate Language)**

- 닷넷 언어인 VB, C# 등의 공통 중간 언어로, CLR에서는 CIL이라고 하며, 보통은 줄여서 IL 코드라고 한다.
- IL 코드는 일대일 대응되는 IL 언어가 따로 있고, 가상 머신에서 실행되기 때문에 일종의 기계어와 유사하며, ILASM.EXE라는 컴파일러를 가지고 있다.
- 모든 닷넷 호환 언어는 CPU에 독립적인 결과물로서 소스 코드를 IL 코드로 컴파일하고, IL 코드를 CLR에서 기계어로 최종 번역하는 것이다.

## **C#**

마이크로소프트에서 개발되었으며, 닷넷 프레임워크를 이용하여 프로그래밍하는 객체 지향 프로그래밍 언어로, 윈도우 프로그래밍, 웹 프로그래밍, 게임, 모바일 프로그래밍 등 모든 영역에서 사용되는 범용 프로그래밍 언어이다.

### **C# 프로그램 실행과정**

C#언어 → 컴파일(비주얼스튜디오) → MSIL(*.exe, 결과물) → CLR 실행(최종적으로는 OS와 상관없이 실행된다.)