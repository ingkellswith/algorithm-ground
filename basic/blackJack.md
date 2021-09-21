# 블랙잭

## 백준 2798번 : 블랙잭

### 1. 풀이

```text
n, m = list(map(int, input().split(' ')))
data = list(map(int, input().split(' ')))

result=0
length =len(data)

count=0
# 아래 3중첩 반복문은 곧 알고리즘으로 구현한 '조합'과 같다.
for i in range(0,length):
  for j in range(i+1, length):
    for k in range(j+1, length):
      sum_value=data[i]+data[j]+data[k]
      if sum_value <= m:
        result=max(result,sum_value)

print(result)
```