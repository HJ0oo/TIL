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

> **<파이썬 공식 문서>** [https://docs.python.org/3/library/functions.html#reversed]<br>
> The reverse() method modifies the sequence in place for economy of space when reversing a large sequence. To remind users that it operates by side effect, it does not return the reversed sequence.<br>

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
- 중요한 점 : reverse는 **reversed 객체**를 반환. reverse(l)만으로는 바뀌지 않음!
- output = reverse(l) 이렇게 값을 할당해야 함.
- list : <**listreverseiterator** object at 0x101053c10>
- tuple , string : <**reversed** object at 0x101053b50>

```python
list(reversed(t)) # 리스트 형태로
tuple(reversed(t)) # 튜플 형태로
''.join(reversed(t)) # 문자열 형태로
```
이런 식으로 변환해서 사용하면 된다.



> **<파이썬 공식 문서>** [https://docs.python.org/3/library/functions.html#reversed]<br>
> reversed(**seq**)<br>
> Return a reverse iterator. seq must be an object which has a __reversed__() method or supports the sequence protocol (the __len__() method and the __getitem__() method with integer arguments starting at 0).<br>

<br>
<br>


## 정리
> ```python
> list.reverse()
> output_seq = reversed(input_seq)
> ```

