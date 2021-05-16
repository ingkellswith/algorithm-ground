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
    # 아래 함수는 끝까지 셌을 경우 4개의 재귀함수를 모두 실행해야 하지만
    # 초반 숫자만 필요할 경우 굳이 모든 재귀함수를 다 실행할 필요가 없다.
    # 따라서 조건문을 걸어서 필요한 재귀함수까지만 실행하게 해야 한다.
    solve(n / 2, x, y)
    solve(n / 2, x, y + n / 2)
    solve(n / 2, x + n / 2, y)
    solve(n / 2, x + n / 2, y + n / 2)

solve(2 ** N, 0, 0)
```

### 2. 정답 풀이

```text
def Z(row, col, size, num): # (row,col: 자른 box의 첫번째 인덱스, size: box 사이즈, num: box 시작점의 숫자)
    if size == 2: # 사이즈가 2x2가 됐을 때
        if row == r and col == c:
            print(num)
            return
        num += 1

        if row == r and col + 1 == c:
            print(num)
            return
        num += 1

        if row + 1 == r and col == c:
            print(num)
            return
        num += 1

        if row + 1 == r and col + 1 == c:
            print(num)
            return
        num += 1

    else:
        half_size = size // 2
        # 왼쪽 위
        if row <= r < row + half_size and col <= c < col + half_size:
            Z(row, col, half_size, num)
        # 오른쪽 위
        elif row <= r < row + half_size and col + half_size <= c < col + size:
            Z(row, col + half_size, half_size, num + (half_size ** 2) * 1)
        # 왼쪽 아래
        elif row + half_size <= r < row + half_size * 2 and col <= c < col + half_size:
            Z(row + half_size, col, half_size, num + (half_size ** 2) * 2)
        # 오른쪽 아래
        elif row + half_size <= r < row + half_size * 2 and col + half_size <= c < col + size:
            Z(row + half_size, col + half_size, half_size, num + (half_size ** 2) * 3)


if __name__ == "__main__":
    N, r, c = map(int, input().split())
    Z(0, 0, 2 ** N, 0)
```