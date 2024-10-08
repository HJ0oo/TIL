# 240711_1_Markdown

> # Markdown
> 개발자들이 텍스트와 코드를 작성해 문서화하는 방법 <br>
> 확장자 .md
---
<br>
<br>

# 제목1
## 제목2
### 제목3
#### 제목4
##### 제목5
###### 제목6 _ 6까지만 지원

---
<br>

- 순서가 없는 리스트
  - 스페이스 2번 넣고 하위 리스트
  - 하위 리스트
    - 하위하위

1. 순서가
2. 있는
3. 리스트
<br>

//1로만 써도 알아서 고쳐줌
1. 순서가
   1. 이것도 스페이스 2번(오류시 1번더)
   2. 하면 하위 리스트로.
2. 있는
3. 리스트 

---
<br>
print("hello") 라고만 쓰면 그냥 텍스트임.
파이썬의 코드로 구현하려면,           //Code Blocks

```python     
print("hello")                      
```

오늘 파이썬을 배웠는데
`print`라고 하는 것을 배웠다.        //Inline Code Block

---
<br>

[최종으로 출력될 텍스트;Google로 이동](https://google.com)//링크 삽입 방법<br>

![이미지에 문제가 생길 시 대체텍스트](https://picsum.photos/200/300) //이미지 삽입 방법(느낌표를 앞에 붙이기) 온라인 상 이미지 주소.

![예시이미지](./images/image_example.png) //동일한 경로에 있으니까 ./image_example.png <br>
이미지파일을 markdown에 집어넣은 것이 아니라 경로에 있는 것을 출력한 것에 불과하므로 같이 움직여야 함. 그래서 보통 images 폴더를 따로 만듦. ./images/image_example.png

---
<br>

**굵게**<br>
애스터리스크(asterisk) 2개<br>
또는 __underbar 2개__

*기울임*<br>
애스터리스크(asterisk) 1개<br>
또는 _underbar 1개_

~~취소선~~<br>
~ 2개

---
<br>

> 인용문(출처쓸때)

> 여기 인용문 내부에서
> 
> ```python
> print("내부에서도 가능")
> ```

---
<br>

### 마크다운을 조금 더 쉽게 하는 방법
- Typora
- Marktext
- vscode내에서 markdown all in one extension 설치