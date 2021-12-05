---
description: '#자료 구조 #정렬 #해시를 사용한 집합과 맵'
---

# 백준 1302번 : 베스트셀러

### 1. 풀이

```text
n=int(input())

books=dict()

for _ in range(0,n):
  book=input()
  if(book in books):
    books[book]+=1
    continue
  books[book]=1

most_selled=''
max_value=0

for key, value in sorted(books.items(), reverse=True):
  max_value=max(max_value, value)
  if(max_value==value):
    most_selled=key

print(most_selled)
```
---