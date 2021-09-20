# 내림차순 정렬

## 백준 1427번 : 소트인사이드

### 1. 선택 정렬 풀이

```text
n=list(map(int, input()))
for i in range(len(n)):
  # 리스트의 각 원소를 max_index로 잡고 반복문 실행
  max_index=i
  for j in range(i+1, len(n)): # 메인 로직
    if(n[max_index]<n[j]):
      max_index=j
  n[i], n[max_index]= n[max_index],n[i]
b=""
for i in n:
  b=b+str(i)
print(b)
```

위 풀이는  
선택 정렬을 내림차순으로 진행한 것과 같다.  

### 2. 버블 정렬(참고)

```text
def bubbleSort(x):
	length = len(x)-1
	for i in range(length):
		for j in range(length-i):
			if x[j] > x[j+1]:
				x[j], x[j+1] = x[j+1], x[j]
	return x
```

### 3. 삽입 정렬(참고)
```text
def insert_sort(x):
  for i in range(1, len(x)):
    j = i - 1
    key = x[i]
    while x[j] > key and j >= 0:
      x[j+1] = x[j]
      j = j - 1
    x[j+1] = key;
  return x
```



