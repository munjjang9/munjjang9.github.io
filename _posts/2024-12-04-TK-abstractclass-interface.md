---
layout: post
title: 추상클래스와 인터페이스
author: munjjang9
tags: [C/C++]
date: 2024-12-04 23:59 +0900
categories: [Languages]
toc: true
---
# [추상](https://munjjang9.github.io/c/c++/2024/12/03/Virtual-Abstract/#%EC%B6%94%EC%83%81--abstract-) 클래스

추상 클래스를 상속 받으면 그 안에 선언되어 있는 추상 함수를 같은 이름으로 재정의 해줘야한다. 무조건 같은 이름으로 재정의 해야 하기에 이름을 강제하는 것이라 볼 수 있다.

상속 받은 추상클래스의 추상 함수를 재정의해주지 않으면 다음과 같은 오류가 발생한다.

예시

![Abstract Error](/assets/images/AbstractError.png "Abstract Error")

# 인터페이스

필요한 기능을 사용할 클래스에만 제공하기 위해 사용한다

방금의 설명만 보면 추상과 똑같은 것 아닌가? 라는 의문을 가질 수 있다. 이는 방금의 예제를 통해 설명이 가능하다. Player와 Enemy, NPC 모두 캐릭터로, Character 클래스를 상속받는다.

그런데, Attack이라는 추상 함수 때문에 NPC에서는 오류가 발생하게 된다. 그러면 Attack 기능은 사용할 수 없는 것인가? 그렇지 않다.

Attack 기능을 Character 클래스가 아닌 Interface에 선언하게 되면 Player와 Enemy 클래스에만 기능을 제공해주는 것이 가능해진다.

C++에서는 인터페이스 키워드를 지원하지는 않는다. 그래서 추상 클래스와 순수 가상 함수로 구현하기도 한다.