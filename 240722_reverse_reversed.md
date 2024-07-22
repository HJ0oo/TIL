# reverse 와 reversed 의 차이
## reverse는 **list타입**에서 제공하는 함수
```python
l = ['a', 'b', 'c']
t = ('a', 'b', 'c')
d = {'a': 1, 'b': 2, 'c': 3}
s = 'abc'

l.reverse()  # list의 순서를 뒤집어줌
t.reverse()  # AttributeError: 'tuple' object has no attribute 'reverse'
d.reverse()  # AttributeError: 'dict' object has no attribute 'reverse'
s.reverse()  # AttributeError: 'str' object has no attribute 'reverse'
```
- 중요한 점 : reverse는 **값을 반환하지 않고** 순서만 뒤섞음.
- l.reverse() 라고 쓰면 충분.


## reversed는 list에서 제공하는 함수가 아니라 **내장함수**
```python
l = ['a', 'b', 'c']
t = ('a', 'b', 'c')
d = {'a': 1, 'b': 2, 'c': 3}
s = 'abc'

reversed(l)  # <listreverseiterator object at 0x101053c10>
reversed(t)  # <reversed object at 0x101053b50>
reversed(d)  # TypeError: argument to reversed() must be a sequence
# 딕셔너리는 순서가 없으니까 불가능
reversed(s)  # <reversed object at 0x101053c10>
```
- 중요한 점 : reverse는 **reversed 객체**를 반환
- list : <**listreverseiterator** object at 0x101053c10>
- tuple , string : <**reversed** object at 0x101053b50>

```python
list(reversed(t)) # 리스트 형태로
tuple(reversed(t)) # 튜플 형태로
''.join(reversed(t)) # 문자열 형태로
```
이런 식으로 변환해서 사용하면 된다.


> <정리> <br>
> list.reverse() <br>
> output_seq = reversed(input_seq)

