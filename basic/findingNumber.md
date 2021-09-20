# 수 찾기

## 백준 1920번 : 수 찾기

### 1. 풀이

```text
n = int(input())
array = set(map(int, input().split()))
m = int(input())
x = list(map(int, input().split()))
for i in x:
    if i not in array:
        print('0')
    else:
        print('1')
```