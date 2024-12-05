---
layout: post
title: 가상과 추상
author: munjjang9
tags: [virtual, abstract]
date: 2024-12-03 18:00 +0900
categories: C/C++
toc: true
---

# 가상( Virtual )과 추상( Abstract )

<br>

## 가상 ( Virtual )
부모 클래스에서 선언, 정의하고 자식 클래스에서 재정의가 가능함

virtual 키워드를 통해 가상화가 되었다는 걸 표기

자식에서 재정의하게 되면, override 키워드를 뒤에 붙여줌(항상 필수는 아님. but 필수인 경우도 있음)

가상함수의 경우, VF-Table. 가상화 테이블이라는 게 만들어지고, 재정의된 함수의 주소를 담고 있는 vf포인터가 생김

부모 클래스의 소멸자에 virtual 키워드가 없으면 자식 클래스에서 소멸자가 콜 되지 않음

- 예시
```c
class Character
{
public:
    Character();
    ~Character(); // -> virtual ~Character();로 바꿔줘야 자식의 소멸자가 호출됨
}

class Player : public Character
{
public:
    Player();
    ~Player(); //호출 X
}

int main()
{
    Character* character = new Player();

    return 0;
}
```
<br>

## 추상 ( Abstract )
이름만 선언해두고 정의를 하지 않으면 추상

부모 클래스에서 선언만 해두고 자식 클래스에서 재정의

추상 멤버 메서드를 하나라도 포함하면 추상 클래스라고 부름

추상 함수를 순수 가상 함수라고도 부름

메모리에 할당이 불가능 함 (=객체화/인스턴스화 불가능)

상속받아 사용하려는 것을 이름이 동일하도록 강제함

```c
class Character //추상 멤버 메서드가 있기 때문에 추상 클래스
{
    virtual void Move() = 0; //순수 가상, 추상
}
```