---
title: "[C++] 구조적 바인딩(Structured Binding)"
excerpt: "구조적 바인딩(Structured Binding)"

categories:
- C++
tags:
- [C++]

toc: true
toc_sticky: true

date: 2023-05-15
last_modified_at: 2023-05-15
---
# 구조적 바인딩(Structured Binding)

**C++17**부터 도입되었으며, 구조적 바인딩을 이용하면 **여러 개의 변수를 선언할 때 배열, 구조체, 페어 또는 튜플의 값으로 초기화**할 수 있다.

```cpp
std::array<int, 3> values = { 11, 22, 33 };
```

이 상태에서 x, y, z란 변수를 선언할 때 각각 앞에 나온 values 배열에 담긴 값으로 초기화할 수 있다. 

구조적 바인딩을 적용하려면 반드시 **auto** 키워드를 붙여야 한다. 예를 들어 auto 자리에 int를 지정하면 안 된다.

```cpp
auto [x, y, z] = values;
```

구조적 바인딩에서는 왼쪽에 나온 선언할 변수 개수와 오른쪽에 나온 표현식 **값 개수가 반드시 일치**해야 한다.

구조적 바인딩은 배열뿐만 아니라 모든 멤버가 **non-static이면서 public으로 선언된** 데이터 구조라면 어떤 것(struct, pair, tuple 등)도 적용할 수 있다. 예를 들면 다음과 같다.

```cpp
struct Point { double mX, mY, mZ; };
Point point;
point.mX = 1.0; point.mY = 2.0; point.mZ = 3.0;
auto [x, y, z] = point;
```



#### 참고

> 마크 그레고리, 『전문가를 위한 C++(4판)』, 남기혁
>

