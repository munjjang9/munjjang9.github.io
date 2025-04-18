---
layout: post
title: Logic Tree
author: munjjang9
tags: [Software Engineering]
date: 2024-12-07 20:00 +0900
categories: [Game Development]
toc: true
---

# Logic Tree

<br>

## 로직 트리란?

문제 해결을 위한 기법 중 하나로, 문제를 논리적인 요소로 분해하고 이를 하나의 트리로 구성하여 문제의 원인을 찾는 방법이다.

보통 왼쪽에서부터 오른쪽으로 그려가며, 가장 왼쪽에 문제를 작성하고, 오른쪽으로 각 원인에 대해 기술한다.

트리의 각 분기는 MECE(Mutually Exclusive Collectively Exhaustive, 상호 배타적이고 집합적으로 철저함)의 기본을 따른다. 이는 항목의 집합을 하위 집합으로 분리하기 위한 원칙이다.

로직 트리에는 크게 Why, What, How 3가지의 종류가 있다. 사용 방법은 다르지만, 사용하는 목적은 모두 문제의 원인을 찾기 위함으로 동일하다.

<br>

---

<br>

예를 들어, 어느 가게의 매출이 줄어드는 문제가 발생한다고 가정해보자.

### Why

Why는 말 그대로 <mark>왜</mark> 이 문제가 발생했는지를 초점에 두고 원인을 찾아가는 방식이다.

그럼 가장 왼쪽 노드에 가게의 매출이 줄어드는 문제를 작성하고, 매출이 왜 줄어드는지에 대한 원인을 다음 노드들에 작성한다. 예로 수요가 줄어드는 원인과, 품질 저하의 원인이 있다고 하면, 또 다음 노드에 왜 그 문제들이 발생했는지를 적어가며 최종 원인을 찾아가는 방식인 것이다.

이 트리를 통해, 발생한 문제의 근본적인 원인을 찾을 수 있다.

<br>

### What

What은 문제가 있을 때, 이를 해결하기 위해 <mark>어떤</mark> 작업을 수행해야 할 지를 트리로 구성하는 방식이다.

가장 왼쪽에는 가게의 매출이 줄어드는 것을 방지/해결 등의 내용을 작성한다.

오른쪽에는 이를 방지, 또는 해결하기 위해 어떤 작업을 수행할 것인지를 작성하고, 또 다음 노드들에는 이전에 작성한 작업을 더욱 세분화 하여 작성해나간다. 이렇게 가장 작은 단위까지 작성하여 어떤 작업을 선행해야 이를 해결할 수 있는 지를 찾는 방식의 트리이다.

이 트리를 통해, 어떤 작업이 이 문제를 해결하는 데 있어 가장 우선시돼야 하는 작업인 지를 찾을 수 있다.

<br>

### How

How는 해결할 문제를 <mark>어떻게</mark> 해결할 것인지를 작성해나가는 트리 방식이다.

예를 들어 판매 이익 증가를 위한 How 트리를 작성한다고 치면, 첫 노드에는 판매 이익 증가를 작성하고 후위 노드들에는 어떻게 이를 노릴 것인지를 작성하게 된다.

하나씩 구성해나가면, 첫 문제를 어떻게 해결해나가면 좋을 지에 대해 여러 방안들이 작성될 것이다. 

이 트리를 통해, 어떻게 작업을 수행해야 문제를 해결하는 데 있어 가장 효율적인 방식인지를 찾을 수 있다.

