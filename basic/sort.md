---
description: '#정렬 #문자열'
---

# 정렬

## 백준 1427번 : 소트인사이드

### 1. 선택 정렬 풀이

```text
n=list(map(int, input()))
for i in range(len(n)):
  # 리스트의 각 원소를 max_index로 잡고 반복문 실행
  max_index=i
  for j in range(i+1, len(n)): # 메인 로직
    if(n[max_index]<n[j]):
      max_index=j
  n[i], n[max_index]= n[max_index],n[i]
b=""
for i in n:
  b=b+str(i)
print(b)
```

위 풀이는  
선택 정렬을 내림차순으로 진행한 것과 같다.

### 2. 버블 정렬\(참고\)

```text
def bubbleSort(x):
    length = len(x)-1
    for i in range(length):
        for j in range(length-i):
            if x[j] > x[j+1]:
                x[j], x[j+1] = x[j+1], x[j]
    return x
```

### 3. 삽입 정렬\(참고\)

```text
def insert_sort(x):
  for i in range(1, len(x)):
    j = i - 1
    key = x[i]
    while x[j] > key and j >= 0:
      x[j+1] = x[j]
      j = j - 1
    x[j+1] = key;
  return x
```

## 백준 2750번 : 수 정렬하기

```text
n=int(input())
array=list()

for _ in range(n):
  array.append(int(input()))

array.sort()

for i in array:
  print(i)
```

## 백준 10814번 : 나이순 정렬

```text
count=int(input())
arr=[]
for _ in range(count):
  a=input().split(' ')
  arr.append((int(a[0]),a[1]))
arr2 = sorted(arr, key = lambda x : x[0])
for i in arr2:
  print(i[0],i[1])
```

## 백준 11650번 : 좌표 정렬

```text
count=int(input())
array=list()
for _ in range(count):
  a,b =map(int,input().split(' '))
  array.append((a,b))
array=sorted(array)
# 바로 윗줄 코드는 array=sorted(array, key=lambda x : (x[0],x[1]))와 동일
for i in array:
  print(i[0],i[1])
```

## 백준 10989번 : 수 정렬하기 3

```text
import sys

n = int(sys.stdin.readline())
array = [0] * 10001

for i in range(n):
  data = int(sys.stdin.readline())
  array[data] += 1
for i in range(10001):
  if array[i] != 0:
    for j in range(array[i]):
      print(i)
```

문제의 조건에 따라 배열이 너무 커지면 메모리 초과가 발생할 수 있다.  
일반적으로 풀게 되면 배열의 크기가 10,000,000이 될 수도 있기 때문에 다른 방법으로 접근해야 한다.  
따라서 1~10000부터 사용하는 숫자의 개수를 세어, 크기가 10000인 배열을 사용했다.

