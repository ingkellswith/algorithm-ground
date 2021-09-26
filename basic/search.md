---
description: '#문자열 #그리디 알고리즘 #브루트포스 알고리즘'
---

# 탐색 알고리즘

## 백준 1543번 : 문서 검색

### 1. 풀이

```text
data=input()
word=input()

i=0
result=0
while i<len(data)-len(word)+1:
  if(data[i:len(word)+i]==word):
    result=result+1
    i=i+len(word)
  else:
    i=i+1

print(result)
```
--- 

## 백준 1568번 : 새

### 1. 풀이

```text
bird=int(input())

i=1
time=0

while bird>0:
  if(bird<i):
    i=1
  bird=bird-i
  time=time+1
  i=i+1

print(time)
```
--- 

## 백준 1668번 : 트로피 진열

### 1. 풀이

```text
n=int(input())

arr=[]

for _ in range(0,n):
  size=int(input())
  arr.append(size)

left_count=1
right_count=1

left_max=0
right_max=0
for i in range(0,len(arr)-1):
  if(i==0):
    left_max=arr[i]
  if(arr[i+1]>left_max):
    left_count+=1
    left_max=arr[i+1]

arr.reverse()

for i in range(0,len(arr)-1):
  if(i==0):
    right_max=arr[i]
  if(arr[i+1]>right_max):
    right_count+=1
    right_max=arr[i+1]

print(left_count)
print(right_count)
```

