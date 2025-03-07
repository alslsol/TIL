# 1. git 기본 개념
cf. [gitbook](https://git-scm.com/book/ko/v2)

## 버전 관리

### 분산 버전 관리 시스템
- 클라이언트(나)와 서버(github) 모두가 똑같은 데이터를 유지해 버전을 관리하는 시스템
    - 동일 콘텐츠 여러 서버에 저장
    - 변화량 트래킹하기 쉬움
    - ex. git
### 로컬 버전 관리 시스템
- 서로 다른 버전을 모두 저장하는 방식
    - ex. 최종, 최종1, 최종2... >> 각각 저장

### 중앙집중식 버전 관리 시스템
- ex. 노션: 노션의 클라우드에만 저장, 로컬 디스크엔 저장X

## git의 3가지 영역

![git형태](https://git-scm.com/book/ko/v2/images/areas.png)

 - **working directory**: 현재 작성 중인 코드/파일
- **staging directory**: add 명령어로 무대 위로 올라간 파일들
- **git directory**(repository): `commit`으로 찍힌 스냅샷을 저장하는 공간

## CLI
- **GUI**: 일반적인 그래픽 인터페이스 >> ex. windows
- **CLI**: 명령어 코드를 이용한 인터페이스 >> ex. git

## git 최초 설정

- 사용자 정보

```python
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```
- `--global`: git으로 사진 찍을 때, 어디서든 사진 찍든 그 사진 찍은 이의 이름을 하나로 정하는 고정값 설정한 것

- `git help`: git이 쓸 수 있는 명령어 모두 보여줌

## git 저장소 만들기
### 1. 새 폴더를 git 저장소로 만들기
- `git init`: 현재 디렉토리에 `.git` 폴더 생성해 >> 새 git 저장소를 초기화
    - 최초 한번만 하면 됨

### 2. 이미 작업 중인 폴더를 git 저장소로 만들기
- git hub의 `code`에서 프로젝트 링크 복사
- `git clone (링크)`: 해당 링크의 프로젝트를 복사해서 git 저장소 클론을 만드는 방법
    - 근데 저장하려는 장소에 동일명 파일 있으면 저장X >> 폴더명 다른 이름으로 설정해 저장

## 수정/저장 사이클
### 과정
- untracked 상태에서 `add` 하면, staged로 올라감
- `commit`하면 unmodified 상태로 넘어가며 트래킹 시작됨
- 여기서 수정 시 modified 상태로 전환됨
- 이때 다시 `commit`하면 unmodified로 회귀
### 용어
- **tracked** 파일: 관리대상 >> 이미 스냅샷에 포함된 파일
    - **modified**: 수정된 상태
    - **unmodified**: 수정X는 동일 상태
- **untracked** 파일: 관리대상X >> 워킹 디렉토리의 파일 중 스냅샷 or staging area에도 오르지 않은 파일

### git 상태 확인
- `git status`: 현재 git의 상태를 확인 >> tracked, untracked 파일 구분해 표시

- `.git` 폴더는 자신의 현 위치를 기준으로만 작동 >> TIL 폴더까지만 관리함, DAMF2 폴더는 관리X
    - 새 `.git` 폴더 독립적으로 관리 가능하도록, 상위 폴더에는 또다른 `.git` 폴더 만들면 오류 발생
    - 새로 만들려면: DAMF2 내 TIL 이외 별도 폴더 만든 뒤, 그 하위에 `.git` 폴더 만들면 됨

## remote 저장소
- 인터넷/네트워크 속에 있는 원격 저장소 
    - 타인과 협업하기 위해 데이터 push/pull 하기 위한 공간
- **생성**: `git remote add (별명) (링크)`
- **삭제**: `git remote remove (별명/링크)`

### 예제) 웹페이지 만들기
- 템플릿 다운 >> TIL 폴더 내 새폴더 만들어 템플릿 저장
- 내 맘대로 웹페이지 코드 수정 >> <open in browser> 통해 수정본 확인하며 작업

```python
#수정한 웹페이지 발행하기

git add . #github-page 폴더에서 현재 폴더 기준 모든 데이터를 staging area로 올림
git commit -m "page" #'page' 메시지 달아서, 스냅샷 찍음
git remote add origin https://github.com/alslsol/alslsol.github.io/settings #원격 저장소에 저장
git push origin master #원격 저장소에 올린 내용 웹페이지로 발행
```

### 예제) remote 저장소를 활용한 협업
```python
#데이터 저장하기

##github에서 new repository 만듦
git init
git add . #staging area에 올리기
git commit -m "끝말잇기 시작" #스냅샷 찍기
git remote add origin https://github.com/alslsol/end-to-end #저장소에 저장
git push origin master #저장소에 발행
```

```python
#다른 컴퓨터/동료: 클론 만들어 저장하기

##DAMF2 폴더에서 우클릭해 VScode 열기
git clone https://github.com/alslsol/end-to-end-2.git #github에서 코드 복사 >> end-to-end-2라는 다른 이름으로 저장
```

```python
##수정/저장
git add .
git commit -m "update"
git push origin master #수정된 내용 github 업로드
```

```python
#저장소에서 자료 불러오기
git pull origin master #github에 저장된 내용 불러옴
```

- 동기화된 내용 가져오기 전에 내 파일 수정하면X >> pull한 다음 수정해야 함
- 만약 이미 수정본 commit해서 가져오려는 파일과 충돌했다면?
    - 에러 메시지 남 + hint로 git pull 하라고 제안 뜸
    - 이후 git pull 하면 >> 4가지 선택지 뜸 >> 적절히 선택지 클릭
    - 이후 커밋해야 완전히 합쳐지기 완료
        - ex. `git commit -m "merging"`

# 2. git 명령어 정리
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
       - `--oneline`: 각 커밋을 한 라인으로 보여줌 >> 많은 커밋을 한 번에 조회 시 유용
       - `--graph`: 각 커밋에 선 달아서 보여줌
- `git remote`
    - 원격 저장소 관리 명령어 >> 데이터 저장할 원격 저장소 지정
    - options:
        - `git remote -v`: 실제 저장된 링크주소 알려줌 >> 근데 링크 매번 언급하기 어려우니, origin이라는 별명으로 대체한 것
       - `git remote add (별명) (링크)`: 원격 저장소 새로 지정 + 링크 대신할 별명 설정
            - 최초 한번만 지정하면 됨 >> `master` 있으면 이미 지정돼 있으니, `git push`만 해도 됨
        - `git remote remove (별명/링크)`: 원격 저장소 지정 삭제
- `git push (별명) master`: 원격 저장소에 저장하기
- `git pull (별명) master`: 원격 저장소에서 데이터 불러오기