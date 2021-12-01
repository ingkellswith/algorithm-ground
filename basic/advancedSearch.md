---
description: '#우선순위 큐'
---

# 고급 탐색 알고리즘

## 백준 1927번 : 최소 힙

### - 자료 구조, 우선순위 큐

### 1. 풀이

```text
import heapq

n = int(input())
heap = []
result = []
for _ in range(n):
  data = int(input())
  if data == 0:
    if heap:
      result.append(heapq.heappop(heap))
    else:
      result.append(0)

  else:
    heapq.heappush(heap, data)

for data in result:
  print(data)
```
--- 

## 백준 1715번 : 카드 정렬하기

### - 자료 구조, 그리디 알고리즘, 우선순위 큐

### 1. 풀이

```text
import heapq

n = int(input())
heap = []
for i in range(n):
  data = int(input())
  heapq.heappush(heap, data)
result = 0
while len(heap) != 1:
  one = heapq.heappop(heap)
  two = heapq.heappop(heap)
  sum_value = one + two
  result += sum_value
  heapq.heappush(heap, sum_value)
print(result)
```

--- 

## 백준 1766번 : 문제집

### - 그래프 이론, 자료 구조, 우선순위 큐, 위상 정렬!!

### 1. 풀이

```text
# 위상 정렬 문제
import heapq

# n : 총 문제 개수
# m : 제약 조건 개수
n, m = map(int, input().split()) 
array = [[] for i in range(n + 1)]
# ex) array=[[],[],[],[],[]]
# array내부의 array는 자신보다 늦게 나와야 할 원소가 들어감
indegree = [0] * (n + 1)
# ex) indegree=[0,0,0,0,0]
# indegree는 0이 되면 heappush(원래 0이던 경우 제외)
heap = []
result = []

for _ in range(m):
  x, y = map(int, input().split())
  array[x].append(y)
  indegree[y] += 1
# ex) array is like [[], [], [], [1], [2]]
# 자신보다 먼저 나와야 할 원소를 나열 ex)자신보다 1,3이 먼저 나와야 하면 [1,3]
# ex) indegree is like [0, 1, 1, 0, 0]
# 자신보다 먼저 나와야할 원소가 많을수록 degree가 높아짐 ex)자신보다 먼저 나와야할 원소가 2개면 2
for i in range(1, n + 1):
  if indegree[i] == 0:
    heapq.heappush(heap, i)
# ex) heap is like [3, 4]

result = []
while heap:
  # heappop한 것만 result에 들어감
  data = heapq.heappop(heap)
  result.append(data)
  for y in array[data]:
    indegree[y] -= 1
    if indegree[y] == 0:
      heapq.heappush(heap, y)

for i in result:
  print(i, end=' ')
```