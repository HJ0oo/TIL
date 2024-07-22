배열 생성 관련 어이 없는 실수

```python
#오답
array=[]
for i in range(N):
    row=[]
    for j in range(M):
        row.append(list(map(int,input().split())))
        print(row)
    array.append(row)
```


```python
#정답
input_array=[]
for i in range(N):
    row=list(map(int,input().split()))
    input_array.append(row)
```