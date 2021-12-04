---
description: '#너비 우선 탐색 #깊이 우선 탐색'
---

#  BFS and DFS

## 백준 1260번 : DFS와 BFS

### - 그래프 이론, 그래프 탐색, 너비 우선 탐색, 깊이 우선 탐색

### 1. 풀이

```text
from collections import defaultdict

n, m, start = list(map(int,input().split()))
graph=defaultdict(list)

for _ in range(m):
  a,b=list(map(int,input().split()))
  graph[a].append(b)
  graph[b].append(a)

# 리버스 안하면 오른쪽부터 dfs돈다.
for a in graph.values():
  a.sort(reverse=True)

def dfs(graph, start_node):
  visited = list()
  need_visit = list()
  need_visit.append(start_node)
    
  while need_visit:
      node = need_visit.pop()
      if node not in visited:
          visited.append(node)
          need_visit.extend(graph[node])
  
  return visited

result=dfs(graph, start)
for i in result:
  print(i, end=' ')

print()
# 리버스 안하면 왼쪽부터 bfs돈다.
for a in graph.values():
  a.sort()

def bfs(graph, start_node):
  visited = list()
  need_visit = list()
  need_visit.append(start_node)

  while need_visit:
      node = need_visit.pop(0)
      if node not in visited:
          visited.append(node)
          need_visit.extend(graph[node])
  
  return visited

result=bfs(graph, start)
for i in result:
  print(i, end=' ')
```

---

## 백준 1697번 : 숨바꼭질

### - 그래프 이론, 그래프 탐색, 너비 우선 탐색

### 1. 정답
```text

from collections import deque

MAX = 100001
n, k = map(int, input().split())
array = [0] * MAX

def bfs():
  q = deque([n])
  while q:
    now_pos = q.popleft()
    if now_pos == k:
      return array[now_pos]
    for next_pos in (now_pos - 1, now_pos + 1, now_pos * 2):
      if 0 <= next_pos < MAX and not array[next_pos]:
        array[next_pos] = array[now_pos] + 1
        q.append(next_pos)

print(bfs())

```
