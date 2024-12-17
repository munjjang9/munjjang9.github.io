---
layout: post
title: 의존성 주입
author: munjjang9
tags: [solid, principle]
date: 2024-11-29 23:59 +0900
categories: [Software Engineering]
toc: true
---

# 의존성 주입
객체 지향 설계 원칙인 SOLID 원칙 중 [의존 - 역전 원칙](https://munjjang9.github.io/c/c++/2024/11/28/programming-method/#%EC%9D%98%EC%A1%B4---%EC%97%AD%EC%A0%84-%EC%9B%90%EC%B9%99-dependency-inversion-principle)에서 중요한 키워드

인터페이스를 사이에 둬서 클래스 레벨에서는 의존관계가 고정되지 않도록 하고 런타임 시에 관계를 동적으로 주입하여 유연성을 확보하고 결합도를 낮출 수 있게 하는 것

클래스 간의 의존성(결합도)을 낮추기 위해 외부에서 의존성을 주입하는 방식

A가 변경 되었을 때, B가 변경되는 것을 막을 수 있다.

