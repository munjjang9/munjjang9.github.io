---
layout: post
title: 예외 처리
author: munjjang9
tags: [C/C++]
date: 2024-12-10 22:00 +0900
categories: [Languages]
toc: true
---

# Exception Handling

<br>

예외 처리는 코드 실행 중에 오류가 발생 했을 경우, 이를 실행하지 않고 해결하기 위한 방법으로써 사용된다.

## try - catch

try 블록은 예외가 발생할 구간을 지정해줄 때 사용된다. catch 블록은 발생한 예외에 대한 처리를 해주는 블록이다. try 블록에 예외처리를 할 코드를 작성하고 catch 블록에서 해당 예외를 처리를 한다.

## finally

finally 블록은 예외가 발생하지 않았거나, try 블록에서 발생한 예외가 catch 블록에서 정상적으로 처리되었을 경우(여기서 말하는 정상적인 처리는 try 블록에서 발생한 예외가 catch 블록들 중 존재하여 이를 처리할 수 있는 경우를 말한다.) 수행된다. 

## throw

throw는 어떤 예외가 발생했다는 것을 알려주기 위한 키워드이다. try 블록 내에서 예외가 발생한 데이터를 throw에 의해 던져지고, catch에서 그걸 받아 처리한다.

<br>

### 예시

```csharp
try
{
    if(예외 조건)
        throw 예외데이터;
}

catch(데이터타입 expn)
{
    // 예외 처리
}

finally
{
    // 예외 발생 없거나 정상적으로 처리된 경우
}
```