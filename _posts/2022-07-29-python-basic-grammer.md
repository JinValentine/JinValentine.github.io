---
layout: single
title: "[Python] 파이썬 간단한 문법"
categories: Python
---

## 알고리즘 공부를 하며 배운 파이썬의 간단한 문법들

- 줄바꿈 없이 출력

```python
print('abc', end=' ')
```

---

- 빠른 동작속도를 위한 입력

```python
import sys
sys.stdin.readline().rstrip()
```

---

- list에 숫자들을 넣고 싶을 때

```python
list(map(int, input().split()))
```

---

- list에 값 추가, 제거, 조회

```python
list.append(value)        # value를 리스트의 마지막에 추가
list.insert(index, value) # list에 지정된 index에 value 넣기
list.extend(list)         # list에 다른 list 내용 추가
list.count(value)         # list에서 value의 개수를 셀 때
```

---

- list의 순서 및 정렬

```python
list.reverse()          # 순서 뒤집기
list.sort()             # 오름차순 정렬
list.sort(reverse=True) # 내림차순 정렬
```

---

- set

```python
set(list) # list안 중복 값을 없애고 set 데이터형태가 된다.
```

---

- 아스키 코드

```python
ord() # 문자를 아스키코드로 변환
chr() # 아스키코드를 문자로 변환
```

---

- 언더바(\_)

```python
for _ in range(5):
    print("Hello World")
# 반복을 수행하되 반복을 위한 변수의 값을 무시하고자 할 때 사용한다.
```

---

- 리스트 컴프리헨션

```python
data = []
for i in range(1, 11):
    if i % 2 == 0:
        data.append(i)

# 리스트 컴프리헨션을 사용하면 1줄로 표현이 가능하다.

data = [i for i in range(1, 11) if i % 2 == 0]
```

---

- raise

```python
if year_of_birth > 2005:
	raise Exception("message")
# 일부러 Exception을 발생시킬 때 사용한다.
```

---

- 조건문 내에서의 부등식

```python
if x > 0 and x < 20:
    print("x는 0 초과 20 미만의 수 입니다.")
# 파이썬은 조건문 안에서 수학의 부등식을 그대로 사용할 수 있다.
```

---

- 람다 표현식

```python
def add(a, b):
    return a + b

#일반적인 메서드
print(add(3, 7))

#람다 표현식 메서드
print((lambda a, b: a + b)(3, 7))
# (lambda 매개변수들: 식)(인수들)
```

---

파이썬 언어로 알고리즘을 공부하면서 배운 기본적인 문법들 중 몇개를 기록해보았다.
파이썬언어에 대해 공부하면서 느낀점은 확실히 **편하다**는 것이다.
