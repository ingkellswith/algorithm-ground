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

### 2. 두 번째 정답 풀이
```text
current_node, destination = map(int, input().split())
MAX = 100001
array = [0] * MAX

def bfs(start_node):
    need_visit = list()
    
    need_visit.append(start_node)
    
    while need_visit:
        now_pos = need_visit.pop(0)

        if now_pos == destination:
          return array[now_pos]

        for next_pos in (now_pos - 1, now_pos + 1, now_pos * 2):
          # 첫 번째 조건 : 범위 안, 두 번째 조건 : 재방문 제외
          if 0 <= next_pos < MAX and not array[next_pos]:
            array[next_pos] = array[now_pos] + 1
            need_visit.append(next_pos)

print(bfs(current_node))
```

---

## 백준 2606번 : 바이러스

### - 그래프 이론, 그래프 탐색, 너비 우선 탐색, 깊이 우선탐색

### 1. 풀이

```text
from collections import defaultdict

node=int(input())
n=int(input())

graph=defaultdict(list)

for i in range(n):
  a,b=map(int, input().split())
  graph[a].append(b)
  graph[b].append(a)

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

print(len(bfs(graph,1))-1)
```

---

## 백준 1012번 : 유기농 배추

### - 그래프 이론, 그래프 탐색, 너비 우선 탐색, 깊이 우선탐색

### 1. 풀이

```text
import sys
sys.setrecursionlimit(100000)

def dfs(x, y):
  visited[x][y] = True
  directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]
  for dx, dy in directions:
    nx, ny = x + dx, y + dy
    # 배열의 최대값 넘으면 아무것도 안 함
    if nx < 0 or nx >= n or ny < 0 or ny >= m:
      continue
    if array[nx][ny] and not visited[nx][ny]:
      dfs(nx, ny)

# 테스트 케이스 수만큼 반복
for _ in range(int(input())):
  m, n, k = map(int, input().split())
  array = [[0] * m for _ in range(n)]
  visited = [[False] * m for _ in range(n)]

  for _ in range(k):
    y, x = map(int, input().split())
    array[x][y] = 1

  result = 0

  for i in range(n):
    for j in range(m):
      if array[i][j] and not visited[i][j]:
        dfs(i, j)
        result += 1

  print(result)
```
---

## 백준 1325번 : 효울적인 해킹

### - 그래프 이론, 그래프 탐색, 너비 우선 탐색, 깊이 우선탐색

### 1. 첫 풀이

```text
from collections import defaultdict

n,m=map(int, input().split())
arr=[0]*(n+1)

graph=defaultdict(list)

for i in range(m):
  a,b=map(int, input().split())
  graph[b].append(a)

def bfs(start_node):
    visited = list()
    need_visit = list()
    need_visit.append(start_node)
    while need_visit:
        node = need_visit.pop(0)
        if node not in visited:
            visited.append(node)
            need_visit.extend(graph[node])
    
    arr[start_node]=len(visited)

    return arr[start_node]

for i in range(1,n+1): 
  bfs(i)

MAX=max(arr)

for i in range(1,n+1): 
  if(arr[i]==MAX):
    print(i, end=' ')

# 정답은 맞지만 시간초과
```

### 2. 시간 내 풀이

```text
from collections import deque

n, m = map(int, input().split())
adj = [[] for _ in range(n + 1)]

for _ in range(m):
  x, y = map(int, input().split())
  adj[y].append(x)

def bfs(v):
  need_visit = deque([v])
  visited = [False] * (n +1)

  visited[v] = True
  count = 1
  while need_visit:
    v = need_visit.popleft()
    for e in adj[v]:
      if not visited[e]:
        need_visit.append(e)
        visited[e] = True
        count +=1

  return count

result = []
max_value = -1

for i in range(1, n +1):
  c = bfs(i)
  if c > max_value:
    result = [i]
    max_value = c
  elif c == max_value:
    result.append(i)
    max_value = c

for e in result:
  print(e, end=" ")
```

첫 번째 풀이랑 다를 게 없는데 왜 시간초과가 안 뜨는 지 모르겠다.  
bfs count계산 후 로직은 두 풀이의 반복문을 비교해봤을 때 시간복잡도에 영향이 미미하고,  
bfs자체 로직도 첫 풀이가 오히려 반복문이 하나 더 줄어 있는데 말이다.  

---

