# 음계

## 백준 2920번 : 음계

### 1. 풀이

```text
a = list(map(int, input().split(' ')))
ascending=True
descending = True
for i in range(1, 8):
    if a[i] > a[i-1]:
        descending=False
    elif a[i] < a[i-1]:
        ascending=False
if ascending:
    print('ascending')
elif descending:
    print('descending')
else:
    print('mixed')
```