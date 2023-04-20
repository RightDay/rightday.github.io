---
title: "[자료구조] 정적배열과 동적배열"
excerpt: "정적배열과 동적배열"

categories:
- Data Structure
tags:
- [Data Structure]

toc: true
toc_sticky: true

date: 2022-05-15
last_modified_at: 2022-05-26
---
# 배열

직접적으로 값을 순차적으로 매핑한다.

배열의 크기를 지정하고 선언하는 **정적 배열(Static Array)**와

배열의 크기를 유동적으로 조절할 수 있는 **동적 배열(Dynamic Array)**가 있다.

배열도 함수 포인터와 마찬가지로, 특정 배열을 선언하게 되면 배열의 이름으로 선언해주는 변수는 포인터이다.



## 정적 배열 (Static Array)

프로그램 실행 전에 미리 공간을 할당받기 때문에, **배열의 크기가** 프로그램이 실행되기 전에 미리 **컴파일 타임**에 정해져야 한다.

- 배열의 크기가 리터럴 상수가 아닌 변수로 넣고 싶다면 ```const```가 붙은 변수, 즉 상수를 넣어야 한다.

  ```cpp
  const int length = 3;
  int array[length];
  ```

- 정적 배열은 주소를 바꾸는 것이 불가능하다.

  - array의 배열 이름은 array의 주소를 담고 있는 상태, 다른 배열의 주소를 담게끔 값을 바꿀 수 없다.



## 동적 배열 (Dynamic Array)

단일 변수에 대한 동적 할당뿐만 아니라 배열 변수를 동적 할당할 수 있다.

컴파일 타임에 배열 길이를 정하는 정적 배열(Static Array)과 다르게 배열을 동적으로 할당하면 **런타임 동안에 배열 길이를 정할 수 있다.**

동적으로 배열을 할당하려면, ```new[]``` 연산자와 ```delete[]``` 연산자를 사용해야 한다.



### 동적으로 배열 할당하기 (Dynamically allocating arrays)

```cpp
#include <iostream>

using namespace std;

int main()
{
    int length;
    cin >> length;	// 실행 중에 입력으로 결정된 크기
    
    int* array = new int[length];	// 동적할당
    
    for (int i = 0; i < length; ++i)	//원소 대입
    {
        cout << *(array + i) << "\t";	// array[i]와 같음
	}
    
    delete [] array;	//메모리 해제
}
```

배열을 할당할 때는 ```new[]```와 같은 배열 버전의 new 연산자를 사용해야 한다.

동적 배열의 메모리는 **정적 배열에 사용되는 메모리와 다른 위치에서 할당**하므로 배열의 크기가 상당히 클 수 있다.

C++에서 **많은 메모리를 할당**해야 하는 프로그램은 동적으로 메모리를 할당하는게 일반적이다.



### 동적으로 배열 해제하기 (Dynamically deleting arrays)

동적으로 할당된 배열을 해제할때는 ```delete[]``` 연산자를 사용한다.

이것은 단일 변수 대신 **여러 변수**를 정리해야 한다는 것을 CPU에 알려준다.

동적 할당에서 프로그래머가 자주하는 실수 중 하나는 동적으로 할당된 배열을 해제할 때 ```delete[]``` 대신 ```delete```를 사용하는 것이다. 

배열에서 delete의 스칼라 버전을 사용하면 **데이터 손상, 메모리 누수, 충돌 또는 기타 문제와 같은 정의되지 않은 동작**이 발생한다.

배열 해재시 ```new[]```가 변수에 할당된 메모리양을 추적하여 ```delete[]```는 적절한 메모리를 해제할 수 있다. 프로그래머는 이 크기, 길이에 접근할 수 없다.



### 동적 배열 초기화(Initializing dynamically allocated arrays)

- 동적 배열을 0으로 초기화

  ```cpp
  int* array = new int[length]();
  ```

- C++ 11부터 초기화 리스트(Intializer list)를 사용해 동적 배열을 초기화할 수 있다.

  ```cpp
  int staticArray[5] = {9,8,5,2,2};	// C++03 정적 배열 초기화
  int* array = new int[5] {9,8,5,2,2};	// C++11 동적 배열 초기화
  ```

- C++ 11에서는 유니온 초기화를 사용하여 고정 배열도 초기화 할 수 있다.

  ```cpp
  int staticArray[5] {9,8,5,2,2};	// C++11 정적 배열 초기화
  char staticArray[14] {"Hello, world!"}; // C++11 정적 배열 초기화
  ```

- 동적 배열을 C 스타일 문자열로 초기화 할 수 없다.

  ```cpp
  char* array = new char[14] {"Hello, world!"};	// C++ 11에서 동작하지 않음
  ```

- 동적 배열은 명시적으로 길이를 설정해 선언해야 한다.

  ```cpp
  int staticArray[] {1,2,3};	// Okay : 정적 배열의 암시적 크기
  
  int* dynamicArray1 = new int[] {1,2,3};	// Not Okay : 동적 배열의 암시적 크기
  
  int* dynamicArray2 = new int[3] {1,2,3};	// Okay : 동적 배열의 명시적 크기
  ```




#### 참고

> 소년코딩 <https://boycoding.tistory.com/205>
>
> 평생 공부 블로그, <https://ansohxxn.github.io/cpp/chapter6-11/>
>
> 완숙의 블로그, <https://egg-money.tistory.com/161>

