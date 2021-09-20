# Z

## 백준 1074번 : Z

### 1. 시간초과 풀이

```text
result = 0
N, X, Y = map(int, input().split(' '))

def solve(n, x, y):
    global result
    if n == 2:
        if x == X and y == Y:
            print(result)
            return
        result += 1
        if x == X and y + 1 == Y:
            print(result)
            return
        result += 1
        if x + 1 == X and y == Y:
            print(result)
            return
        result += 1
        if x + 1 == X and y + 1 == Y:
            print(result)
            return
        result += 1
        return
    solve(n / 2, x, y)
    solve(n / 2, x, y + n / 2)
    solve(n / 2, x + n / 2, y)
    solve(n / 2, x + n / 2, y + n / 2)

solve(2 ** N, 0, 0)
```

### 2. 정답 풀이

```text
def Z(x, y, N):
    global res
    if x == r and y == c:
        print(res)
        exit(0)
    elif N == 1:
        res += 1
        return
    if not (x <= r < x + N) and not (y <= c < y + N):
        res += N ** 2
        return
    Z(x, y, N // 2)
    Z(x, y + N // 2, N // 2)
    Z(x + N // 2, y, N // 2)
    Z(x + N // 2, y + N // 2, N // 2)

def main():
    global res
    res = 0
    Z(0, 0, 2 ** N)

if __name__ == "__main__":
    N, r, c = map(int,input().split())
    main()
```