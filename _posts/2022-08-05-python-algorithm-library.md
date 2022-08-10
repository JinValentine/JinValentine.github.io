---
layout: single
title: "[Python] 파이썬 알고리즘 문제에서 자주 쓰는 라이브러리들"
categories: Python
tag: [python, algorithm, library]
published: true
use_math: true
---

# 파이썬 알고리즘 문제에서 자주 쓰이는 라이브러리들에 대해 알아보자

표준 라이브러리: 특정한 프로그래밍 언어에서 자주 사용되는 표준 소스코드를 미리 구현해 놓은 라이브러리

파이썬 표준 라이브러리는 해당 링크로 들어가면 공식 문서가 있기 때문에 추가로 필요한 기능이 있다면 링크를 참조하자
https://docs.python.org/ko/3/library/index.html

- 내장 함수: print(), input()과 같은 기본 입출력 기능부터 sorted()와 같은 정렬 기능을 포함하고 있는 기본내장 라이브러리이다. 파이썬 프로그램을 작성할 때 없어서는 안되는 필수적인 기능을 포함하고 있다.

- itertools: 파이썬에는 반복되는 형태의 데이터를 처리하는 기능을 제공하는 라이브러리이다. 순열과 조합 라이브러리를 제공한다.

- heapq: 힙(Heap) 기능을 제공하는 라이브러리이다. 우선순위 큐 기능을 구현하기 위해 사용한다.

- bisect: 이진 탐색(Binary Search) 기능을 제공하는 라이브러리이다.

- collections: 덱(deque), 카운터(Counter) 등의 유용한 자료구조를 포함하고 있는 라이브러리이다.

내장함수의 경우 기본적인 함수가 많기에 생략한다.

---

## itertools

파이썬에서 반복되는 데이터를 처리하는 기능을 포함하고 있는 라이브러리이며 permutations, combinations가 가장 유용하게 사용되는 클래스이다.

#### permutations

- 리스트와 같은 iterable 객체에서 r개의 데이터를 뽑아 일렬로 나열하는 모든 경우(순열)를 계산해준다.
- 클래스이므로 객체 초기화 이후에는 리스트 자료형으로 변환하여 사용한다.

**예시**

```python
from itertools import permutations

data = ['A', 'B', 'C'] # 데이터 준비
result = list(permutations(data, 3)) # 모든 순열 구하기

print(result)
```

**결과**

```python
[('A', 'B', 'C'), ('A', 'C', 'B'), ('B', 'A', 'C'), ('B', 'C', 'A'), ('C', 'A', 'B'), ('C', 'B', 'A')]
```

#### combinations

- iterable 객체에서 r개의 데이터를 뽑아 순서를 고려하지 않고 나열하는 모든 경우(조합)를 계산한다.
- 클래스이므로 객체 초기화 이후에는 리스트 자료형으로 변환하여 사용한다.

**예시**

```python
from itertools import combinations

data = ['A', 'B', 'C'] # 데이터 준비
result = list(combinations(data, 2)) # 2개를 뽑는 모든 조합 구하기

print(result)
```

**결과**

```python
[('A', 'B'), ('A', 'C'), ('B', 'C')]
```

**추가 내용**

- **permutations**와 같이 기능을 하고 데이터를 **중복**해서 뽑고 싶다면 **product** 클래스를 이용하자
- **combinations**와 같이 기능을 하고 데이터를 **중복**해서 뽑고 싶다면 **combinations_with_replacement** 클래스를 이용하자

---

## heapq

파이썬에서는 힙(Heap)기능을 위해 heapq 라이브러리를 제공한다. heapq는 다익스트라 최단 경로 알고리즘을 포함해 다양한 알고리즘에서 우선순위 큐 기능을 구현하고자 할 때 사용된다.

파이썬의 힙은 최소 힙(Min Heap)으로 구성되어 있으므로 단순히 원소를 힙에 전부 넣었다가 빼는 것만으로도 시간 복잡도 $O(NlogN)$에 오름차순 정렬이 완성된다. 보통 최소 힙 자료구조의 최상단 원소는 '가장 작은' 원소이기 때문이다.

```python
heapq.heappush() : 힙에 원소를 삽입 할 때
heapq.heappop() : 힙에서 원소를 꺼내고자 할 때
```

#### 힙 정렬(Heap Sort)을 heapq로 구현하는 예제

```python
import heapq

def heapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, value)
    # 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
    for _ in range(len(h))
        result.append(heapq.heappop(h))
    return result

result = heapsort([1, 3, 5, 7, 9, 2, 4, 6, 8, 0])
print(result)
```

**결과**

```python
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

#### 최대 힙을 구현하여 내림차순 힙 정렬을 구현하는 방법

파이썬에서는 최대 힙(Max Heap)을 제공하지 않는다.  
따라서 heapq 라이브러리를 이용하여 최대 힙을 구현해야할 때는 원소의 부호를 임시로 변경하는 방식을 사용한다.

**예시**

```python
import heapq

def heapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, -value)
    # 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
    for _ in range(len(h))
        result.append(-heapq.heappop(h))
    return result

