---
layout: post
title: 병행성과 병렬성
author: munjjang9
tags: [concurrency, parallelism]
date: 2024-12-06 18:00 +0900
categories: [Computer Architecture]
toc: true
---

# 병행성( Concurrency )과 병렬성( Parallelism )

<br>

## 병행성

하나의 프로세스를 이용해서 두 개 이상의 프로세스를 동시에 실행하는 것

하나 이상의 프로그램들이 한 순간에 하나의 CPU에서 처리를 시작함

하지만 한 순간에는 하나의 프로세스만 처리가 됨

<br>

## 병렬성

여러 개의 프로세서가 한 개 이상의 프로세스가 분할된 것(Thread)을 동시에 처리하는 것

하나 이상의 프로그램들이 한 순간에 여러 개의 CPU에서 처리를 시작함

한 순간에 두 개 이상의 프로그램을 처리할 수 있음