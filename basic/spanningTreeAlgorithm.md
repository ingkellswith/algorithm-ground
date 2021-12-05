---
description: '#그래프 이론 #다익스트라'
---

# 최소 신장 트리(Minimum Spanning Tree, MST)

## 백준 1774번 : 우주신과의 교감

### - 그래프 이론, 최소 신장 트리

### 1. 풀이

```text
import math

def get_distance(p1, p2):
  a = p1[0] - p2[0]
  b = p1[1] - p2[1]
  return math.sqrt((a * a) + (b * b))

def get_parent(parent, n):
  if parent[n] == n:
    return n
  return get_parent(parent, parent[n])

def union_parent(parent, a, b):
  a = get_parent(parent, a)
  b = get_parent(parent, b)
  # a<b는 a>b로 해도 성립한다.
  # 이유는 parent를 정하는 방법만 일관되면 상관없기 때문이다.
  if a < b:
    parent[b] = a
  else:
    parent[a] = b

def find_parent(parent, a, b):
  a = get_parent(parent, a)
  b = get_parent(parent, b)
  if a == b:
    return True
  else:
    return False

edges = []
parent = {}
locations = []
# n: 우주신들의 개수(n<=1,000) 
# m: 이미 연결된 신들과의 통로의 개수(m<=1,000)
n, m = map(int, input().split())

for _ in range(n):
# 황선자를 포함하여 우주신들의 좌표 x, y
# (0<= X<=1,000,000), (0<=Y<=1,000,000)
  x, y = map(int, input().split())
  locations.append((x, y))
length = len(locations)

for i in range(length - 1):
  for j in range(i + 1, length):
    # print('연습', i + 1, j + 1, get_distance(locations[i], locations[j]))
    # (시작점, 도착점, 거리)
    # 중복으로 구하진 않음 ex) (1,2,2.0)만 구하고 (2,1,2.0)을 구하지 않음
    edges.append((i + 1, j + 1, get_distance(locations[i], locations[j])))

# range(0,n+1)로 해도 됨
for i in range(1, n + 1):
  parent[i] = i

for i in range(m):
  a, b = map(int, input().split())
  union_parent(parent, a, b)

edges.sort(key=lambda data: data[2])
result = 0

for a, b, cost in edges:
  if not find_parent(parent, a, b):
    union_parent(parent, a, b)
    result += cost

print("%0.2f" % result)
```