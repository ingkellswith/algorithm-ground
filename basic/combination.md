---
description: '#순열과 조합 #브루트포스 알고리즘'
---

# 파이썬에서의 순열과 조합

파이썬 기본 라이브러리 사용법 출처 : https://heytech.tistory.com/78

1. 순열
```text
from itertools import permutations 
dataset = ['A', 'B', 'C'] 
res = list(permutations(dataset, 3))
print(f"모든 조합: {res}") 
# [('A', 'B', 'C'), ('A', 'C', 'B'), ('B', 'A', 'C'), 
# ('B', 'C', 'A'), ('C', 'A', 'B'), ('C', 'B', 'A')]
```

2. 조합
```text
from itertools import combinations 
dataset = ['A', 'B', 'C'] 
res = list(combinations(dataset, 2)) 
print(f"모든 경우: {res}") 
# [('A', 'B'), ('A', 'C'), ('B', 'C')]
```

3. 중복 순열
```text
from itertools import product 
dataset = ['A', 'B', 'C'] 
res = list(product(dataset, repeat = 2)) 
print(f"모든 경우: {res}") 
# [('A', 'A'), ('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'B'), ('B', 'C'), ('C', 'A'), ('C', 'B'), ('C', 'C')]
```

4. 중복 조합
```text
from itertools import combinations_with_replacement 
dataset = ['A', 'B', 'C'] 
res = list(combinations_with_replacement(dataset, 2)) 
print(f"모든 경우: {res}") 
# [('A', 'A'), ('A', 'B'), ('A', 'C'), ('B', 'B'), ('B', 'C'), ('C', 'C')]
```

---

## 백준 2798번 : 블랙잭

### 1. 중첩 반복문 풀이

```text
n, m = list(map(int, input().split(' ')))
data = list(map(int, input().split(' ')))

result=0
length =len(data)

count=0
# 아래 3중첩 반복문은 곧 알고리즘으로 구현한 '조합'과 같다.
for i in range(0,length):
  for j in range(i+1, length):
    for k in range(j+1, length):
      sum_value=data[i]+data[j]+data[k]
      if sum_value <= m:
        result=max(result,sum_value)

print(result)
```

### 2. 파이썬 기본 라이브러리 사용 풀이

```text
from itertools import combinations 
 
n, m = list(map(int, input().split(' ')))
data = list(map(int, input().split(' ')))

res = list(combinations(data, 3))

max_number=0
for i in res:
  sum=0
  for j in i:
    sum=sum+j
  if(sum<=m):
    max_number=max(sum,max_number)

print(max_number)
```

# 중복순열 

## 백준 7490번 : 0 만들기

### 1. 재귀함수 풀이

```text
import copy

def recursive(array, n):
  if len(array) == n:
    operators_list.append(copy.deepcopy(array))
    return
  array.append(' ')
  recursive(array, n)
  array.pop()
  array.append('+')
  recursive(array, n)
  array.pop()
  array.append('-')
  recursive(array, n)
  array.pop()

test_case = int(input())
for _ in range(test_case):
  operators_list = []
  n = int(input())
  recursive([], n - 1)
  integers = [i for i in range(1, n + 1)]
  for operators in operators_list:
    string = ""
    for i in range(n - 1):
      string += str(integers[i]) + operators[i]
    string += str(integers[-1])
    if eval(string.replace(" ", "")) == 0:
      print(string)

  print()
```

### 2. 파이썬 라이브러리 사용 풀이
```text
from itertools import product 

test_case = int(input())
answer=[]
for i in range(test_case):
  n = int(input())
  operators_list = list(product([' ', '-', '+'], repeat = n-1))
  integers = [i for i in range(1, n + 1)]
  result=[]
  for operators in operators_list:
    string = ""
    for i in range(n - 1):
      string += str(integers[i]) + operators[i]
    string += str(integers[-1])
    if eval(string.replace(" ", "")) == 0:
      result.append(string)
  #아래 코드에서 sorted()안하면 틀리게 나옴
  answer.append(sorted(result))

for result in answer:
    for r in result:
        print(r)
    print()
```

