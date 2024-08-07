# DFS와 BFS
> 비선형구조인 그래프 구조에서 모든 자료 빠짐없이 검색
## 깊이 우선 탐색 (DFS: Depth-First Search)
DFS는 가능한 한 최대한 깊이 들어가면서 노드를 탐색하는 방법.
- 순서: 한 방향으로 끝까지 탐색 후, 다른 방향 탐색
- **스택** 또는 **재귀**를 사용
- 갈림길에서 하나 선택해서 탐색하고 가장 마지막에 만났던 갈림길의 정점으로 되돌아가서 다시 깊이 우선 탐색 반복해야 하므로 후입선출 구조의 스택 사용

### **예시 코드 (스택)**
```python
# 1번 코드 - set 사용
def dfs_stack(graph, start):
    visited = set()
    '''
    set()를 쓰는 이유 
    # 빠른 검색 - vertex not in visited
    해시 테이블 기반 자료구조이므로 시간복잡도 O(1).
    리스트를 사용한다면 리스트 전체를 탐색해야 하므로 시간복잡도 O(n)임.
    # 삽입 - .append(vertex) vs .add(vertex)
    append는 중복 노드 허용하므로 복잡.
    set는 중복 제거니까 간단.
    ''' 
    stack = [start]
    
    while stack:                  # 아무것도 없으면 다 후진한거 - 제일 처음으로 돌아온거 - 완료!
        vertex = stack.pop()      # 스택에 쌓아 두고 pop으로 후진하기
        if vertex not in visited: # 방문하지 않은 갈래로 이동
            visited.add(vertex)
            stack.extend(neighbor for neighbor in graph[vertex] if neighbor not in visited) # push를 사용하는 방법은 아래 기재(3번 코드)
    
    return visited
```    
```py
# 2번 코드 - 리스트를 사용하면서도 O(1)
'''
노드 개수에 맞춘 리스트 초기화

노드의 개수에 맞춰 리스트를 초기화하고, 모든 값을 0으로 설정한다.
예: 7개의 노드가 있다면 visited = [False] * 7로 초기화한다.
방문한 노드의 인덱스를 'True'로 설정

노드를 방문할 때 해당 노드의 인덱스에 해당하는 위치를 'True'로 설정한다.
예: C 노드를 방문하면 visited[C_index] = True로 설정한다.

<장점>
상수 시간 복잡도: 방문 여부를 확인하는 데 O(1) 시간이 걸린다. 인덱스를 직접 사용하기 때문에 탐색 시간이 매우 빠르다.

간단한 구현: 인덱스를 사용한 간단한 접근 방법으로 코드가 간결하다.

<단점>
메모리 사용: 노드 수가 많을 경우, visited 리스트의 메모리 사용량이 많아질 수 있다. 하지만 인덱스가 연속적이고 범위가 적은 경우에는 큰 문제가 되지 않는다.

노드 인덱스 관리: 노드의 인덱스가 연속적이고 정수여야 한다. 인덱스가 정수 범위를 벗어나거나 비연속적일 경우에는 추가적인 매핑 작업이 필요하다.
'''

def dfs_index_based(graph, start, visited):
    stack = [start]
    
    while stack:
        vertex = stack.pop()
        if not visited[vertex]:  # 노드가 방문되지 않은 경우
            visited[vertex] = True  # 노드를 방문으로 표시
            stack.extend(neighbor for neighbor in graph[vertex] if not visited[neighbor]) # extend를 사용할 때는 한 번에 이웃 노드들을 모두 추가할 수 있어 코드가 간결해질 수 있다. push를 사용하는 방법은 아래 기재(3번 코드)
    
    
    return visited

# 예시 그래프 (노드 인덱스는 0부터 시작한다고 가정)
graph = {
    0: [1, 2],  # 노드 A
    1: [0, 3, 4],  # 노드 B
    2: [0, 5],  # 노드 C
    3: [1],  # 노드 D
    4: [1, 5],  # 노드 E
    5: [2, 4]  # 노드 F
}

# 방문 배열 초기화 (노드 6개)
visited = [False] * 6

# 실행
print(dfs_index_based(graph, 0, visited))  # 출력: [True, True, True, True, True, True] (모든 노드 방문됨)

```
```py
# 3번 코드 - extend 대신에 push 사용
def dfs_push_based(graph, start, visited):
    stack = [start]
    
    while stack:
        vertex = stack.pop()
        if not visited[vertex]:
            visited[vertex] = True  
            for neighbor in reversed(graph[vertex]):  # 이웃 노드들을 역순으로 추가
                if not visited[neighbor]:
                    stack.append(neighbor)  # 스택에 이웃 노드를 추가
    
    return visited
```
# 
#### (스택) 전체 코드 정리
```py
def build_adjacency_list(edges, num_nodes):
    # 인접 리스트 초기화 (인덱스 0은 빈 리스트로 두고, 1부터 num_nodes까지 사용)
    graph = [[] for _ in range(num_nodes + 1)]
    
    for i in range(0, len(edges), 2): # 노드 한 개 당 숫자 2개니까
        u = edges[i]
        v = edges[i + 1]
        
        graph[u].append(v)
        graph[v].append(u)
    
    return graph

def dfs_stack_based(graph, start, visited):
    # 방문 배열 초기화 (노드 번호가 1부터 시작한다고 가정)
    visited = [False] * (num_nodes + 1)
    stack = [start]
    
    while stack:
        vertex = stack.pop()
        if not visited[vertex]:  # 노드가 방문되지 않은 경우
            visited[vertex] = True  # 노드를 방문으로 표시
            for neighbor in reversed(graph[vertex]):  # 이웃 노드들을 역순으로 추가
                if not visited[neighbor]:
                    stack.append(neighbor)  # 스택에 이웃 노드를 추가
    
    return visited

# 입력 받기
input_edges = input("Enter the edges (space-separated): ").split()
input_edges = list(map(int, input_edges))

num_nodes = int(input("Enter the number of nodes: "))

# 그래프 생성
graph = build_adjacency_list(input_edges, num_nodes)

# 시작 노드 입력 받기
start_node = int(input("Enter the start node: "))

# DFS 실행
visited_nodes = dfs_stack_based(graph, start_node)

# 방문 결과 출력
print("Visited nodes:")
for node in range(1, num_nodes + 1):
    if visited_nodes[node]:
        print(node, end=' ')
print()

# 예시 입력과 출력
# 입력 예시:
# Enter the edges (space-separated): 1 2 2 3 3 4 4 5 1 5
# Enter the number of nodes: 5
# Enter the start node: 1

# 출력 예시 (DFS 탐색 결과, 노드 1을 시작으로 탐색):
# Visited nodes:
# 1 2 3 4 5

```








