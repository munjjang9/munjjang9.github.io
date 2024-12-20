---
layout: post
title: 통합 테스트
author: munjjang9
tags: [Software Engineering]
date: 2024-12-14 22:00 +0900
categories: [Game Development]
toc: true
---

# Integration Test

<br>

## 통합 테스트란?

---

단위 모듈 당 테스트를 진행하여 문제가 없는지 판단하는 [단위테스트](https://munjjang9.github.io/software%20engineering/2024/12/13/TK-Unit-Test/#%EB%8B%A8%EC%9C%84-%ED%85%8C%EC%8A%A4%ED%8A%B8%EB%9E%80)와는 달리, 통합 테스트는 두 개 이상의 모듈을 묶어서 테스트를 진행하고 문제가 없는지 확인하는 방법이다.

이를 통해 모듈간 데이터의 통신이 원활하게 이루어지는지를 확인할 수 있다. 각 단위 별로 테스트를 진행하는 단위 테스트와는 달리 여러 모듈이 한 번에 테스트가 진행되기 때문에 테스트 실행 시간이 길어진다. 

그렇기에 통합 테스트는 초반부터 진행해 가는 것이 아닌, 단위 테스트를 거쳐 각 단위 모듈에 이상이 없는지를 판단하며 개발하다가, 개발 후반에 통합테스트를 통해 모듈 간에 데이터를 주고 받는 것에 문제점이 없는지를 판단하기 위해 사용된다.