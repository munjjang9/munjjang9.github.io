---
layout: post
title: 렌더링 파이프라인
author: munjjang9
tags: [Graphics/Rendering]
date: 2024-12-22 18:00 +0900
categories: [Study]
toc: true
---

# Rendering Pipeline

<br>

## Direct X 11의 렌더링 파이프 라인

렌더링 파이프라인은 메모리 자원들을 GPU로 넘겨받아 처리한 뒤, 이를 통해 이미지를 렌더링 하기 위해 쓰이는 체제이다.

Direct X 11의 렌더링 파이프라인은 다음과 같다.

> IA - VS - HS - TS - DS - GS - SO - RS - PS - OM

![Rendering Pipeline](/assets/images/d3d11-pipeline-stages.jpg)


약간의 분류를 해보자면

IA ~ SO 까지는 3D를 처리하는 단계이고,

RS ~ OM 까지는 2D를 처리하는 단계이다.

또한, VS, HS, TS, DS, GS, PS 단계는 자체적으로 프로그래밍을 통한 제어가 가능하다.

<br>

### IA (Input Assembler)
---
IA단계에서는 입력 값. 즉, 정점들의 정보를 어떻게 조립할지를 결정한다.

Vertex Buffer(정점 버퍼), Index Buffer(인덱스 버퍼), Primitive Topology(기본 위상), Input Layout(입력 배치)등의 정보를 IA 단계에서 넘겨받는다.(RAM -> VRAM)

이를 통해, 넘겨받은 정점들을 어떤 순서로, 어떤 모양으로 조립할 것인지를 결정한다.

<br>

### VS (Vertex Shader)
---
VS 단계에서는 IA단계를 거쳐온 정점들을 처리한다. 정점의 좌표, 색상, 텍스처, 조명 정보들을 처리하여 해당 정점이 어떤 위치에서 어떻게 나타날지 등을 결정할 수 있다.

정점을 지우거나 새로 추가할 수 없으며, 컬링 작업을 수행할 수 없다.

hlsl로 작성된 파일을 통해 이러한 정점 정보들을 처리할 수 있다.

<br>

### HS (Hull Shader)
---

공간을 분할하는 단계

제어점을 읽고 테셀레이션 단계에서 수행하기 위한 출력 제어점을 생성한다. 제어점의 수, 패치 면의 유형, 공간 분할 시 사용하는 분할의 유형 등을 선언한다. 이렇게 테셀레이션 단계에서 요구하는 상태를 선언하는 단계가 HS(헐 셰이더) 단계이다.

<br>

### TS (Tessellator Stage)
---

HS 단계에서 전달 받은 공간 분할 요소나 유형을 한 번 더 쪼개는 역할을 한다. 작은 삼각형 단위로 쪼갠 후, 해당 uv 좌표와 토폴로지를 DS단계로 넘겨준다.

<br>

### DS (Domain Shader)
---

HS 단계에서 출력된 제어점 정보들을 가지고 TS 단계에서 출력된 좌표당 한 번씩 호출되어 계산을 수행한다.
결과적으로 출력 패치의 세분화된 지점의 꼭지점 위치를 출력한다.

<br>

### GS (Geometry Shader)
---

기본 요소인 삼각형, 선, 점 전체를 인접한 꼭지점과 함께 처리한다. 

VS 단계에서도 꼭지점에 대한 처리를 수행하지만, GS 단계에서는 전체 기본 요소에 대한 꼭지점을 처리하기에 둘은 서로 다른 역할을 수행한다.

이렇게 기본 요소들의 꼭지점을 입력 받은 뒤, 지정된 토폴로지를 형성하는 여러 꼭지점을 출력한다. 

<br>

### SO (Stream Output)
---

SO 단계는 말그대로 스트림으로 출력물을 내놓는 단계이다.

이전 파이프라인에서 출력된 꼭지점의 데이터를 입력받아 메모리에 존재하는 버퍼에게 연속적으로 해당 정보들을 출력해준다. 만약 GS나 DS단계가 비활성 상태이면 VS 단계의 정점 정보를 버퍼로 전달한다.

<br>

### RS (Rasterizer Stage)
---

컬링이라는 기법이 있다. 무언가를 잘라내는 기법인데 RS 단계에서 이 기법 중 하나가 사용된다.

바로 백페이스 컬링(Back-Face Culling)이라는 기법인데, 이는 뷰에 보이지 않는, 즉 카메라에 비춰지지 않는 것들을 잘라내는 작업을 수행한다.

RS 단계에서는 PS에 전달해줄 기본 요소들을 준비하고(픽셀 위치에 색상을 지정하는 등), PS를 호출하는 방법을 결정한다.

또한, 깊이에 대한 판단이 RS 단계에서 일어난다. (OM단계에서 일어나는 거 아님!)

<br>

### PS (Pixel Shader)
---

PS 단계에서는 RS 단계에서 전달받은 데이터를 조합하여 픽셀에 대한 정보를 생성한다.

RS 단계에서 각 요소들을 보간하여 픽셀이 어떻게 생성되어야 할지를 넘겨준다면, PS는 이를 가지고 실제로 픽셀을 생성하는 역할을 한다고 보면 된다.

PS 단계에서는 Clipping 작업도 수행이 된다.

<br>

### OM (Output Merger)

앞 단계들에서 전달받은 출력물들(픽셀 셰이더 값, 깊이&스텐실 정보 등)을 조합하여 RTV(Render Target View)와 DSV(Depth Stencil View)의 내용과 조합하여 결과를 만들어낸다. 이 과정에서 나온 결과물이 최종 우리의 화면에 나타난다고 보면 된다.


<br>
<br>
<br>
<br>

- 참조 : https://learn.microsoft.com/en-us/windows/uwp/graphics-concepts/graphics-pipeline