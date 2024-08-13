# 스택
> 자료 **쌓아 올린 형태**의 자료구조
> 스택에 저장된 자료는 선형 구조를 가진다.
> - 선형구조 : 자료 간 1대 1의 관계
> - 비선형구조 : 자료 간 1대 N의 관계(ex.트리)
> 
> 
><자료구조>
> - **LIFO(Last-In-First-Out) 후입선출**
> - 배열 사용 가능
> - 저장소 자체를 스택이라 부르기도 함
> - 스택에서 **마지막 삽입된 원소의 위치**를 **top**이라고 부른다.
>
><연산>
> - 삽입 **push**
> - 삭제 **pop**
> - 스택이 공백인지 확인 **isEmpty**
> - 스택의 top에 있는 item을 반환 **peek**




스택을 활용한 복잡한 알고리즘을 다룰 때는 우선적으로 전체 구조 파악하기.

## 스택의 push 알고리즘
```py
def push(item):
  s.append(item) # append는 사실 연산이 느린 편임...

def my_push(item,size):
  global top
  top += 1
  if top == size : # 디버깅용 코드(더 이상 못 넣어!)
    return "overflow"s
  else : stack[top] = item
```

## 스택의 pop 알고리즘
- my_pop(pop은 이름이 겹치니까)
- 지울 필요 없음 주의하기

```py
def my_pop_1():
  if len(s) == 0 :
    return
  else : return s.pop()

def my_pop_2():
  global top
  if top == -1 :
    return "underflow"
  else :
    top -= 1
    return stack[top+1]

def my_pop_3():
  global top
  if top > -1 :
    top -= 1
    return stack[top+1]
  return "underflow"
```

```py
# 스택 구현하기
stack_size = 10
stack = [0] * stack_size
top = -1

my_push('첫번째',size)
my_push('두번째',size)
print(stack)            # ['첫번째', '두번째', 0, 0, 0, 0, 0, 0, 0, 0]
print(my_pop_2())       # 두번째
print(my_pop_2())       # 첫번째
print(my_pop_2())       # underflow
```
## 스택 구현 고려사항
- 1차원 배열 사용할 경우 구현 용이하지만, 초기에 스택의 크기를 변경하기 어렵다는 단점이 있다.
#### **스택의 동적 구현**
- 저장소 동적 할당하여 스택 구현
- 동적 연결 리스트를 이용하여 구현
- 구현이 복잡하지만, 메모리를 효율적으로 사용할 수 있음.
- 스택의 동적 구현 - C언어와 C++로도 해볼 것

## Python - 연결 리스트 활용 스택 동적 구현
```py
#1 내장 리스트를 이용한 구현
class StackUsingList:
    def __init__(self):
        self.stack = []

    def push(self, item):
        self.stack.append(item)
# 사용 예시
stack = StackUsingList()
stack.push(10)
stack.push(20)
print(stack.stack)  # [10, 20]



#2 연결 리스트를 이용한 구현
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class StackUsingLinkedList:
    def __init__(self):
        self.top = None

    def push(self, item):
        new_node = Node(item)
        new_node.next = self.top
        self.top = new_node

# 사용 예시
stack = StackUsingLinkedList()
stack.push(10)
stack.push(20)
current = stack.top
while current:
    print(current.value, end=" ")  # 20 10
    current = current.next
```


## C, C++ - 스택 동적 구현
```c

```

```cpp

```


## 스택 응용 문제
- 괄호검사 () {}
- 반복 문자 지우기
  - ex) abbc : 전체 문자열 하나씩 stack에 쌓기. ab일 때 b가 top이니까 top과 새로 들어오는 문자 b 비교 ...



###### 참고) python에 비해 pypy 장점 - 빠름, 서버쪽 부담이 적음
참고 ) 스택을 리스트로 구현할 때 굳이 [-1] 이렇게 마이너스 인덱스는 쓰지말자.. 스택 특성 이용해!




괄호문제에서
```py
pair ={ '{':'}' , '(':')'}
```
if문보다 처리속도 빠름
그냥 인덱스 꺼내오니까
파이프라이닝? 으로 인해 if나 for가 나타나면 별로 좋지 않음
아까 불러놓은 애들 필요없네 기다려봐 느낌이라서
실제로 막 효율이 떨어지는건 아니지만
'최적'의 코드가 될수는없다




## 스택 활용
- 계산기