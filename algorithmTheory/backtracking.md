백트래킹(backtracking)
===
# 백트래킹 : 제약 조건 만족 문제에서 해를 찾기 위한 전략  

- 해를 찾기 위해, 후보군에 제약 조건을 점진적으로 체크하다가,  
해당 후보군이 제약 조건을 만족할 수 없다고 판단되는 즉시 backtrack (다시는 이 후보군을 체크하지 않을 것을 표기)하고,  
바로 다른 후보군으로 넘어가며, 결국 최적의 해를 찾는 방법  
- 실제 구현시, 고려할 수 있는 모든 경우의 수 (후보군)를 상태공간트리(State Space Tree)를 통해 표현  
- 상태 공간 트리를 탐색하면서, 제약이 맞지 않으면 해의 후보가 될만한 곳으로 바로 넘어가서 탐색
- Promising: 해당 루트가 조건에 맞는지를 검사하는 기법
- Pruning (가지치기): 조건에 맞지 않으면 포기하고 다른 루트로 바로 돌아서서, 탐색의 시간을 절약하는 기법

# 상태 공간 트리  

![state-space-tree](https://user-images.githubusercontent.com/55550753/138076351-0909b34a-bc1a-4b34-ad1a-4ac49dde55a8.PNG)  

# N-queen 문제

NxN 크기의 체스판에 N개의 퀸을 서로 공격할 수 없도록 배치하는 문제

![n-queen1](https://user-images.githubusercontent.com/55550753/138076489-5a0fe75d-0b2c-4e3d-886f-0ce39133816f.PNG)  

# N-queen 해결

![n-queen2](https://user-images.githubusercontent.com/55550753/138076525-de12f95f-e019-4571-80c9-d4198ff39b24.PNG)

![n-queen3](https://user-images.githubusercontent.com/55550753/138076592-4fee9a44-00a4-4f56-9483-ccb95a5ff311.PNG)

# N-queen 문제 해결 코드

```text
def is_available(candidate, current_col):
    current_row = len(candidate)
    for queen_row in range(current_row):    
        if candidate[queen_row] == current_col or abs(candidate[queen_row] - current_col) == current_row - queen_row:
            return False
    return True


def DFS(N, current_row, current_candidate, final_result):
    if current_row == N:
        final_result.append(current_candidate[:])
        return
    
    for candidate_col in range(N):
        if is_available(current_candidate, candidate_col):
            current_candidate.append(candidate_col)
            DFS(N, current_row + 1, current_candidate, final_result)
            current_candidate.pop()


def solve_n_queens(N):
    final_result = []
    DFS(N, 0, [], final_result)
    return final_result

print(solve_n_queens(4)) 
```