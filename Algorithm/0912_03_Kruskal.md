# 서로소 집합(상호배타 집합)
> ## 표현 방법
> - 연결리스트
> - 트리
>
> ## 상호배타 집합 연산
> - Make-Set(x) : 초기 설정
> - Find-Set(x) : 대표자가 누구니?
> - Union(x)    : 같은 집합으로 묶어주자
> <br>
> <br>

## 상호배타집합 표현 - 연결리스트
- 같은 집합의 원소들은 하나의 연결리스트로 관리한다.
- 연결리스트의 맨 앞의 원소를 집합의 대표 원소로 삼는다.
- 각 원소는 집합의 대표 원소를 가리키는 링크를 갖는다.

## 상호배타집합 표현 - 트리
- 하나의 집합을 하나의 트리로 표현한다.
- 자식 노드가 부모 노드를 가리키며 루트 노드가 대표자가 된다.
![상호배타집합 표현 트리 대체이미지](./image/Union-Find-1.PNG)
- Make-Set(x) : 유일한 멤버 x를 포함하는 새로운 집합을 생성하는 연산. 자기 자신을 대표자로 선정.
- Find-Set(x) : x를 포함하는 집합을 찾는 연산. 자기 자신이 대표라면 자기 자신을 return, 아니라면 Find-Set(부모)
- Union(x,y) : x와 y를 포함하는 두 집합을 통합하는 연산. 대표자끼리 합치는 것. y의 대표자를 x의 대표자와 동일하게 함.


## 파이썬으로 구현
```py
'''
7 11
0 1 32
0 2 31
0 5 60
0 6 51
1 2 21
2 4 46
2 6 25
3 4 34
3 5 18
4 5 40
4 6 51
'''

V, E = map(int, input().split())    # V 마지막 정점, 0~V번 정점. 개수 (V+1)개
edge = []
for _ in range(E):
    u, v, w = map(int, input().split())
    edge.append([u, v, w])  # 출발, 도착, 가중치 묶어서 저장 (간선 정보들을 모두 저장)
edge.sort(key=lambda x: x[2])  # 가중치 기준으로 오름차순 정렬
parents = [i for i in range(V)]       # 대표원소 배열


def find_set(x):
    if parents[x] == x:
        return x

    parents[x] = find_set(parents[x])  # 경로 압축
    return parents[x]


def union(x, y):
    root_x = find_set(x)
    root_y = find_set(y)

    if root_x == root_y:
        return

    # 더 작은 루트노트에 합친다.
    if root_x < root_y:
        parents[root_y] = root_x
    else:
        parents[root_x] = root_y

# MST의 간선수 N = 정점 수 - 1
cnt = 0     # 선택한 edge의 수 (사용이유: N - 1 가 되면 신장트리 완성) - 시간 효율을 위해 사용
total = 0   # MST 가중치의 합
# print(edge)
for u, v, w in edge:
    # 출발점과 도착점이 같은 그룹에 속해있다면, 이미 연결된 친구들이다.
    # 다른 집합이라면
    if find_set(u) != find_set(v):  # 싸이클이 없다면
        print(u, v, w)  # 선택한 순서대로 출력
        cnt += 1
        union(u, v)
        total += w
        if cnt == V - 1:  # MST 구성이 끝나면
            break

print(f'최소 비용 = {total}')


```

## 활용 - 그래프는 이미 연결된 노드끼리 또 연결할 경우 cycle이 발생함. **cycle을 찾을 때 union-find를 이용할 것.**