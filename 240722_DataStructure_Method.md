> 헷갈렸던 것들만 정리

# List
```python
list1.sort()              # 정답. 이것만으로 list1의 순서 정렬됨
result = (list1.sort())   # 오답. result = None
```

# String
```python
string.split() # 리스트 형태를 반환
string.title() # 단어별 첫 글자를 대문자 바꿔줌
string.isdecimal() # 문자열인데, 그 문자열이 모두 0~9의 숫자 문자로만 이루어졌는지
```

## 기타
1. 형변환 잘 생각하기
2. 리스트 길이만큼 반복할 떄 주의하기 - range 잊지 말고 적기
```python
for _ in range(len(list))
```
3. 여러 값을 return 할 때
```python
return tuple(input_list[0],input_list[len(input_list)-1]) # 이렇게 하면 오류
'''
TypeError: tuple expected at most 1 argument, got 2
'''
return input_list[0],input_list[len(input_list)-1] # 이렇게 해야함
```
4. 쭉 나열해서 print해야할 때
```python
for i in arr:
    print(data_2[i],end='') # end를 \n 이 아닌 공백으로!
```

> **파이썬 공식문서** [https://docs.python.org/ko/3/library/functions.html#print]
> ```python
> print(*objects, sep=' ', end='\n', file=None, flush=False)
> ```
> Print objects to the text stream file, separated by sep and followed by end. sep, end, file, and flush, if present, must be given as keyword arguments.<br>
> 모든 비 키워드 인자는 str() 이 하듯이 문자열로 변환된 후 스트림에 쓰이는데, sep 로 구분되고 end 를 뒤에 붙입니다.<br>
> sep 과 end 는 모두 문자열이어야 합니다; None 일 수도 있는데, 기본값을 사용한다는 뜻입니다.<br> objects 가 주어지지 않으면 print() 는 end 만 씁니다. <br>
> file 인자는 write(string) 메서드를 가진 객체여야 합니다; 존재하지 않거나 None 이면, sys.stdout 이 사용됩니다. 인쇄된 인자는 텍스트 문자열로 변환되기 때문에, print() 는 바이너리 모드 파일 객체와 함께 사용할 수 없습니다. 이를 위해서는. 대신 file.write(...) 를 사용합니다. <br>
