# 240711_3_HowToUseGit
> # GIT
> 코드의 버전 관리, 이전 버전과 변경 비교, 개발과정 추적
<br>
<br>




# GIT의 이해 - 분산버전관리시스템
### 분산‘버전관리시스템'
변화를 기록하고 추적. **버전**을 관리하는 것<BR>
만약 전체 내용을 전부 저장한다면 저장용량이 기하급수적으로 많아짐. 따라서 과거로부터의 **변경사항만**을 저장.<BR>
마지막 파일과 변경사항만을 저장

### ‘분산’버전관리시스템
**중앙**<BR>
버전은 중앙 서버에 저장되고 중앙서버에서 파일을 가져옴 <BR>
vs <BR>
**분산**<BR>
버전을 여러 개의 복제된 저장소에 저장 및 관리
- 중앙 서버 의존하지 않고 동시에 다양한 작업을 수행할 수 있다
- 중앙 서버의 장애나 손실에 대비하여 백업 복구 용이
- 인터넷 연결 안되어있어도 가능. 일단 저장하고 나중에 중앙이랑 동기화하면 되니까.
- 같은 버전을 백업 여러개 하는 것
<BR><BR>


# GIT의 3가지 영역
1. Working Directory
   - 개발자가 실제로 작업하고 있는 공간
2. Staging Area
   - 중간 대기실. git add를 통해 Working Directory에서 Staging Area로 추가할 수 있음.
3. Repository
   - git commit을 통해 Staging Area에 있던 파일들이 커밋되어 Repository로 이동. 


# GIT 문법
**git init** : 로컬 저장소 설정 초기화<BR>
git의 버전관리를 시작할 디렉토리에서 진행<BR>
주소에 (master)가 있다? git의 영역이다<BR>
- git은 하위폴더에 영향을 미침
- **주의 : 하위 폴더에서 다시 git init을 선언하면 해당 하위폴더는 git에서 볼수가없음!(가장 바깥 쪽 저장소가 안쪽 저장소를 읽을수없음) 관리하고자 하는 최상단에서만 git init하기**
- 실수했다면 복구방법 <BR>숨긴항목 지우면 됨! 실수한 위치에서 .git파일 지우면됨!
  
---
**git add** : 변경사항이 있는 파일을 staging area로 add<BR>
**git add .** : 현재있는위치 전부 올리기 : 여러개를 한꺼번에 올리는 방법<br>
**git status** : 현재 로컬 저장소의 파일 상태를 보여줌. *중간중간 계속 확인하기!!* <br>
**git commit** : staging area에 있는 것들을 repository에 기록 저장소에 기록. 해당시점 버전을 생성하고 변경이력을 남기는것.<br>
**git commit -m “메시지”** : 저장소 영역에 올리기 위해. 버전의 이름이라고 할 수 있는 커밋의 메시지를 정해줘야 함.<br>


- 처음에 이 작업을 하면 오류가 뜰 것. 이 커밋을 누가 만들어줬는지 알려줘야 하기 때문.<br>
- **git config --global user.email "이메일주소"** <br>
- **git config --global user.name "이름"**<br>
- --global 이기 때문에 한 번 하면 더 이상 요구되지 않음<br>
- **git config --global -l** : 정상 등록되었는지 확인.

**git log** : commit history 보기. 지금 보고 있는 게 repository임. 단점 - 여러줄을 차지함<br>
**git log --oneline** : 그래서 이렇게 짧게 만들수있음.<br>

# Remote Repository
원격 저장소에 저장. 대표적 - gitlab, github, bitbucket
### README file
- 파일의 이름이 반드시 README여야 함.
- 이 저장소에 대한 가이드
- 예시) 파이썬은 오픈소스 언어이므로 python의 README 파일을 볼 수 있음

### remote 
git remote add ***orgin*** remote_repo_url<br>
**로컬에서 원격 저장소에 대해 마음대로 별칭을 짓는 것이라고 생각하기<br>**
git remote add orgin ***remote_repo_url***<br>
**원격저장소의 링크**<br>
**git remote -v**<br>현재 디렉토리와 연결된 원격 저장소가 어디인지 확인

### push
원격 저장소의 상태와 로컬 저장소의 상태가 같아지는 것<br>
push하면 **변경사항만** 올리는 것<br>
**git push origin master**


### pull
push와 달리, **전부** 내려받는 것<br>
변경사항 직전의 상황이 같아야 pull 가능<br>
그래서 pull에서 오류가 나는 경우가 잦으므로 주의하기

### clone
**git clone** remote_repo_url<br>
clone을 받았다면 git init 필요없음

---
 
### Gitignore
추적하지 못하게 git의 관리에서 빼는 것.
.gitignore 확장자 없이
.으로 시작하는 건 주로 숨김 파일이나 설정 파일


> 참고
> 예시) git log 를 했을 때 너무 길면 오류가 뜸
> 1. q를 눌러서 quit 하거나
> 2. 엔터키를 계속 치면 됨