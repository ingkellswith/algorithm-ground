---
description: '#기하학'
---

# 기하학

## 백준 1004번 : 어린 왕자

### 1. 풀이

```text
t = int(input())

for i in range(t):
    count = 0

    x1, y1, x2, y2 = map(int, input().split())
    n = int(input())

    for i in range(n):
        px, py, pr = map(int, input().split())
        # **2는 제곱 **0.5는 루트를 씌운 것과 같다.
        # d1은 시작점부터 한 점까지의 거리
        d1 = (((x1 - px) ** 2) + ((y1 - py) ** 2)) ** 0.5
        # d2는 도착점부터 한 점까지의 거리
        d2 = (((x2 - px) ** 2) + ((y2 - py) ** 2)) ** 0.5
        # 시작점과 도착점을 기준으로 한 점의 반지름을 체크
        if (d1 < pr and d2 > pr) or (d1 > pr and d2 < pr):
            count += 1
    print(count)
```
중간의 행성을 피하는 것은 우주선이 할 일이고,
알고리즘은 **출발점이나 도착점이 행성의 내부에 위치**한 것을 체크하면 된다.