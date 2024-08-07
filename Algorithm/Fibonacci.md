# 피보나치
## 재귀호출 recursive call
```py
def fibonacci_recursive(n): # O(n^2)
    if n <= 1:
        return n
    return fibonacci_recursive(n-1) + fibonacci_recursive(n-2)
```
## 메모이제이션 memoization
- 이전에 계산한 값을 메모리에 저장해서 매번 다시 계산하지 않도록 하는 방식
```py
def fibo1(n): # O(n)
  global memo
  if n >= 2 and memo[n] == 0 : # memo[n] == 0 : fibo1(n)이 계산된 적이 없으면
    memo[n] = fibo1(n-1) + fibo1(n-2)
  return memo[n]

memo = [0] * (n+1)
memo[0] = 0
memo[1] = 1
```

## DP(Dynamic Programming) 동적계획알고리즘
> DP에는 재귀적 방식과 반복적 방식이 있다.<br>
> 
> 재귀적 방식 (Recursive with Memoization) : 메모이제이션을 활용한 재귀적 방식은 이미 계산된 값을 저장하여 중복 계산을 방지한다.<br>
> 반복적 방식 (Iterative) : 반복적 방식은 테이블을 사용하여 하위 문제부터 순차적으로 해결한다.

> 똑같이 값을 구할 수 있다면 메모이제이션은 재귀를 사용하여 함수가 되돌아갈 곳도 정해야하고 ...<BR> 
> 함수가 짧다면 함수 내부를 실행하는 시간보다 호출,복귀하는 시간이 더 걸릴수도.<BR>
> 그래서 피보나치 수열의 경우 호출 복귀 시간이 불필요해지므로 반복구조가 더 빠르다.(DP가 더 좋을 것)<BR>
```py
def fibo2(n) :
  f = [0] * (n+1)
  f[0] = 0
  f[1] = 1
  for i in range(2,n+1) :
    f[i] = f[i-1] + f[i-2]
  return f[n]
```


## DP 관련 - 연속행렬 곱셈 해보기
- 