### **예시 코드 (재귀)**
```python
  def dfs(graph, start, visited=None):
      if visited is None:
          visited = set()
      visited.add(start)
      for neighbor in graph[start]:
          if neighbor not in visited:
              dfs(graph, neighbor, visited)
      return visited

  # 예시 그래프
  graph = {
      'A': ['B', 'C'],
      'B': ['A', 'D', 'E'],
      'C': ['A', 'F'],
      'D': ['B'],
      'E': ['B', 'F'],
      'F': ['C', 'E']
  }

  # 실행
  print(dfs(graph, 'A'))  # 출력: {'A', 'B', 'C', 'D', 'E', 'F'}
```
















탐색 과정에서 방향존재하지않음(무향,무방향그래프)/ 유향그래프 양방향인지 단방향인지
보통 '출발 도착'으로 저장
저장하는 순간 결정되어버림
나중에 트리 다룰때 방향성 문제됨








<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>

## 너비 우선 탐색 (BFS: Breadth-First Search)
- BFS는 현재 노드와 인접한 노드들을 먼저 탐색하는 방법.
- 큐를 사용
- 순서: 같은 레벨의 노드들을 먼저 탐색 후, 다음 레벨 탐색
```py
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])
    visited.add(start)

    while queue:
        vertex = queue.popleft()
        for neighbor in graph[vertex]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
    return visited

# 예시 그래프
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A', 'F'],
    'D': ['B'],
    'E': ['B', 'F'],
    'F': ['C', 'E']
}

# 실행
print(bfs(graph, 'A'))  # 출력: {'A', 'B', 'C', 'D', 'E', 'F'}
```
## DFS와 BFS의 차이 요약
> DFS: 깊이 우선, 스택/**재귀** 사용, 더 깊이 있는 노드를 먼저 방문<BR>
> BFS: 너비 우선, 큐 사용, 같은 레벨의 노드를 먼저 방문 <BR>
> (재귀 잊지않기. 단순하게 'DFS는 스택, BFS는 큐' 라고 외우지 않기)