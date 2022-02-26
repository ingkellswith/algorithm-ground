---
description: '#동적 프로그래밍'
---

# 동적 프로그래밍

## 백준 1904번 : 01타일

### - 다이나믹 프로그래밍

### 1. 풀이
```text
n = int(input())

dp = [0] * 1000001
dp[1] = 1
dp[2] = 2

for i in range(3, n + 1):
# 15746이 무슨 숫자인진 모르겠으나 안 붙이면 정답이 아님
# a=b, b=a+b 이렇게 swap방식으로 하면 시간 초과뜸
    dp[i] = (dp[i - 2] + dp[i - 1]) % 15746

print(dp[n])
```

---

## 백준 12865번 : 평범한 배낭

### - 다이나믹 프로그래밍, 배낭 문제

### 1. 풀이
```text
n, k = map(int, input().split())
arr = [[0] * (k + 1) for _ in range(n + 1)]

for i in range(1, n + 1):
  weight, value = map(int, input().split())
  for j in range(1, k + 1):
    if j < weight:
      arr[i][j] = arr[i - 1][j]
    else:
      arr[i][j] = max(arr[i - 1][j], arr[i - 1][j - weight] + value)

print(arr[n][k])
```

---

## 백준 11053번 : 가장 긴 증가하는 부분 수열

### - 다이나믹 프로그래밍

### 1. 첫 풀이
```text
from collections import Counter

n = int(input())
arr = list(map(int, input().split()))
result=[]

for key, value in Counter(arr).items():
  result.append(key)

print(len(result))
# 숫자 순서가 상관 없다고 가정했을 때 배열 안에 각 숫자를 distinct하게 센 것이다.
# 결과적으로 문제는 이것을 요구하는 것이 아님
```

### 2. 정답
```text
n = int(input())
array = list(map(int, input().split()))
result = [1] * n

for i in range(1, n):
  for j in range(0, i):
    if array[j] < array[i]:
      result[i] = max(result[i], result[j] + 1)

print(max(result))
```

---

## 백준 9251번 : LCS(Longest Common Subsequence, 최장 공통 부분 수열)

### - 다이나믹 프로그래밍

### 1. 풀이
```text
x = input()
y = input()

arr = [[0] * (len(y) + 1) for _ in range(len(x) + 1)]

for i in range(1, len(x) + 1):
  for j in range(1, len(y) + 1):
    if x[i - 1] == y[j - 1]:
      arr[i][j] = arr[i - 1][j - 1] + 1
    else:
      arr[i][j] = max(arr[i][j - 1], arr[i - 1][j])

print(arr[len(x)][len(y)])
```

---

## 백준 5582번 : 공통 부분 문자열

### - 다이나믹 프로그래밍, 문자열

### 1. 풀이
```text
answer = 0
x, y = input(), input()

dp=[[0] * (len(y) + 1) for _ in range(len(x) + 1)]

for i in range(1, len(x) + 1):
    for j in range(1, len(y) + 1):
        if (x[i-1] == y[j-1]):
            dp[i][j] = dp[i-1][j-1] + 1
            answer = max(dp[i][j], answer)

print(answer)
```

백준 **9251번** : LCS(Longest Common Subsequence, 최장 공통 부분 문자열)과 유사한 문제이나,
**9251번**은 서로 떨어진 문자도 '공통 부분 문자열'로 취급하나 **5582번**은 서로 붙어 있는 문자만 '공통 부분 문자열'로 취급한다.

---

## 백준 1495번 : 기타리스트

### - 다이나믹 프로그래밍

### 1. 풀이

```text
n, s, m = map(int, input().split())
arr = list(map(int, input().split()))

dp = [[0] * (m + 1) for _ in range(n + 1)]
dp[0][s] = 1

for i in range(1, n + 1):
  for j in range(m + 1):
    if dp[i - 1][j] == 0:
      continue
    if j - arr[i - 1] >= 0:
      dp[i][j - arr[i - 1]] = 1
    if j + arr[i - 1] <= m:
      dp[i][j + arr[i - 1]] = 1

result = -1
for i in range(m, -1, -1):
  if dp[n][i] == 1:
    result = i
    break
    
print(result)
```

---

## 백준 2655번 : 가장 높은 탑 쌓기

### - 다이나믹 프로그래밍

### 1. 풀이

```text
n = int(input())
arr = []
arr.append((0, 0, 0, 0))

for i in range(1, n + 1):
  area, height, weight = map(int, input().split())
  arr.append((i, area, height, weight))
# 무게를 기준으로 정렬합니다.
arr.sort(key=lambda data: data[3])

dp = [0] * (n + 1)

for i in range(1, n + 1):
  for j in range(0, i):
    if arr[i][1] > arr[j][1]:
      dp[i] = max(dp[i], dp[j] + arr[i][2])

max_value = max(dp)
index = n
result = []

while index != 0:
  if max_value == dp[index]:
    result.append(arr[index][0])
    max_value -= arr[index][2]
  index -= 1
  
result.reverse()
print(len(result))
[print(i) for i in result]
```
---

## 백준 1014번 : 컨닝

### - 다이나믹 프로그래밍, 비트마스킹, 최대 유량, 비트필드를 이용한 다이나믹 프로그래밍

### 1. 오답 풀이
```text
test_case=int(input())

result=[]

for _ in range(test_case):
  arr=list()
  count=0
  count2=0
  n, m = list(map(int,input().split(' ')))

  for i in range(n):
    arr.append(list(input()))

  if(m % 2 == 0):
    for i in range(m//2):
      for j in range(n):
        if(arr[j][i*2]=='.'):
          count+=1

    for i in range(m//2):
      for j in range(n):
        if(arr[j][i*2+1]=='.'):
          count2+=1

    result.append(max(count, count2))
  
  elif(m % 2 == 1):
    for i in range(m//2+1):
      for j in range(n):
        if(arr[j][i*2]=='.'):
          count+=1

    for i in range(m//2):
      for j in range(n):
        if(arr[j][i*2+1]=='.'):
          count2+=1

    result.append(max(count, count2))

for i in result:
  print(i)
```
```text
.XXX
XXXX
X.XX
```
위 풀이는 이 유형을 만족하지 못한다.

정답 풀이과정은 https://nerogarret.tistory.com/33을 참고
