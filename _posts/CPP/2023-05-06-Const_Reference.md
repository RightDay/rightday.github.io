---
title: "[C++] Const & Reference"
excerpt: "Const & Reference"

categories:
- C++
tags:
- [C++]

toc: true
toc_sticky: true

date: 2023-05-06
last_modified_at: 2023-05-06
---
# Const

## const 상수

값을 상수로 선언할 수 있게 해주는 키워드이다.

C 언어에서는 전처리 구문인 #define을 사용했지만 C++에서는 상수를 #define 대신 const로 정의하는 것이 바람직하다.

> #define은 전처리기가 처리하고, const는 컴파일러가 처리한다. const로 정의할 대상에 타입이나 스코프를 적용할 수 있다는 장점이 있다.

``` c++
const int versionNumberMajor = 2;
const int versionNumberMinor = 1;
const std::string productName = "Super Hyper Net Modulator";
```



## const 매개변수

C++에서는 non-const 변수를 const 변수로 캐스팅할 수 있다. 이렇게 하면 다른 코드에서 변수를 변경하지 않도록 어느정도 보호할 수 있다.

const 매개변수로 구성된 함수안에서 매개변수의 값을 변경하면 컴파일 오류가 발생한다.

```cpp
void mysteryFunction(const std::string* someString)
{
    *someString = "Test"; // 이 부분에서 컴파일 에러가 발생한다.
}

int main()
{
    std::string myString = "The string";
    myteryFunction(&myString);
    return 0;
}
```



# Reference

C++에서 제공하는 레퍼런스(참조)를 사용하면 기존 변수에 새 이름을 지정할 수 있다.

```cpp
int x = 42;
int & xReference = x;
```

변수의 타입 뒤에 &를 붙이면 그 변수는 레퍼런스가 된다. 코드에서 다루는 방법은 일반 변수와 같지만 내부적으로는 원본 변수에 대한 포인터로 취급한다. 앞에 나온 에에서 일반 변수 x와 레퍼런스 변수 xReference는 모두 같은 값을 가리킨다. 둘 중 한 변수에서 값을 변경하면 그 결과가 다른 변수에도 반영된다.

## 레퍼런스 전달 방식

일반적으로 함수에 전달한 변수는 **값 전달 방식**으로 처리한다. 예를 들어 함수의 매개변수에 정수를 전달하면 함수 안에는 그 정수의 **복제본**이 전달된다. 따라서 **함수 안에서 원본 변수의 값을 변경할 수 없다.** C에서는 스택 변수에 대한 포인터를 자주 사용했는데, 이런 방식을 사용하면 다른 스택 프레임에 있는 원본 변수를 수정할 수 있다. 이러한 포인터를 역참조하면 그 포인터가 현재 스택 프레임을 가리키지 않더라도 함수 안에서 그 변수가 가리키는 메모리의 값을 수정할 수 있지만, 포인터 연산이 많아져서 간단한 작업도 코드가 복잡해지는 단점이 있다.

C++에서는 값 전달 방식보다 뛰어난 **레퍼런스(참조) 전달 방식**을 제공한다.

```cpp
void addOne(int i)
{
    i++;	// 복제본이 전달됐기 때문에 원본에는 아무런 영향을 미치지 않는다.
}

void addOne(int& i)
{
    i++;	//원본 변수가 변경된다.
}
```

정수 타입에 대한 레퍼런스를 받는 함수를 호출하는 문장을 작성하는 방식은 정숫값을 받는 함수를 호출할 때와 똑같다.

```cpp
int myInt = 7;
addOne(myInt);
```

## const 레퍼런스 전달 방식

const 레퍼런스의 가장 큰 장점은 성능이다. 함수에 매개변수를 값으로 전달하면 그 값 전체가 복제된다. 하지만 레퍼런스로 전달하면 **원본에 대한 포인터만 전달되기 때문에 원본 전체를 복제할 필요가 없다.** 또한 const 레퍼런스로 전달하면 **복제되지도 않고 원본 변수가 변경되지도 않는 장점**을 모두 취할 수 있다.

const 레퍼런스는 특히 **객체**를 다룰 때 유용하다. 객체는 대체로 커서 복제하는 동안 의도하지 않은 효과를 발생할 수 있기 때문이다.

```cpp
void printString(const std::string& myString)
{
    std::cout << myString << std::endl;
}

int main()
{
    std::string someString = "Hello World";
    printString(someString);
    printString("Hello World");	//리터럴을 전달해도 된다.
    return 0;
}
```

> 함수에 객체를 전달할 때 값으로 전달하기보다는 const 레퍼런스로 전달하는 것이 좋다. 그러면 불필요한 복제 작업을 피할 수 있다. 전달할 객체를 함수 안에서 수정하려면 non-const 레퍼런스로 전달한다.





#### 참고

> 마크 그레고리, 『전문가를 위한 C++(4판)』, 남기혁
>

