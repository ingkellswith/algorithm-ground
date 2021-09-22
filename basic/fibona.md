---
description: '#수학 #구현'
---

# 피보나치

## 백준 2747번 : 피보나치 수

### 1. 첫 풀이

```text
count = int(input())-1

a=0
b=1
temp=0

for n in range(count):
  temp=a+b
  a=b
  b=temp

if(temp == 0):
  print(1)
else:
  print(temp)
```

### 2. 재귀 함수 풀이

```text
def fibonacci(n):
    if n == 0:
        return 0
    if n == 1:
        return 1
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(int(input())))
```

### 3. 최적화 풀이

```text
n = int(input())

a, b = 0, 1

while n > 0:
    // 값 대입 두 번만 하면 끝나는 것이 핵심
    a, b = b, a + b
    n -= 1

print(a)
```

