---
layout: post
title: 룽게-쿠타 방법
author: munjjang9
tags: [Math, Physics]
date: 2025-11-20 23:30 +0900
categories: [Study]
toc: true
---

## Runge-Kutta Method
---
룽게-쿠타 방법은 오일러 적분법의 단점을 개선한 수치 해석 기법이다.  

오일러 적분법이 단순하지만 오차가 크다는 문제가 있었다면, 룽게-쿠타 방법은 더 복잡하지만 훨씬 정확한 결과를 제공한다.  

게임 물리 엔진에서 정확도가 중요한 시뮬레이션을 구현할 때 사용되는 방법이다.  

<br>

### 왜 룽게-쿠타 방법이 필요한가?
---
[이전 포스트](https://munjjang9.github.io/study/2025/11/19/EulerIntegration/)에서 오일러 적분법의 문제점을 다뤘었다.

오일러 적분법은 단순히 현재 순간의 기울기만 사용해서 다음 위치를 예측한다.  

이는 마치 고속도로에서 현재 방향만 보고 계속 직진하는 것과 같다.  

도로가 휘어지는 것을 고려하지 않기 때문에 결국 길을 벗어나게 된다.  

룽게-쿠타 방법은 여러 지점의 기울기를 샘플링해서 평균을 내는 방식으로 이 문제를 해결한다.

<br>

### RK2 (2차 룽게-쿠타)
---
가장 간단한 형태는 2차 룽게-쿠타, 즉 RK2이다.

이 방법은 중점 방법(Midpoint Method)이라고도 불린다.

#### 동작 원리

1. 현재 위치에서 오일러 방법으로 **중간 지점**을 계산한다  
2. 중간 지점에서의 기울기를 구한다  
3. **중간 지점의 기울기**를 사용해서 최종 위치를 계산한다  

![RK2 Method](/assets/images/RK2-Method.png)

#### 수학적 표현

```
k1 = f(xn, tn) * h
k2 = f(xn + k1/2, tn + h/2) * h
xn+1 = xn + k2
```

여기서:  
- `f(x, t)`는 미분 방정식 (예: 속도)  
- `h`는 시간 간격 (deltaTime)  
- `k1`은 시작점의 기울기  
- `k2`는 중간점의 기울기  

<br>

### RK4 (4차 룽게-쿠타)
---
실제로 가장 많이 사용되는 것은 4차 룽게-쿠타, 즉 RK4이다.

이 방법은 네 개의 샘플 지점을 사용해서 더욱 정확한 결과를 낸다.

#### 동작 원리

1. 시작점에서 기울기 계산 (k1)  
2. 중간점 전반부에서 기울기 계산 (k2)  
3. 중간점 후반부에서 기울기 계산 (k3)  
4. 끝점에서 기울기 계산 (k4)  
5. 네 기울기의 **가중 평균**을 사용해서 최종 위치 계산  

![RK4 Method](/assets/images/RK4-Method.png)

#### 수학적 표현

```
k1 = f(xn, tn) * h
k2 = f(xn + k1/2, tn + h/2) * h
k3 = f(xn + k2/2, tn + h/2) * h
k4 = f(xn + k3, tn + h) * h

xn+1 = xn + (k1 + 2*k2 + 2*k3 + k4) / 6
```

중간 지점의 기울기(k2, k3)에 2배의 가중치를 주는 것이 핵심이다.

<br>

### C++ 구현 - RK2
---
먼저 2차 룽게-쿠타를 구현해보자.

```cpp
class PhysicsObjectRK2
{
public:
    Vector3 Position;
    Vector3 Velocity;
    Vector3 Acceleration;

    // 가속도를 계산하는 함수 (예: 중력, 스프링 힘 등)
    Vector3 CalculateAcceleration(const Vector3& Pos, const Vector3& Vel)
    {
        // 여기서는 단순히 중력만 적용
        return Acceleration;
    }

    void UpdateRK2(float DeltaTime)
    {
        // k1: 현재 시점의 속도와 가속도
        Vector3 K1_Velocity = Velocity;
        Vector3 K1_Acceleration = CalculateAcceleration(Position, Velocity);

        // 중간 지점 계산
        Vector3 MidPosition = Position + K1_Velocity * (DeltaTime * 0.5f);
        Vector3 MidVelocity = Velocity + K1_Acceleration * (DeltaTime * 0.5f);

        // k2: 중간 지점의 속도와 가속도
        Vector3 K2_Velocity = MidVelocity;
        Vector3 K2_Acceleration = CalculateAcceleration(MidPosition, MidVelocity);

        // k2를 사용해서 최종 업데이트
        Position = Position + K2_Velocity * DeltaTime;
        Velocity = Velocity + K2_Acceleration * DeltaTime;
    }
};
```

<br>

### C++ 구현 - RK4
---
이제 4차 룽게-쿠타를 구현해보자.

```cpp
class PhysicsObjectRK4
{
public:
    Vector3 Position;
    Vector3 Velocity;
    Vector3 Acceleration;

    Vector3 CalculateAcceleration(const Vector3& Pos, const Vector3& Vel)
    {
        // 중력 적용
        return Acceleration;
    }

    void UpdateRK4(float DeltaTime)
    {
        // k1: 시작점
        Vector3 K1_Vel = Velocity;
        Vector3 K1_Acc = CalculateAcceleration(Position, Velocity);

        // k2: 중간점 (전반부)
        Vector3 Pos2 = Position + K1_Vel * (DeltaTime * 0.5f);
        Vector3 Vel2 = Velocity + K1_Acc * (DeltaTime * 0.5f);
        Vector3 K2_Vel = Vel2;
        Vector3 K2_Acc = CalculateAcceleration(Pos2, Vel2);

        // k3: 중간점 (후반부)
        Vector3 Pos3 = Position + K2_Vel * (DeltaTime * 0.5f);
        Vector3 Vel3 = Velocity + K2_Acc * (DeltaTime * 0.5f);
        Vector3 K3_Vel = Vel3;
        Vector3 K3_Acc = CalculateAcceleration(Pos3, Vel3);

        // k4: 끝점
        Vector3 Pos4 = Position + K3_Vel * DeltaTime;
        Vector3 Vel4 = Velocity + K3_Acc * DeltaTime;
        Vector3 K4_Vel = Vel4;
        Vector3 K4_Acc = CalculateAcceleration(Pos4, Vel4);

        // 가중 평균으로 최종 업데이트
        Position = Position + (K1_Vel + K2_Vel * 2.0f + K3_Vel * 2.0f + K4_Vel) * (DeltaTime / 6.0f);
        Velocity = Velocity + (K1_Acc + K2_Acc * 2.0f + K3_Acc * 2.0f + K4_Acc) * (DeltaTime / 6.0f);
    }
};
```

<br>

### 성능 비교
---
각 방법의 특징을 비교해보자.

| 방법 | 함수 호출 횟수 | 정확도 | 복잡도 |
|------|--------------|--------|--------|
| Euler | 1 | 낮음 | 매우 단순 |
| RK2 | 2 | 중간 | 단순 |
| RK4 | 4 | 높음 | 복잡 |

RK4는 오일러 방법보다 4배 많은 계산을 하지만, 오차는 **16배** 정도 줄어든다.

<br>

### 언제 RK4를 사용해야 할까?
---
다음과 같은 경우에 RK4가 적합하다.

#### 사용해야 하는 경우
1. **정확도가 중요한 시뮬레이션**: 물리 퍼즐 게임, 시뮬레이터  
2. **진동 시스템**: 스프링, 진자, 캐릭터 본 시뮬레이션  
3. **장기간 시뮬레이션**: 오차 누적이 문제가 되는 경우  
4. **천 시뮬레이션**: 옷, 깃발, 로프 등  

#### 오일러로 충분한 경우
1. **단순한 투사체**: 총알, 미사일, 화살  
2. **일회성 움직임**: 폭발 파편, 이펙트  
3. **대량의 객체**: 파티클 시스템 (수백~수천 개)  
4. **프로토타입**: 빠른 개발이 필요한 초기 단계  

<br>

### 실제 게임 엔진에서의 활용
---
대부분의 상용 물리 엔진은 RK4를 직접 사용하지 않는다.

대신 다음과 같은 절충안을 사용한다.

#### Verlet Integration
- RK4보다 빠르면서도 안정적  
- 위치 기반 시뮬레이션에 적합  
- Unity의 Cloth 시스템에서 사용  

#### Semi-Implicit Euler (Symplectic Euler)
- 오일러보다 안정적이면서 빠름  
- 대부분의 게임 물리에 충분  
- Unity의 기본 물리 엔진에서 사용  

#### Adaptive RK4
- 필요한 곳에만 RK4 적용  
- 오차가 큰 부분은 자동으로 시간 간격 줄임  
- 과학 시뮬레이션에서 사용  

<br>

### 최적화 팁
---
RK4는 계산량이 많기 때문에 최적화가 중요하다.

#### 선택적 적용
```cpp
void Update(float DeltaTime)
{
    if (bRequireHighAccuracy)
    {
        // 정확도가 중요한 객체만 RK4 사용
        UpdateRK4(DeltaTime);
    }
    else
    {
        // 나머지는 Semi-Implicit Euler 사용
        UpdateSemiImplicitEuler(DeltaTime);
    }
}
```

#### SIMD 활용
여러 객체를 동시에 계산할 때 SIMD를 사용하면 성능이 크게 향상된다.

```cpp
// 4개 객체를 한 번에 계산
void UpdateRK4_SIMD(__m128 Positions, __m128 Velocities, float DeltaTime)
{
    // SIMD 연산으로 4배 빠른 계산 가능
}
```

#### 캐싱
`CalculateAcceleration` 함수가 복잡하다면 결과를 캐싱한다.

```cpp
// 같은 프레임 내에서 중복 계산 방지
std::unordered_map<Vector3, Vector3> AccelerationCache;
```

<br>

### 안정성 vs 정확도
---
흥미롭게도, **더 정확하다고 항상 더 좋은 것은 아니다**.

게임에서는 때로 안정성이 정확도보다 중요하다.

예를 들어:  
- RK4는 정확하지만, 큰 시간 간격에서 불안정할 수 있다  
- Semi-Implicit Euler는 덜 정확하지만, 에너지 보존이 더 잘된다

특히 캐릭터 컨트롤러나 물리 기반 애니메이션에서는 안정성이 더 중요하다.

플레이어는 1% 오차는 눈치채지 못하지만, 캐릭터가 땅을 뚫고 들어가는 것은 바로 알아챈다.

<br>

### 하이브리드 접근법
---
실무에서는 여러 방법을 조합해서 사용하는 것이 일반적이다.

```cpp
class HybridPhysicsSystem
{
public:
    void Update(float DeltaTime)
    {
        // 중요한 객체들만 RK4
        for (auto& obj : HighPrecisionObjects)
        {
            obj.UpdateRK4(DeltaTime);
        }

        // 일반 객체는 Semi-Implicit Euler
        for (auto& obj : StandardObjects)
        {
            obj.UpdateSemiImplicitEuler(DeltaTime);
        }

        // 파티클은 단순 Euler
        for (auto& particle : Particles)
        {
            particle.UpdateEuler(DeltaTime);
        }
    }
};
```

<br>

### 마치며
---
룽게-쿠타 방법은 오일러 적분법의 단점을 크게 개선한 방법이다.

더 많은 계산이 필요하지만, 그만큼 정확하고 안정적인 시뮬레이션이 가능하다.

게임 개발에서는 상황에 맞게 적절한 방법을 선택하는 것이 중요하다.

- 단순한 움직임: Euler 또는 Semi-Implicit Euler  
- 중간 정확도: RK2 또는 Verlet  
- 높은 정확도: RK4 또는 Adaptive RK  

물리 엔진의 내부 동작을 이해하면, 성능과 정확도 사이에서 더 현명한 선택을 할 수 있다.

- 참고: https://en.wikipedia.org/wiki/Runge%E2%80%93Kutta_methods  
- 참고: https://gafferongames.com/post/integration_basics/  
- 참고: https://www.gamedev.net/tutorials/programming/math-and-physics/a-tutorial-on-euler-angles-and-quaternions-r2598/
