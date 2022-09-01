---
layout: single
title: "[백준] 2609번 최대공약수, 최소공배수 구하기 (파이썬) "
categories: Algorithm
tag: [python, algorithm]
published: true
---

# 유클리드 호제법을 이용해 최대공약수, 최대공배수를 구해보자

알고리즘을 처음 시작했을 때는 최대공약수, 최대공배수를 단순히 for문을 사용해서 구했지만 **유클리드 호제법**을 사용하면 더 빠르게 값을 구할 수 있기에 이제는 이 방식을 이용해서 구하게 되었다.

## 문제링크

백준 2609번  
[문제링크 바로가기](https://www.acmicpc.net/problem/2609)

---

## 풀이

```python

import sys

input = sys.stdin.readline

num1, num2 = map(int, input().split())

# 유클리드 호제법을 활용한 최대공약수, 최소공배수 구하기

#최대공약수
def gcd(num1 , num2):
    while num2 > 0:
        num1, num2 = num2, num1 % num2

    return num1

#최소공배수
def lcm(num1, num2):
    return num1 * num2 // gcd(num1, num2)

print(gcd(num1, num2))
print(lcm(num1, num2))

```

### 유클리드 호제법

#### 유클리드 호제법이란?

유클리드 호제법(Euclidean algorithm) 또는 유클리드 알고리즘은 2개의 자연수 또는 정식(整式)의 최대공약수를 구하는 알고리즘의 하나이다.
호제법이란 말은 두 수가 서로 상대방 수를 나누어서 결국 원하는 수를 얻는 알고리즘을 나타낸다.

#### 최대공약수

num1 -> num2로 num2 -> (num1 % num2)로 값을 서로 바꿔가면서 num2의 값이 0이 되면 num1값이 **최대공약수**

#### 최소공배수

num1 \* num2를 최대공약수로 나눈 값이 **최소공배수**

---

### 참조

[유클리드 호제법\_위키백과](https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C_%ED%98%B8%EC%A0%9C%EB%B2%95)

**잘못된 정보 또는 오타가 기재되어있을 경우 피드백해주시면 감사하겠습니다!**
