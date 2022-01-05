---
description: '#재귀'
---

# 재귀 함수

## 백준 2447번 : 별 찍기 - 10

### 1. 풀이

```text
num = int(input())

def star(n):
  if n == 1: 
    return ['*'] 

  stars = star(n//3) 
  L = [] # 별을 출력할 리스트

  for s in stars: 
    L.append(s*3) # 상 구간
  for s in stars: 
    L.append(s+' '*(n//3)+s) # 중 구간
  for s in stars: 
    L.append(s*3) # 하 구간
		
  return L

print('\n'.join(star(num)))
```

아래는 star(3)의 결과값
```text
['***', '* *', '***']
```

아래는 star(9)의 결과값
```text
['*********', '* ** ** *', '*********', '***   ***', '* *   * *', '***   ***', '*********', '* ** ** *', '*********']
```