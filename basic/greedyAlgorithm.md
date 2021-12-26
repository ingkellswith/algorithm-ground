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
---

## 백준 2212번 : 센서

### - 그리디 알고리즘, 정렬

### 1. 풀이

```text
import sys

n = int(input())
k = int(input())

# 집중국의 개수가 n 이상일 때
if k >= n:
  print(0) # 각 센서의 위치에 설치하면 되므로 정답은 0
  sys.exit()
# 모든 센서의 위치를 입력 받아 오름차순 정렬
array = list(map(int, input().split(' ')))
array.sort()
# 각 센서 간의 거리를 계산하여 내림차순 정렬
distances = []
for i in range(1, n):
  distances.append(array[i] - array[i - 1])
distances.sort(reverse=True)
# 가장 긴 거리부터 하나씩 제거
for i in range(k - 1):
  distances[i] = 0
print(sum(distances))
```

---

## 백준 1461번 : 도서관

### - 그리디 알고리즘, 정렬

### 1. 풀이  

![baek1461](https://user-images.githubusercontent.com/55550753/146008609-e0f2f8d9-7484-4a55-b046-e8d0fd034d38.PNG)  
  
```text
# 정답=왕복 거리-가장 먼 책의 편도 거리
import heapq
# n: 책의 개수, 
# m: 세준이가 한 번에 들 수 있는 책의 개수
n, m = map(int, input().split(' '))
# 책의 위치
array = list(map(int, input().split(' ')))
positive = []
negative = []
# 가장 거리가 먼 책까지의 거리
largest = max(max(array), - min(array))
# 최대 힙(Max Heap)을 위해 원소를 음수로 구성
for i in array:
# 책의 위치가 양수인 경우
  if i > 0:
     heapq.heappush(positive, -i)
  # 책의 위치가 음수인 경우
  else:
    heapq.heappush(negative, i)

result = 0
while positive:
# 한 번에 m개씩 옮길 수 있으므로 m개씩 빼내기
  result += heapq.heappop(positive)
  for _ in range(m - 1):
    if positive:
      heapq.heappop(positive)

while negative:
# 한 번에 m개씩 옮길 수 있으므로 m개씩 빼내기
  result += heapq.heappop(negative)
  for _ in range(m - 1):
    if negative:
      heapq.heappop(negative)

# 일반적으로 왕복 거리를 계산하지만, 가장 먼 곳은 편도 거리 계산
print(-result * 2 - largest)
```

---

## 백준 1781번 : 컵라면

### - 자료 구조, 그리디 알고리즘, 우선순위 큐

### 1. 시간 초과 풀이    
  
```text
# 첫 줄에 숙제의 개수 N
n = int(input())
arr=[]
for i in range(n):
  deadline, noodle=map(int,input().split(' '))
  arr.append((deadline, noodle))

arr.sort()

result=0
for i in range(1, n+1):
  temp=[]
  for element in arr:
    if(element[0]==i):
      temp.append(element)
  if(len(temp)>0):
    result+=temp[-1][1]

print(result)
```

### 2. 정답 풀이
```text
import heapq

# 첫 줄에 숙제의 개수 N
n = int(input())
arr=[]
q=[]

for i in range(n):
  a, b=map(int,input().split(' '))
  arr.append((a, b))

arr.sort()

for i in arr:
  a=i[0]
  heapq.heappush(q,i[1])
  # 데드라인 초과할 경우 그냥 원소 제거
  if a<len(q):
    heapq.heappop(q)

print(sum(q))
```
우선순위 큐를 사용하면 한 번의 반복문으로 해결가능하다.