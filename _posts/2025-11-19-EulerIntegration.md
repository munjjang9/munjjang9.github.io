---
layout: post
title: 오일러 적분법
author: munjjang9
tags: [Math, Physics]
date: 2025-11-19 19:30 +0900
categories: [Study]
toc: true
---

## 서론
---
새로운 프로젝트를 진행하면서 물리를 다뤄야 할 일이 많아졌다.  
특히, 줄을 구현하게 되었는데, 줄이 단순히 두 물체 사이를 잇는 것이 아니라, 중력이나 다른 힘들의 영향을 받는 것이 표현되어야 했다.  
그래서 핑계김에 수학과 물리에 대해 공부를 해보려 한다.  

## Euler Integration
---
오일러 적분법은 게임 프로그래밍에서 물리 시뮬레이션을 구현할 때 가장
기초가 되는 수치 해석 기법이다.

게임에서 캐릭터가 점프하거나 총알이 날아가는 것과 같은 모든 물리적인
움직임을 표현할 때 이 방법을 사용하게 된다.

이번 포스트에서는 오일러 적분법이 무엇인지, 어떻게 동작하는지
알아보려고 한다.

<br>

### 왜 오일러 적분법을 사용할까?
---
게임에서 물체의 움직임을 표현하려면 물리 법칙을 따라야 한다.

예를 들어, 공을 위로 던지면 중력 때문에 속도가 점점 느려지다가 결국
다시 떨어진다.

이런 움직임을 정확하게 계산하려면 미분방정식을 풀어야 하는데,
실시간으로 계산하기에는 너무 복잡하다.

그래서 게임에서는 <mark>근사값을 이용한 수치 해석 방법</mark>을
사용한다.

오일러 적분법은 그 중에서도 가장 단순하고 이해하기 쉬운 방법이다.

<br>

### 기본 개념
---
오일러 적분법의 핵심 아이디어는 이렇다.

"매우 짧은 시간 동안에는 물체의 속도가 거의 일정하다고 가정하자"

이 가정 하에 다음 프레임의 위치와 속도를 계산하는 것이다.

<br>

#### 위치 업데이트
---
현재 위치에서 속도만큼 이동한다.


다음 위치 = 현재 위치 + (현재 속도 × 시간) position_next =
position_current + velocity × deltaTime


<br>

#### 속도 업데이트
---
현재 속도에 가속도를 더한다.


다음 속도 = 현재 속도 + (가속도 × 시간) velocity_next =
velocity_current + acceleration × deltaTime


<br>

여기서 deltaTime은 한 프레임에 걸리는 시간이다. 보통 60fps
게임이라면 약 0.0167초가 된다.

<br>

### 수학적 표현
---
수학적으로 오일러 적분법은 다음과 같이 표현할 수 있다.

![Euler Integration
Formula](/assets/images/Euler-Integration-Formula.png)

위 식에서 x는 위치, v는 속도, a는 가속도를 나타낸다.

h는 시간 간격(deltaTime)이고, n은 현재 프레임을 의미한다.

<br>

### 실제 구현 예시
---
C++로 간단한 오일러 적분법을 구현해보면 다음과 같다.
```cpp
class PhysicsObject
{
public:
    Vector3 Position;
    Vector3 Velocity;
    Vector3 Acceleration;

    void Update(float DeltaTime)
    {
        // 순수 오일러 적분법
        // 위치 업데이트 후 속도 업데이트
        // 현재 속도를 사용 (이전 프레임의 속도)
        Position = Position + Velocity * DeltaTime;
        Velocity = Velocity + Acceleration * DeltaTime;

        // 수정 오일러 적분법 적용
        // 속도 업데이트 후 위치 업데이트
        // 업데이트 된 새로운 속도를 사용
        Velocity = Velocity + Acceleration * DeltaTime;
        Position = Position + Velocity * DeltaTime;
    }
};
```

예를 들어, 중력을 받는 물체를 시뮬레이션한다면 이렇게 사용할 수
있다.

```cpp
PhysicsObject Ball;
Ball.Position = Vector3(0, 10, 0); // 높이 10에서 시작
Ball.Velocity = Vector3(0, 0, 0); // 정지 상태
Ball.Acceleration = Vector3(0, -9.8, 0); // 중력 가속도

// 매 프레임마다 호출
void GameLoop(float DeltaTime)
{
    Ball.Update(DeltaTime);
}
```

