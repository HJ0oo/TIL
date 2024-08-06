### 방법 1. gitlab에서 settings > respository > mirroring repositories 옵션
admin 계정이 아니라 미러링 불가.
### 방법 2. 그냥 평소에 push 하듯이, gitlab 연결된 곳에서 <BR>**$ git push --mirror "원하는 github 주소"**
성공! 앞으로 gitlab에서의 작업을 미러링해서 github에 모을 수 있다!<br>
잔디도 빈 곳 없이 심을 수 있을듯😊

### 방법 3. 새로운 레포에서...
1. $ git subtree add --prefix=**기존**리포지토리명 **기존**리포지토리주소 **기존**브랜치명<br>
예시) $ git subtree add --prefix=TIL https://github.com/ihjkong/TIL.git master<br>
2. $ git push origin master<br>
찾아본 레퍼런스와 달리, 오류가 발생하지 않고 정상 작동되어 수월하게 진행