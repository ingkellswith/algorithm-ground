---
description: '#이분 탐색 #매개 변수 탐색'
---

# 이진 탐색 기본 코드
```text
data_list = [66, 65, 18, 71, 11, 10, 42, 68, 36, 89]
data_list.sort()

def binary_search(data, search):
    print (data)
    if len(data) == 1 and search == data[0]:
        return True
    if len(data) == 1 and search != data[0]:
        return False
    if len(data) == 0:
        return False
    
    medium = len(data) // 2
    if search == data[medium]:
        return True
    else:
        if search > data[medium]:
            return binary_search(data[medium+1:], search)
        else:
            return binary_search(data[:medium], search)

binary_search(data_list, 66)
```

# 이분 탐색

## 백준 2110번 : 공유기 설치

### 1. 풀이
```text
n, c = list(map(int, input().split(' ')))
array = []
for _ in range(n):
  array.append(int(input()))
array = sorted(array)
start = 1
end = array[-1] - array[0]
result = 0
while(start <= end):
  mid = (start + end) // 2 # mid는 Gap을 의미합니다.
  value = array[0]
  count = 1
  for i in range(1, len(array)):
    if array[i] >= value + mid:
      value = array[i]
      count += 1
  if count >= c: # C개 이상의 공유기를 설치할 수 있는 경우
    start = mid + 1
    result = mid
  else: # C개 이상의 공유기를 설치할 수 없는 경우
    end = mid - 1
print(result)
```

첫 풀이에서 start를 ```start = array[1]-array[0]```로 설정했는데  
틀렸다고 처리하길래 1로 바꾸었더니 통과했다.  
이분 탐색에서 시작 지점을 주의할 수 있도록 하자.  

---
# 이분 탐색 + 너비 우선 탐색(Breadth First Search)

## 백준 1939번 : 중량제한

### 1. 풀이

```text
from collections import deque

n, m = map(int, input().split())
adj = [[] for _ in range(n + 1)]

def bfs(c):
  queue = deque([start_node])
  visited = [False] * (n + 1)
  visited[start_node] = True
  while queue:
    x = queue.popleft()
    for y, weight in adj[x]:
      if not visited[y] and weight >= c:
        visited[y] = True
        queue.append(y)
  return visited[end_node]

start = 1000000000
end = 1
for _ in range(m):
  x, y, weight = map(int, input().split())
  adj[x].append((y, weight))
  adj[y].append((x, weight))
  start = min(start, weight)
  end = max(end, weight)

start_node, end_node = map(int, input().split())

result = start
while(start <= end):
  mid = (start + end) // 2 # mid는 현재의 중량을 의미합니다.
  if bfs(mid): # 이동이 가능하므로, 중량을 증가시킵니다.
    result = mid
    start = mid + 1
  else: # 이동이 불가능하므로, 중량을 감소시킵니다.
    end = mid - 1

print(result)
```