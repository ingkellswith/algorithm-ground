최소신장트리
===
# 신장 트리(Spanning Tree)의 조건  
- 본래의 그래프의 모든 노드를 포함해야 함  
- 모든 노드가 서로 연결  
- 트리의 속성을 만족시킴 (사이클이 존재하지 않음)  

![spanning-tree](https://user-images.githubusercontent.com/55550753/137920184-c337077f-8ad7-47df-bfa7-e1ce463055cc.PNG)

# 최소 신장 트리(Minimum Spanning Tree)
가능한 Spanning Tree 중에서, 간선의 가중치 합이 최소인 Spanning Tree를 지칭한다.  

![minimum-spanning-tree](https://user-images.githubusercontent.com/55550753/137920169-bbbcea26-919a-493a-b6b2-7b281c82eed4.PNG)

# 크루스칼 알고리즘(Kruskal's algorithm)

1. 모든 정점을 독립적인 집합으로 만든다.  
2. 모든 간선을 비용을 기준으로 정렬하고, 비용이 작은 간선부터 양 끝의 두 정점을 비교한다.  
3. 두 정점의 최상위 정점을 확인하고, 서로 다를 경우 두 정점을 연결한다. (최소 신장 트리는 사이클이 없으므로, 사이클이 생기지 않도록 하는 것임)  

![kruskal](https://user-images.githubusercontent.com/55550753/137920836-1bd7446d-4038-4827-9b8b-887b08573b02.PNG)

# 크루스칼 알고리즘 코드
```text
mygraph = {
    'vertices': ['A', 'B', 'C', 'D', 'E', 'F', 'G'],
    'edges': [
        (7, 'A', 'B'),
        (5, 'A', 'D'),
        (7, 'B', 'A'),
        (8, 'B', 'C'),
        (9, 'B', 'D'),
        (7, 'B', 'E'),
        (8, 'C', 'B'),
        (5, 'C', 'E'),
        (5, 'D', 'A'),
        (9, 'D', 'B'),
        (7, 'D', 'E'),
        (6, 'D', 'F'),
        (7, 'E', 'B'),
        (5, 'E', 'C'),
        (7, 'E', 'D'),
        (8, 'E', 'F'),
        (9, 'E', 'G'),
        (6, 'F', 'D'),
        (8, 'F', 'E'),
        (11, 'F', 'G'),
        (9, 'G', 'E'),
        (11, 'G', 'F')
    ]
}

parent = dict()
rank = dict()


def find(node):
    # path compression 기법
    if parent[node] != node:
        parent[node] = find(parent[node])
    return parent[node]


def union(node_v, node_u):
    root1 = find(node_v)
    root2 = find(node_u)
    
    # union-by-rank 기법
    if rank[root1] > rank[root2]:
        parent[root2] = root1
    else:
        parent[root1] = root2
        if rank[root1] == rank[root2]:
            rank[root2] += 1
    
    
def make_set(node):
    parent[node] = node
    rank[node] = 0

def kruskal(graph):
    mst = list()
    
    # 1. 초기화
    for node in graph['vertices']:
        make_set(node)
    
    # 2. 간선 weight 기반 sorting
    edges = graph['edges']
    edges.sort()
    
    # 3. 간선 연결 (사이클 없는)
    for edge in edges:
        weight, node_v, node_u = edge
        if find(node_v) != find(node_u):
            union(node_v, node_u)
            mst.append(edge)
    
    return mst

print(kruskal(mygraph))
```
