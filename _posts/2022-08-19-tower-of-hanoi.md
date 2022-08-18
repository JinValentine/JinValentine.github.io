---
layout: single
title: "[백준] 11729번 하노이 탑 이동 순서 (파이썬) "
categories: Algorithm
tag: [python, algorithm]
published: true
---

# 재귀함수를 이용해 하노이 탑 이동 순서를 구해보자

알고리즘을 공부하는 요즘 재귀함수에 대한 이해가 너무 부족해 재귀함수를 이용하는 문제를 풀어보았다.

## 문제링크

백준 11729번
[문제링크 바로가기](https://www.acmicpc.net/problem/11729)

---

## 풀이

```python

def cnt(n):
    if n == 1:
        return 1
    else:
        return cnt(n-1)*2 + 1

def hanoi(n, start, end, backup):
    if n == 1:
        print(start, end)
        return
    hanoi(n - 1, start, backup, end)
    print(start, end)
    hanoi(n - 1, backup, end, start)

n = int(input())
print(cnt(n))
hanoi(n, 1, 3, 2)
```

### 옮긴 횟수를 구하는 과정

n개의 원판을 이동시킬 때 (n - 1)의 원판을 이동시킨 후 제일 밑에 있는 하나의 원판을 이동시킨다. 그리고 다시 (n - 1)원판을 이동시키기 때문에 해당 식이 나오게 된다.

### 수행과정을 구하는 과정

1. 원반을 옮길 때는 맨 밑에 있는 원반을 제외하고 나머지 (n-1)개를 모두 보조기둥으로 옮겨야 한다.
2. 이후 맨 밑에 있는 원반을 목표기둥으로 옮기면 된다. 이 때 목표기둥으로 옮겨진 원반은 더이상 이동할 일이 없기 때문에 이 원반을 제외한 (n-1)개로 다시 진행하면 된다.
3. (n-1)개로 다시 진행할 때는 원래 n개일 때 시작기둥이였던 기둥에는 아무것도 없기 때문에 보조기둥으로 바뀌고 원래 보조기둥이였던 기둥에는 나머지 원반들이 있기 때문에 시작기둥이 된다.

---

### 참조

[[파이썬]알고리즘 이야기(01. 하노이 탑)](https://www.youtube.com/watch?v=FYCGV6F1NuY)

**잘못된 정보 또는 오타가 기재되어있을 경우 피드백해주시면 감사하겠습니다!**
