---
layout: post
title: ConstExpr
author: munjjang9
tags: [C/C++]
date: 2025-01-01 21:00 +0900
categories: [Languages]
toc: true
---

## constexpr
---

객체나 함수의 앞에 붙는 키워드로, C++ 11에서 새로 생긴 키워드이다.

Constant Expression의 줄임말로 객체나 함수의 앞에 붙어 그 리턴 값을 컴파일 시간에 알 수 있다.

constexpr은 해당 식이 상수식이라는 것을 명시하는 것이다.

<br>

### constexpr VS const
---

const는 변수를 상수로써 관리하기 위해 사용되며, const로 정의된 상수는 컴파일 시간에 값을 알 수 없다.

```cpp
const int a = 1;

int b = 2;

const int c = b;
```

위의 경우에, a는 1이라는 값을 가지고, 변경이 불가능하다. 그리고 c는 b의 값을 가지며 처음 값이 정해지면 변경이 불가능하다.

<br>

```cpp
int a = 1; //(1)

constexpr b = a; //(2)

constexpr c = 2; //(3)

constexpr d = c; //(4)
```

위의 경우에 2번에서 오류가 나게 된다. 그 이유는 constexp이 붙은 상수의 오른쪽에는 상수 식이 와야 하기 떄문이다.

따라서 3번처럼 상수가 오거나, c처럼 상수로 선언된 변수또는 식이 와야한다.

<br>

constexpr은 const의 부분집합이라고 볼 수 있다.