최단경로 구하기
===
# 다익스트라 알고리즘을 사용하여 (단방향)최단경로 구하기

![dijkstra-graph](https://user-images.githubusercontent.com/55550753/136809756-0be4ff0b-e6b4-43f0-b696-85420d5677c5.PNG)

### 위와 같은 그래프에서 최단경로 구하기(모든 방향은 단방향)

```text
import heapq

def dijkstra(graph, start):
    
    distances = {node: float('inf') for node in graph}
    distances[start] = 0
    queue = []
    heapq.heappush(queue, [distances[start], start])
    
    while queue:
        # current_node로 가는데 걸리는 길이가 current_distance
        current_distance, current_node = heapq.heappop(queue)
        
        if distances[current_node] < current_distance:
            continue
            
        for adjacent, weight in graph[current_node].items():
            # distance = current_node로 가는데 걸리는 길이 + (근접한 다른)adjacent 노드로 가는데 걸리는 길이
            distance = current_distance + weight
            
            # 위에서 계산한 distance와 기존 distance를 비교
            if distance < distances[adjacent]:
                distances[adjacent] = distance
                heapq.heappush(queue, [distance, adjacent])
                
    return distances

mygraph = {
    'A': {'B': 8, 'C': 1, 'D': 2},
    'B': {},
    'C': {'B': 5, 'D': 2},
    'D': {'E': 3, 'F': 5},
    'E': {'F': 1},
    'F': {'A': 5}
}

dijkstra(mygraph, 'A')
```