### 장점

---

1. 구현이 간단하다: 단 두 줄의 코드로 구현 가능하다
2. 계산이 빠르다: 곱셈과 덧셈만으로 이루어져 있어 성능이 좋다
3. 이해하기 쉽다: 물리학의 기본 공식을 그대로 따르기 때문에
직관적이다

### 단점
--- 
하지만 오일러 적분법에는 치명적인 단점이 있다.

오차가 누적된다는 것이다.

짧은 시간 동안 속도가 일정하다고 가정하기 때문에, 실제 값과 계산 값
사이에 오차가 발생한다.

이 오차는 시간이 지날수록 점점 커지게 된다.

#### 불안정성 문제
--- 
특히 스프링이나 진자처럼 왔다갔다 하는 움직임을 시뮬레이션할 때
문제가 심각해진다.

오일러 적분법으로 계산하면 에너지가 계속 증가하는 현상이 발생한다.

실제로는 마찰이 없다면 일정한 높이로 진동해야 하는데, 계산 오차
때문에 점점 더 높이 튀어오르게 된다.

이를 수치적 불안정성(Numerical Instability)이라고 한다.

### 정확도 개선 방법
--- 
오차를 줄이는 가장 간단한 방법은 deltaTime을 작게 만드는 것이다.

프레임당 한 번 계산하는 대신, 물리 시뮬레이션만 더 자주 업데이트하는
것이다.

```cpp
void Update(float DeltaTime)
{
    const float FixedTimeStep = 0.01f; // 100fps로 물리 계산
    float Accumulator = DeltaTime;

    while (Accumulator >= FixedTimeStep)
    {
        PhysicsUpdate(FixedTimeStep);
        Accumulator -= FixedTimeStep;
    }
}
```

하지만 이 방법도 근본적인 해결책은 아니다.

더 정확한 시뮬레이션이 필요하다면 다른 적분 방법을 사용해야 한다.

• Semi-Implicit Euler Method: 속도를 먼저 업데이트하고 새 속도로
위치를 계산  
• Verlet Integration: 이전 프레임의 정보를 활용하여 정확도 향상  
• Runge-Kutta Methods: 더 복잡하지만 훨씬 정확한 방법  

### 언제 사용해야 할까?
--- 
오일러 적분법은 다음과 같은 경우에 적합하다.

1. 간단한 움직임: 총알, 투사체처럼 한 방향으로 날아가는 물체
2. 프로토타입: 빠른 개발이 필요한 초기 단계
3. 성능이 중요한 경우: 수백 개의 물체를 동시에 시뮬레이션할 때

반대로 다음과 같은 경우에는 다른 방법을 고려해야 한다.

1. 정확도가 중요한 시뮬레이션: 물리 퍼즐 게임, 시뮬레이터
2. 스프링이나 진자 같은 진동 시스템: 캐릭터의 뼈, 천 시뮬레이션
3. 장시간 지속되는 시뮬레이션: 오차 누적이 문제가 될 수 있는 경우

### 실제 게임에서의 활용
--- 
언리얼 엔진이나 유니티 같은 상용 엔진에서는 오일러 적분법을 직접
사용하지 않는다.

대부분 Semi-Implicit Euler나 Verlet Integration 같은 개선된 방법을
사용한다.

하지만 오일러 적분법을 이해하는 것은 중요하다.

왜냐하면 모든 수치 적분 방법의 기초가 되기 때문이다.

직접 물리 엔진을 만들거나, 엔진의 물리 시스템을 커스터마이징할 때
이런 기초 지식이 큰 도움이 된다.

### 마치며
--- 
오일러 적분법은 단순하지만 강력한 도구이다.

처음 물리 시뮬레이션을 공부할 때 가장 먼저 접하게 되는 방법이기도
하다.

완벽하지는 않지만, 그 단순함과 직관성 덕분에 여전히 많은 곳에서
사용되고 있다.

게임 프로그래밍을 하면서 물리 엔진을 다룰 때, 내부적으로 어떤 원리로
작동하는지 이해하면 훨씬 수월하게 작업할 수 있다.

• 참고 : https://en.wikipedia.org/wiki/Euler_method
• 참고 : https://gafferongames.com/post/integration_basics/