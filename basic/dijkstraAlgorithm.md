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

테스트 케이스는 맞으나 시간 초과가 발생한다.
문제 풀이 방식에 역추적이 들어있으니 충분히 고민해 볼 문제다.

---

## 백준 4485번 : 녹색 옷 입은 애가 젤다지?

### - 그래프 이론, 다익스트라

### 1. 풀이

```text
import heapq
import sys

input = sys.stdin.readline
INF = float('inf')

dx = [-1, 1, 0, 0]
dy = [0, 0, -1, 1]

def dijkstra():
    q = []
    heapq.heappush(q, (graph[0][0], 0, 0))
    distance[0][0] = 0

    while q:
        cost, x, y = heapq.heappop(q)

        if x == n - 1 and y == n - 1:
            print(f'Problem {count}: {distance[x][y]}')
            break

        for i in range(4):
            new_x = x + dx[i]
            new_y = y + dy[i]

            if 0 <= new_x < n and 0 <= new_y < n:
                new_cost = cost + graph[new_x][new_y]

                if new_cost < distance[new_x][new_y]:
                    distance[new_x][new_y] = new_cost
                    heapq.heappush(q, (new_cost, new_x, new_y))

count = 1

while True:
    n = int(input())
    if n == 0:
        break

    graph = [list(map(int, input().split())) for _ in range(n)]
    distance = [[INF] * n for _ in range(n)]

    dijkstra()
    count += 1
```
백준 1987번 알파벳 - 백트래킹과 유사한 문제다.
두 문제 비교해볼 것.

---
## 백준 11779번 : 최소비용 구하기2

### - 그래프 이론, 다익스트라

### 1. 풀이
```text
from heapq import heappop, heappush
INF = float('inf')

def sol(start, end):
    dist = [INF for _ in range(N)]
    dist[start] = 0
    path = [-1 for _ in range(N)]
    q = []
    heappush(q, [0, start])
    while q:
        # point노드로 가는데에 cost가 소모된다.
        cost, point = heappop(q)
        for adjacent, weight in graph[point]:
            # point노드에서 adjacent노드로 가는데에 weight+cost가 소모된다.
            weight += cost
            if weight < dist[adjacent]:
                dist[adjacent] = weight
                path[adjacent] = point
                heappush(q, [weight, adjacent])
    return dist[end], path
# 첫째 줄에 도시의 개수 n(1≤n≤1,000) 
# 둘째 줄에는 버스의 개수 m(1≤m≤100,000)
N, M = int(input()), int(input())
graph = [[] for _ in range(N)]
# 1. 출발 도시 번호
# 2. 도착지의 도시 번호
# 3. 비용
for _ in range(M):
    S, E, C = map(int, input().split())
    graph[S-1].append([E-1, C])
# 출발지, 도착지
start, end = map(int, input().split())
# 함수 실행해서 최소비용과 경로배열 리턴
costResult, p = sol(start-1, end-1)
# 경로배열에서 경로를 찾는 과정
pathResult = [end-1]
temp = end-1
while p[temp] != -1:
    pathResult.append(p[temp])
    temp = p[temp]
# 결과 출력
print(costResult)
print(len(pathResult))
for i in pathResult[::-1]:
    print(i+1, end=' ')
```
테스트 케이스 출력값이
```text
4
3
1 4 5
```
로 나온다. 
1 3 5나 1 4 5는 똑같이 
최단 거리가 4이고 3개의 노드를 지나는 것이 동일하므로 문제는 없다고 생각한다.
(1 3 5가 나와야 할 조건도 없음)

---
## 백준 1854번 : K번째 최단경로 찾기

### - 그래프 이론, 다익스트라

### 1. 풀이
```text
from collections import defaultdict
import heapq
# n은 각각 김 조교가 여행을 고려하고 있는 도시들의 개수
# m은 도시 간에 존재하는 도로의 수
# k는 k번째 최단경로
n,m,k = map(int, input().split())

graph=defaultdict(list)
countDict=defaultdict(list)

for _ in range(m):
  a,b,c = map(int, input().split())
  graph[a].append((b,c))

INF=float('inf')
distances=[INF for _ in range(m+1)]

distances[1]=0
q=[]
heapq.heappush(q, [distances[1], 1])
countDict[1].append(0)
while q:
  current_distance, current_node = heapq.heappop(q)
  for adjacent, distance in graph[current_node]:
    cost= current_distance + distance
    # 최단경로 아니어도 그냥 다 세면 됨
    countDict[adjacent].append(cost)
    if(cost < distances[adjacent]):
      distances[adjacent]=cost
      heapq.heappush(q, [cost, adjacent])

for i, arr in countDict.items():
  if(i!=0 and len(arr)>=k ):
    temp=sorted(arr)
    print(temp[k-1])
  else:
    print(-1)

```
테스트 케이스는 통과했으나 정답은 아니다.