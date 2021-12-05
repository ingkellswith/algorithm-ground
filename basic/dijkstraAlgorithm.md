---
description: '#그래프 이론 #다익스트라'
---

# 다익스트라 알고리즘

## 백준 10282번 : 해킹

### - 그래프 이론, 다익스트라

### 1. 풀이

```text
import heapq

def dijkstra(start):
  heap_data = []
  heapq.heappush(heap_data, (0, start))
  distance[start] = 0
  while heap_data:
    dist, now = heapq.heappop(heap_data)
    if distance[now] < dist:
     continue
    for i in adj[now]:
      cost = dist + i[1]
      if distance[i[0]] > cost:
        distance[i[0]] = cost
        heapq.heappush(heap_data, (cost, i[0]))

# 테스트 케이스 수만큼 반복
for _ in range(int(input())):
  # n: 컴퓨터 개수
  # m: 의존성 개수 
  # start: 해킹당한 컴퓨터의 번호 
  n, m, start = map(int, input().split())
  adj = [[] for i in range(n + 1)]
  distance = [float('inf')] * (n + 1)
  for _ in range(m):
    # 컴퓨터 x가 컴퓨터 y를 의존하며, 컴퓨터 y가 감염되면 cost초 후 컴퓨터 x도 감염됨을 뜻한다.
    x, y, cost = map(int, input().split())
    # 2차원 배열 내부에 튜플 존재
    adj[y].append((x, cost))

  dijkstra(start)

  count = 0
  max_distance = 0

  for i in distance:
    if i != float('inf'):
      count += 1
      if i > max_distance:
        max_distance = i
  print(count, max_distance)
```

---

## 백준 5719번 : 거의 최단 경로

### - 그래프 이론, 그래프 탐색, 다익스트라

### 1. 시간 초과 풀이

```text
import heapq

def dijkstra():
  heap_data = []
  heapq.heappush(heap_data, (0, start))
  distance[start] = 0
  while heap_data:
    dist, now = heapq.heappop(heap_data)
    if distance[now] < dist:
      continue
    for i in adj[now]:
      cost = dist + i[1]
      # i[0]은 now에서 갈 수 있는 노드, i[1]은 cost
      # 기존 다익스트라에서 and not dropped[now][i[0]]이 부분만 추가됨
      if distance[i[0]] > cost and not dropped[now][i[0]]:
        distance[i[0]] = cost
        heapq.heappush(heap_data, (cost, i[0]))

def bfs():
  need_visit = list()
  need_visit.append(end)
  while need_visit:
    now = need_visit.pop(0)
    if now == start:
      continue
    for prev, cost in reverse_adj[now]:
      # 역추적으로 dropped 이차원 배열에서 해당값을 True로 만든다.
      # 그리고 need_visit에 추가해준다.
      if distance[now] == distance[prev] + cost:
        dropped[prev][now] = True
        need_visit.append(prev)

result=[]

while True:
  # 장소의 수 N (2 ≤ N ≤ 500)
  # 장소는 0부터 N-1번까지 번호가 매겨져 있다.
  # 도로의 수 M (1 ≤ M ≤ 10000)가 주어진다. 
  n, m = map(int, input().split())
  if n == 0:
    break
  # 시작점 start
  # 도착점 end(start ≠ end; 0 ≤ start, end < N) 
  start, end = map(int, input().split())
  adj = [[] for _ in range(n + 1)]
  reverse_adj = [[] for _ in range(n + 1)]
  for _ in range(m):
    # 다음 M개 줄에는 도로의 정보 x, y, cost가 주어진다. 
    # (x ≠ y ; 0 ≤ x, y < N; 1 ≤ cost ≤ 1000) 
    # 이 뜻은 x에서 y로 가는 도로의 길이가 cost라는 뜻이다.
    # x에서 y로 가는 도로는 최대 한 개이다. 
    # 또, x에서 y로 가는 도로와 y에서 x로 가는 도로는 다른 도로이다.  
    x, y, cost = map(int, input().split())
    adj[x].append((y, cost))
    reverse_adj[y].append((x, cost))
  
  dropped = [[False] * (n + 1) for _ in range(n + 1)]

  distance= [float("inf")] * (n + 1)
  dijkstra()

  bfs()

  distance= [float("inf")] * (n + 1)
  dijkstra()

  if distance[end] != float("inf"):
    result.append(distance[end])
  else:
    result.append(-1)

for i in result:
  print(i)
```

정답은 맞으나 시간 초과가 발생한다.
문제 풀이 방식에 역추적이 들어있으니 충분히 고민해 볼 문제다.

---