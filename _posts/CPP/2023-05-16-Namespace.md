---
title: "[C++] 네임스페이스(Namespace)"
excerpt: "네임스페이스(Namespace)"

categories:
- C++
tags:
- [C++]

toc: true
toc_sticky: true

date: 2023-05-16
last_modified_at: 2023-05-16
---
# 네임스페이스(Namespace)

네임스페이스는 코드에서 이름이 서로 충돌하는 문제를 해결하기 위해 나온 개념이다.

예를 들어 foo() 함수를 정의해서 코드를 작성하다가 외부 라이브러리를 추가했더니 거기에도 foo() 함수가 있는 경우가 있다. 이때 컴파일러는 foo()란 이름만 보고서는 어느 함수를 가리키는지 알 수 없다.

이럴 때 네임스페이스를 사용하면 어떤 이름이 어디에 속해 있는지 문맥을 정의할 수 있다.



**namespace.h**

```cpp
namespace mycode
{
    void foo();
}
```

네임스페이스는 이렇게 함수나 메서드의 선언뿐만 아니라 구현 부분도 묶을 수 있다. 예를 들어 foo() 함수의 구현 부분을 namespace.cpp에 작성할 때 네임스페이스를 지정하는 방법은 다음과 같다.



**namespace.cpp**

```cpp
#include <iostream>
#include "namespaces.h"

void mycode::foo()
{
    std::cout << "foo() called in the mycode namespace" << std::endl;
}
```

또는

```cpp
#include <iostream>
#include "namespaces.h"

namespace mycode
{
    void foo()
    {
        std::cout << "foo() called in the mycode namespace" << std::endl;
	}
}
```



이처럼 foo()를 mycode 네임스페이스 아래에 두면 외부 라이브러리에 foo()가 있더라도 서로 구분할 수 있다. 네임스페이스를 적용한 foo()를 호출하려면 ::(스코프 지정 연산자 scope resolution operator)를 이용하여 함수 이름 앞에 네임스페이스를 붙인다.

```cpp
mycode::foo(); // mycode 네임스페이스에 정의된 foo() 함수를 호출한다.
```

mycode 네임스페이스 블록 안에서 접근할 때는 네임스페이스를 접두어로 붙이지 않아도 된다. 이렇게 네임스페이스를 생략하면 코드의 가독성을 좀 더 높일 수 있다. 또한 **using 지시자**를 이용하면 **네임스페이스 접두어를 생략**할 수도 있다. 컴파일러는 using 지시자를 보면 그 뒤에 나오는 문장부터는 using에 지정된 네임스페이스에 속하는 것으로 처리한다.

```cpp
#include "namespaces.h"

using namespace mycode;

int main()
{
    foo();	// mycode::foo();와 같다.
    return 0;
}
```

이어지는 코드에서는 cout 앞에 네임스페이스 접두어를 생략해도 된다. 하지면 std 네임스페이스의 다른 항목을 사용하려면 네임스페이스 접두어를 붙여야 한다.

```cpp
using std::cout;
cout << "Hello, World!" << std::endl;
```



> **헤더파일 안에서는 절대로 using 문을 작성하면 안 된다.** 그러면 그 헤더 파일을 인클루드하는 모든 파일에서 using 문으로 지정한 방식으로 호출해야 한다.



## C++17 중첩된 네임스페이스

C++17에서는 중첩된 네임스페이스를 좀 더 쉽게 사용할 수 있도록 개선했다. 중첩된 네임스페이스란 네임스페이스 안에 있는 네임스페이스를 말한다. C++17 이전에는 다음과 같이 작성했다.

```cpp
namespace MyLibraries
{
    namespace Networking 
    {
        namespace FTP
        {
            /* ... */
        }
    }
}
```

C++17부터는 다음과 같이 간결해졌다.

```cpp
namespace MyLibraries::Netwrking::FTP
{
    /* ... */
}
```

네임스페이스 앨리어스를 사용하면 네임스페이스의 이름을 다르게 표현하거나 기존 이름을 좀 더 짧게 만들 수 있다.

```cpp
namespace MyFTP = MyLibraries::Networking::FTP;
```



#### 참고

> 마크 그레고리, 『전문가를 위한 C++(4판)』, 남기혁
>

