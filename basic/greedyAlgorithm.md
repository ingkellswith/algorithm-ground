---
description: '#그리디 알고리즘'
---

# 그리디 알고리즘

## 백준 5585번 : 거스름돈

### - 그리디 알고리즘

### 1. 풀이

```text
n=int(input())

pay=[500, 100, 50, 10, 5, 1]
count=0
price=1000-n
i=0

while True:
  if price==pay[i]:
    count+=1
    break
  if (price>pay[i]):
    count+=1
    price=price-pay[i]
  else:
    i+=1

print(count)
```

---

## 백준 1439번 : 뒤집기

### - 그리디 알고리즘

### 1. 풀이

```text
n=str(input())

count=0
arr=list(n)

if(arr[0]==arr[-1]):
  for i in range(len(n)-1):
    if arr[i]!=arr[i+1]:
      count+=1
  print(count//2)
elif(arr[0]!=arr[-1]):
  for i in range(len(n)-1):
    if arr[i]!=arr[i+1]:
      count+=1
  print(count//2+1)
```
---

## 백준 2012번 : 등수 매기기

### - 그리디 알고리즘, 정렬

### 1. 풀이

```text
n=int(input())

expected_sum=0
arr=[]

for i in range(1,n+1):
  a=int(input())
  arr.append(a)

arr.sort()

for i in range(n):
  if(i+1!=arr[i]):
    expected_sum+=abs(arr[i]-(i+1))

print(expected_sum)
```

---

## 백준 1092번 : 배

### - 그리디 알고리즘, 정렬

### 1. 첫 풀이

```text
crane_count=int(input())
crane_arr=list(map(int,input().split()))

box_count=int(input())
box_arr=list(map(int,input().split()))

crane_arr.sort(reverse=True)
box_arr.sort(reverse=True)

if(crane_arr[0]<box_arr[0]):
  print(-1)

count=0
i=0
while len(box_arr)!=0:
  count+=1
  for crane in crane_arr:
    if(len(box_arr)==0):
      break
    if(crane>=box_arr[i]):
      box_arr.pop(0)

print(count)
```
테스트 케이스는 다 통과했지만 오답 처리..

### 2. 정답 풀이

```text
import sys

n = int(input())
cranes = list(map(int, input().split()))

m = int(input())
boxes = list(map(int, input().split()))

# 모든 박스를 옮길 수 없는 경우
if max(cranes) < max(boxes):
  print(-1)
  sys.exit()
# 각 크레인이 현재 옮겨야 하는 박스의 번호 (0부터 시작)
positions = [0] * n
# 각 박스를 옮겼는지의 여부
checked = [False] * m
# 최적의 해를 구해야 하므로, 내림차순 정렬
cranes.sort(reverse=True)
boxes.sort(reverse=True)
result = 0
count = 0

while True:
  if count == len(boxes): # 박스를 다 옮겼다면 종료
    break
  for i in range(n): # 모든 크레인에 대하여 각각 처리
    while positions[i] < len(boxes):
      # 아직 안 옮긴 박스 중에서, 옮길 수 있는 박스를 만날 때까지 반복
      if not checked[positions[i]] and cranes[i] >= boxes[positions[i]]:
        checked[positions[i]] = True
        positions[i] += 1
        count += 1
        break
      positions[i] += 1
  result += 1

print(result)
```