result = heapsort([1, 3, 5, 7, 9, 2, 4, 6, 8, 0])
print(result)
```

**결과**

```python
[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```

---

## bisect

파이썬에서는 이진 탐색을 쉽게 구현할 수 있도록 bisect 라이브러리를 제공한다.  
bisect 라이브러리는 '정렬된 배열'에서 특정한 원소를 찾아야 할 때 매우 효과적으로 사용된다.

**많이 사용되는 함수**

```python
bisect_left(a, x) #정렬된 순서를 유지하면서 리스트 a에 데이터 x를 삽입할 가장 왼쪽 인덱스를 찾는 메서드

bisect_right(a, x) # 정렬된 순서를 유지하도록 리스트 a에 데이터 x를 삽입할 가장 오른쪽 인덱스를 찾는 메서드
```

**예시**

```python
from bisect import bisect_left, bisect_right

a = [1, 2, 4, 4, 8]
x = 4

print(bisect_left(a, x))
print(bisect_right(a, x))
```

**결과**

```python
2
4
```

또한 정렬된 리스트'에서 **값이 특정 범위에 속하는 원소의 개수**를 구하고자 할 때 효과적으로 사용될 수 있다.

**예시**

```python
from bisect import bisect_left, bisect_right

# 값이 [left_value, right_value]인 데이터의 개수를 반환하는 함수
def count_by_range(a, left_value, right_value):
    right_index = bisect_right(a, right_value)
    left_index = bisect_left(a, left_value)
    return right_index - left_index

# 리스트 선언
a = [1, 2, 3, 3, 3, 3, 4, 4, 8, 9]

# 값이 4인 데이터 개수 출력
print(count_by_range(a, 4, 4))

# 값이 [-1, 3] 범위에 있는 데이터 개수 출력
print(count_by_range(a, -1, 3))
```

**결과**

```python
2
6
```

---

## Collections

파이썬의 collections 라이브러리는 유용한 자료구조를 제공하는 표준 라이브러리이다.  
collections 라이브러리의 기능 중에서 유용하게 사용되는 클래스는 deque와 Counter이다.

#### deque

- 보통 파이썬에서는 deque를 사용해 큐를 구현한다.
- 리스트 자료형과 다르게 인덱싱, 슬라이싱 등의 기능은 사용할 수 없다.
- 연속적으로 나열된 데이터의 시작 부분이나 끝부분에 데이터를 삽입하거나 삭제할 때 매우 효과적이다.
- 스택이나 큐의 기능을 모두 포함한다고 볼 수 있기 때문에 스택 혹은 큐 자료구조의 대용으로 사용될 수 있다.

```python
deque.popleft() # 첫 번째 원소를 제거할 때
deque.pop # 마지막 원소를 제거할 때
deque.appendleft(x) # 첫 번째 인덱스에 원소 x를 삽입할 때
deque.append(x) # 마지막 인덱스에 원소를 삽입할 때
```

**예시**

```python
from collections import deque

data = deque([2, 3, 4])
data.appendleft(1)
data.append(5)

print(data)
print(list(data)) # 리스트 자료형으로 변환
```

**결과**

```python
deque([1, 2, 3, 4, 5])
[1, 2, 3, 4, 5]
```

#### Counter

- Counter는 등장 횟수를 세는 기능을 제공한다.
- 리스트와 같은 iterable 객체가 주어졌을 때, 해당 객체 내부의 원소가 몇 번씩 등장했는지를 알려준다.

**예시**

```python
from collections import Counter

counter = Counter(['red', 'blue', 'red', 'green', 'blue', 'blue'])

print(counter['blue'])  # 'blue'가 등장한 횟수 출력
print(counter['green']) # 'green'이 등장한 횟수 출력
print(dict(counter)) # 사전 자료형으로 변환
```

**결과**

```python
3
1
{'red': 2, 'blue': 3, 'green': 1}
```

---

## math

math 라이브러리는 자주 사용되는 수학적인 기능을 포함하고 있는 라이브러리이다.

#### 팩토리얼

factorial(x) 함수는 x! 값을 반환한다.

**예시**

```python
import math

print(math.factorial(5)) # 5 팩토리얼을 출력
```

**결과**

```python
120
```

#### 제곱근 찾기

sqrt(x) 함수는 x의 제곱근을 반환한다.

**예시**

```python
import math

print(math.sqrt(7)) # 7의 제곱근을 출력
```

**결과**

```python
2.6457513110645907
```

#### 최대 공약수 찾기

gcd(a, b) 함수는 a와 b의 최대 공약수를 반환한다.

**예시**

```python
import math

print(math.gcd(21, 14))
```

**결과**

```python
7
```

#### 파이(pi)와 자연상수(e)

**예시**

```python
import math

print(math.pi) # 파이(pi) 출력
print(math.e) # 자연상수 e 출력
```

**결과**

```python
3.141592653589793
2.718281828459045
```

---

### 참조

이것이 취업을 위한 코딩 테스트다 with 파이썬 (한빛미디어, 나동빈)

**잘못된 정보 또는 오타가 기재되어있을 경우 피드백해주시면 감사하겠습니다!**
