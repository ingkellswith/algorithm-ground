---
description: '#구현'
---

# 백준 1236번 : 성 지키기

### 1. 풀이

```text
n, m = map(int, input().split())
array = []
for _ in range(n):
  array.append(input())
row = [0] * n
column = [0] * m
for i in range(n):
  for j in range(m):
    if array[i][j] == 'X':
      row[i] = 1
      column[j] = 1

row_count = 0
for i in range(n):
  if row[i] == 0:
    row_count += 1
column_count = 0
for j in range(m):
  if column[j] == 0:
    column_count += 1
print(max(row_count, column_count))
```  

처음보는 유형이었다.  
해답은 'X'가 선언되지 않은 행, 열에 대해서  
max(row_count, column_count)을 구하면 되는 문제였다.  

---