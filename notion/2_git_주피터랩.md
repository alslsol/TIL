# 2. git + 주피터 랩

생성 일시: 2025년 2월 12일 오후 3:28
최종 편집 일시: 2025년 2월 19일 오후 4:32

# 1. git 이해하기

## 1.1 특징

### 1) 분산 버전 관리 시스템

- **분산 버전 관리 시스템**: 클라이언트/서버가 동일한 데이터 유지해 버전 관리하는 시스템
    - 동일 콘텐츠 여러 서버에 저장
    - 변화량 트래킹하기 쉬움
    - ex. git
- **로컬 버전 관리 시스템**: 서로 다른 버전 각각 모두 저장하는 방식
    - ex. 최종, 최종1, 최종2... >> 각각 저장
- **중앙집중식 버전 관리 시스템**: ex. 노션 >> 노션 클라우드에만 저장, 로컬 디스크엔 저장X

### 2) 3가지 영역으로 구분: working directory, staging area, repository

![](https://git-scm.com/book/ko/v2/images/areas.png)

- **working directory**: 현재 작성 중인 코드/파일
- **staging directory**: add 명령어로 무대 위로 올라간 파일들
- **git directory**(repository): `commit`으로 찍힌 스냅샷을 저장하는 공간

### 3) CLI 방식

- **CLI**: 명령줄 인터페이스 >> ex. git
- **GUI**: 그래픽 사용자 인터페이스 >> ex. windows

---

## 1.2 git 최초 설정

### 사용자 정보 입력

- git으로 스냅샷 보낼 때, 출처 고정값 설정 필요

```python
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```

### git 저장소 만들기

- `git init`: 현재 디렉토리에 `.git` 폴더 생성해줌
    - 새 폴더를 git 저장소로 만드는 방식
    - 최초 한번만 하면 됨
- `git clone (remote_url)`: 해당 링크의 프로젝트를 복사해서 git 저장소 클론을 만드는 방법
    - `git clone (링크) (폴더명)`: 다른 이름으로 클론 저장 >> 동일명 폴더 이미 존재하면X기 때문
    - 이미 만들어진 git 저장소 복제하는 방식

---

## 1.3 수정/저장

### 용어

- **tracked** 파일: 관리대상 >> 이미 스냅샷에 포함된 파일
    - **modified**: 수정된 상태
    - **unmodified**: 수정X는 동일 상태
- **untracked** 파일: 관리대상X >> 워킹 디렉토리의 파일 중 스냅샷 or staging area에도 오르지 않은 파일

### 과정

- untracked 상태에서 `add` 하면, staged로 올라감
- `commit`하면 unmodified 상태로 넘어가며 트래킹 시작됨
- 여기서 수정 시 modified 상태로 전환됨
- 이때 다시 `commit`하면 unmodified로 회귀

### git 상태 확인

- `git status`: 현재 git 상태를 확인 >> tracked/untracked 파일 구분해 표시
- `.git` 폴더는 자신의 현 위치를 기준으로만 작동 >> TIL 폴더까지만 관리함, DAMF2 폴더는 관리X
    - 새 `.git` 폴더 독립적으로 관리 가능하도록, 상위 폴더에는 또다른 `.git` 폴더 만들면 오류 발생
    - 새로 만들려면: DAMF2 내 TIL 이외 별도 폴더 만든 뒤, 그 하위에 `.git` 폴더 만들면 됨

### remote 저장소

- 인터넷/네트워크 속에 있는 원격 저장소
    - 타인과 협업하기 위해 데이터 `push`/ `pull` 하기 위한 공간
- **생성**: `git remote add (별명) (링크)`
- **삭제**: `git remote remove (별명/링크)`

## 1.4 실습

### 1.4.1 웹페이지 만들기

- 템플릿 다운 >> TIL 폴더 내 새폴더 만들어 템플릿 저장
- 내 맘대로 웹페이지 코드 수정 >> ‘open in browser’ 통해 수정본 확인하며 작업
- 수정한 웹페이지 발행하기

```jsx
git add . # github-page 폴더에서 현재 폴더 기준 모든 데이터를 staging area로 올림
git commit -m "page" #'page' 메시지 달아서, 스냅샷 찍음
git remote add origin <https://github.com/alslsol/alslsol.github.io/settings> #원격 저장소에 저장
git push origin master #원격 저장소에 올린 내용 웹페이지로 발행
```

### 1.4.2 원격(remote) 저장소를 활용한 협업

- 작업물 저장하기
    - git_hub 들어가서 new repository 만들기

```jsx
git init
git add . #staging area에 올리기
git commit -m "끝말잇기 시작" #스냅샷 찍기
git remote add origin <https://github.com/alslsol/end-to-end> #저장소에 저장
git push origin master #저장소에 발행
```

- 다른 컴퓨터에서, 클론 만들기
    - DAMF2 폴더에서 우클릭해 VScode 열기

```jsx
git clone <https://github.com/alslsol/end-to-end.git>
	# git_hub에서 코드 복사해 클론 저장
```

- 수정/저장하기

```jsx
git add . # 수정한 내용을 staging area로 올림
git commit -m "update" # 수정한 내용 스냅샷 찍음
git push origin master # 스냅샷 git_hub 업로드
```

- 원격 저장소에서 데이터 불러오기

```jsx
git pull origin master # git_hub에 저장된 커밋 불러옴
```

- 동기화된 내용 가져오기 전에 내 파일 수정하면X >> pull한 다음 수정해야 함
- 만약 이미 수정본 commit해서 가져오려는 파일과 충돌했다면?
    - 에러 메시지 남 + hint로 git pull 하라고 제안 뜸
    - 이후 git pull 하면 >> 4가지 선택지 뜸 >> 적절히 선택지 클릭
    - 이후 커밋해야 완전히 합쳐지기 완료
        - ex. `git commit -m "merging"`

---

# 1.5 git 명령어 정리

- `git init`
    - 현재 디렉토리에 `.git` 폴더 생성해 >> 새 git 저장소를 초기화
- `git clone {remote_url}`
    - 해당 링크의 프로젝트를 복사해서 git 저장소 클론을 만드는 방법
    - `git clone (링크) (폴더명)`: 다른 이름으로 복사해 저장
- `git status`
    - 현재 git의 상태를 확인 >> tracked, untracked 파일 구분해 표시
- `git add {파일명/폴더명}`
    - working directory에서 변경된 파일을 staging area로 이동
    - ex. `git add .`: 현재 내 위치 기준, 모든 파일/폴더를 staging area로 올림
- `git commit -m "메시지"`
    - staging area에 있는 변경사항을 스냅샷 찍음
    - options:
        - `git commit --amend`: 파일 빠뜨렸거나, 메시지 라벨 수정할 때 >> 되돌려서 다시 커밋하기
- `git log`
    - 커밋의 히스토리 조회
    - `q` 입력 >> 다시 터미널로 나올 수 있음
    - options:
        - `-oneline`: 각 커밋을 한 라인으로 보여줌 >> 많은 커밋을 한 번에 조회 시 유용
        - `-graph`: 각 커밋에 선 달아서 보여줌
- `git remote`
    - 원격 저장소 관리 명령어 >> 데이터 저장할 원격 저장소 지정
    - options:
        - `git remote -v`: 실제 저장된 링크주소 알려줌 >> 근데 링크 매번 언급하기 어려우니, origin이라는 별명으로 대체한 것
        - `git remote add (별명) (링크)`: 원격 저장소 새로 지정 + 링크 대신할 별명 설정
            - 최초 한번만 지정하면 됨 >> `master` 있으면 이미 지정돼 있으니, `git push`만 해도 됨
        - `git remote remove (별명/링크)`: 원격 저장소 지정 삭제
- `git push (별명) master`: 원격 저장소에 저장하기
- `git pull (별명) master`: 원격 저장소에서 데이터 불러오기

## 참고자료) [gitbook](https://git-scm.com/book/ko/v2)

---

# 2. git branch

## 2.1 branch

- 분기를 만들어 가지를 만드는 것
    - 파편화해서 안정적으로 코드 짜기 위함
    - 나눠서 안정성 있게 개발해서, 이후 하나로 합치기 위한 과정임
- 원리: develop branch에서 충분히 수정해 최선의 코드 도출 >> master branch로 가져와 병합(merge)
    - 주의: 어느 branch에 위치해 있는지 확인 필요

## 2.2 명령어 정리

- `git log --oneline`: commit 내력 출력
    - options:
        - `--oneline`: 한 줄로 간략히
        - `--graph`: 그래프 작성
- `git branch`: branch 모두 출력
- `git branch (branch_name)`: 브랜치 생성
- `git switch (branch_name)`: branch 이동/전환
- `git merge (가져올 branch)`: 해당 branch 현재 위치한 branch와 병합

## 2.3 branch 과정

### 생성

```python
git branch testing #testing 브랜치 생성
git switch testing #testing 브랜치로 전환

##master/testing 모두 add-commit 하기
##testing 브랜치에서만 내용 수정 >> 다시 add-commit
>> master는 원본 유지, testing만 변화 >> 이후 testing을 master로 가져와 병합할 것
```

### 병합(merge)

```python
git switch master #master 브랜치로 전환
git merge testing #testing 브랜치를 master와 병합

##만약, master/testing 브랜치 모두 수정사항 있다면 >> 취사선택해서 merge 해야 함
##이 경우, git merge 이후 >> 다시 commit 해야 merge 마무리됨

git log --online --graph #1줄로 간략히, 그래프 그려서 그간의 커밋 내역 출력
```

### 삭제

```python
git branch -d testing #병합 완료했으니 testing 브랜치 삭제
git log --oneline #testing 브랜치 삭제해도 log 기록은 남음
```

## 2.4 실습

### 2.4.1 git_hub 오픈소스에 접근하기

- 타인이 올린 오픈소스 그냥 코드 다운X >> 권한 없어서 다운 불가능
    - `forks` 통해 내 git_hub로 복제 >> 이후 클론 만들어야 함
- git_hub에서 타인이 작성한 오픈소스 들어가기
- 우측 상단 `forks` >> 타인 코드를 내 git_hub로 복제
- 내 git_hub로 옮긴 코드 복사 >> 클론 생성 가능해짐
- `git clone (code_url)`: git_hub 코드를 나의 로컬 디스크에 저장
    - git_hub에 있는 타인 코드 그냥 복사X >> 권한 없어서 불가능
    - git_hub `forks`: 타인의 오픈소스를 내 계정 git_hub로 복제 >> 내 계정에서 코드 복사해 클론 생성O

### 2.4.2 PR: 내 작업물을 타인의 저장소에 올리기

- **PR**: 내가 작업한 결과물을 상대가 관리하는 저장소에 올리는 것
- 내 repository 상단의 `pull requests` 탭 누름 >> new pull requests 통해 코드 넣은 게시물 게재
    - git_hub `pull requests`: 상대 master로 나의 master를 병합하는 것

---

# 3. 주피터 랩 설정

## 3.1 가상 환경 만들기

### **가상 환경**

- 폴더 목적별 필요 모듈 별도로 사용하도록 가상 환경 설정 → 폴더별 환경 달리 설정하는 것
    - 만약 주피터 랩부터 설치했다면 >> 이는 컴퓨터 전체에 설치하게 된 것 >> 다른 폴더에서도 쓸 수 있음
- 과정:
    - 가상 환경 활성화: `source (폴더_url)`
        - 비활성화: `deactivate` → 명령어만 입력해도O
    - 모듈 설치: `python -m (모듈명) (폴더명)`
    - 모듈 실행

```jsx
source venv/Scripts/activate # 가상 환경 활성화
python -m venv venv # venv 모듈을 venv 폴더에 설치
```

## 3.2 주피터 랩

- `pip`: 모듈 설치 명령어

```jsx
pip install jupyterlab # '주피터랩'이라는 도구 설치 명령어
jupyter lab # 주피터 랩 실행
```

- vs code 종료 시, 가상 환경 종료돼 주피터 랩도 꺼짐
    - 매일 가상 환경 활성화 + 주피터 랩 실행 코드 입력해야 함

```jsx
source venv/Scripts/activate
jupyter lab
```

## 3.3 자료 업로드

### git_ignore_list 만들기

- [gitignore.io]([gitignore.io](https://www.toptal.com/developers/gitignore/))
    
    git_hub에 `commit` 할 때, 무시하고 싶은 목록 만드는 사이트
    
- python, windows, macOS 검색해 나온 코드 복사 >> `.gitignore` 파일 만들어 붙여넣기
    - 그러면 일부 자료 비활성화 >> `commit` 할 때 제외됨

```python
git init
git add .
git commit -m "메시지"
#git_hub에서 원격 저장소 만들기 >> 저장소 링크 복사
git remote add origin https://github.com/alslsol/python
git push origin master
```