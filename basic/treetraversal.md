---
description: '#트리 #재귀'
---

# 트리 순회

## 백준 1991번 : 트리 순회

### 1. 풀이

```text
class Node:
  def __init__(self, data, left_node, right_node):
    self.data = data
    self.left_node = left_node
    self.right_node = right_node

def pre_order(node):
  print(node.data, end='')
  if node.left_node != '.':
    pre_order(tree[node.left_node])
  if node.right_node != '.':
    pre_order(tree[node.right_node])

def in_order(node):
  if node.left_node != '.':
    in_order(tree[node.left_node])
  print(node.data, end='')
  if node.right_node != '.':
    in_order(tree[node.right_node])

def post_order(node):
  if node.left_node != '.':
    post_order(tree[node.left_node])
  if node.right_node != '.':
    post_order(tree[node.right_node])
  print(node.data, end='')

n = int(input())
tree = {}
for i in range(n):
  data, left_node, right_node = input().split()
  tree[data] = Node(data, left_node, right_node)
  
pre_order(tree['A'])
print()
in_order(tree['A'])
print()
post_order(tree['A'])
```

## 백준 2250번 : 트리의 높이와 너비

### - 그래프 이론, 그래프 탐색, 깊이 우선 탐색

### 1. 풀이

```
class Node:
  def __init__(self, number, left_node, right_node):
    self.parent = -1
    self.number = number
    self.left_node = left_node
    self.right_node = right_node
def in_order(node, level):
  global level_depth, x
  level_depth = max(level_depth, level)
  if node.left_node != -1:
    in_order(tree[node.left_node], level + 1)
  level_min[level] = min(level_min[level], x)
  level_max[level] = max(level_max[level], x)
  x += 1
  if node.right_node != -1:
    in_order(tree[node.right_node], level + 1)

n = int(input())
tree = {}
level_min = [n]
level_max = [0]
root = -1
x = 1
level_depth = 1

for i in range(1, n + 1):
  tree[i] = Node(i, -1, -1)
  level_min.append(n)
  level_max.append(0)
for _ in range(n):
  number, left_node, right_node = map(int, input().split())
  tree[number].left_node = left_node
  tree[number].right_node = right_node
  if left_node != -1:
    tree[left_node].parent = number
  if right_node != -1:
    tree[right_node].parent = number

for i in range(1, n + 1):
  if tree[i].parent == -1:
    root = i

in_order(tree[root], 1)

result_level = 1
result_width = level_max[1] - level_min[1] + 1
for i in range(2, level_depth + 1):
  width = level_max[i] - level_min[i] + 1
  if result_width < width:
    result_level = i
    result_width = width
    
print(result_level, result_width)
```