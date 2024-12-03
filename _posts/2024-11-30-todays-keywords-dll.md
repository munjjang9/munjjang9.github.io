---
layout: post
title: Dynamic Linked Library
author: munjjang9
tags: [keyword, dll, dynamic linked library]
date: 2024-11-30 23:59 +0900
categories: Keywords
toc: true
---

<br>
<br>

# 동적 연결 라이브러리 (DLL : Dynamic Linked Library)
여러가지 프로그램에서 필요할 때나, 동시에나 사용할 수 있는 코드와 데이터가 포함된 동적 라이브러리

## DLL의 장점

1. 컴파일 하는 데 걸리는 시간이 줄어든다.

2. 별도의 소스 코드 없이 기능만 제공하는 것이 가능하다.

3. 사용하는 프로그램이나 소스 코드와 분리되어 있어, 그들과 충돌이 일어나지 않는다.

4. 같은 운영체제 상에서는 다른 언어로 제작된 기능들도 사용할 수 있다.

5. 프로그램 내에서 같은 기능이 있을 때, 해당 기능을 DLL로 빼서 사용하면 메모리를 절약할 수 있다.

6. 컴파일 된 프로그램의 크기가 작아진다.

7. 웬만하면 내용이 바뀌지 않기 때문에, 실행파일만 업데이트 하면 된다. 여러 자원을 절약할 수 있다.

8. <mark>Direct X</mark> 등의 고용량 라이브러리는 필요한 기능만 DLL을 로딩하여 메모리를 절약할 수 있다.