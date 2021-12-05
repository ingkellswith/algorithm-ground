---
description: '#더블 스택 #자료 구조 #스택 #연결 리스트'
---

# 키 로거

## 백준 5397번 : 키로거

### 1. 풀이

```text
test_case = int(input())
for _ in range(test_case):
  left_stack = []
  right_stack = []
  data = input()
  for i in data:
    if i == '-':
      if left_stack:
        left_stack.pop()

    elif i == '<':
      if left_stack:
        right_stack.append(left_stack.pop())

    elif i == '>':
      if right_stack:
        left_stack.append(right_stack.pop())

    else:
      left_stack.append(i)

  left_stack.extend(reversed(right_stack))
  print(''.join(left_stack))
```

