---
description: '#이분 탐색 #매개 변수 탐색'
---

# 이분 탐색

## 백준 2110번 : 공유기 설치

### 1. 풀이
```text
n, c = list(map(int, input().split(' ')))
array = []
for _ in range(n):
  array.append(int(input()))
array = sorted(array)
start = 1
end = array[-1] - array[0]
result = 0
while(start <= end):
  mid = (start + end) // 2 # mid는 Gap을 의미합니다.
  value = array[0]
  count = 1
  for i in range(1, len(array)):
    if array[i] >= value + mid:
      value = array[i]
      count += 1
  if count >= c: # C개 이상의 공유기를 설치할 수 있는 경우
    start = mid + 1
    result = mid
  else: # C개 이상의 공유기를 설치할 수 없는 경우
    end = mid - 1
print(result)
```

첫 풀이에서 start를 ```start = array[1]-array[0]```로 설정했는데  
틀렸다고 처리하길래 1로 바꾸었더니 통과했다.  
이분 탐색에서 시작 지점을 주의할 수 있도록 하자.  