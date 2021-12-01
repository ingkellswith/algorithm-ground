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