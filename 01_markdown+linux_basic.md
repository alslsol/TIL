# 1. 마크다운 기본 문법
## 제목

1-4개의 # 기호를 사용해 제목 수준을 지정

## 텍스트 스타일
- 굵기: **단어**
- 기울기: *단어*
- 취소선: ~~단어~~
- 굵기+기울기: ***단어***

## 텍스트 인용
>인용구문

## 코드 인용(핵심)
- in-line에서 코드 인용: 이것은 `code` 입니다.
- 코드 자체 인용할 때: 백틱(`) 활용

- 코드 블럭: 백틱(`) 3개로 열고 닫기
    -첫 백틱 옆에 프로그램명 적으면, 각 코드 색으로 변경

```python
def hello():
    print("hello!")
```

## 링크
- [링크명](링크주소_url)
    - 대괄호: 대체 텍스트 입력하는 공간
    - 소괄호: 링크 주소 입력하는 공간

[구글](http://google.com)

## 이미지
- 인터넷에 올라와 있는 사진을 업로드할 때: ![사진에 대한 설명](실제 보여주고 싶은 사진의 경로)

![강아지](https://image.dongascience.com/Photo/2020/03/5bddba7b6574b95d37b6079c199d7101.jpg)

- 내 디바이스에 있는 사진 업로드할 때: ![고양이](주소: 이 파일을 기준으로 하나씩 타고 올라가는 식으로 주소 찾아야 함)

![고양이](../cat.jpg)

- `..`: 현 파일의 상위 폴더 탐색 >> 상대 경로로 주소 찾는 방식
- 상대 경로: 내가 있는 파일을 기준으로 상대적으로 위치 탐색
    - ex. 올리브영 기준 오른쪽에 있는 게 버티고 타워야
- 절대 경로: 충청남도 천안시 서북구... >> 전체 주소를 말한 것

## 목록
### 순서가 있는 목록
1. 첫 번째
2. 두 번째
3. 세 번째

### 순서가 없는 목록
- 첫 번째
    - 1-1 입니다
    - 1-2 입니다
- 두 번째
- 세 번째

## 참고자료
[마크다운 문법](https://docs.github.com/ko/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

- 위 내용은 노션, 옵시디언 등에서 모두 해당, 이외 문법은 각 플랫폼에 따라 다름

# 2. 리눅스 기본 명령어

## 리눅스 명령어의 기본 형식

```python
command [options] [arguments]
```
- **command**: 실행할 명령어 or 프로그램 -> ex. python, git...
    - 띄어쓰기 붙이면 하나의 명령어로 인식하므로, 띄어쓰기 중요 >> ex. `python-v` (x)
- **options**: 명령어의 옵션 >> 보통 options엔 마이너스 붙음
- **arguments**: 명령어에 전달할 인자 >> 실제 활용하는 데이터

ex. `python`: command, `-V`: options

## 1) 파일/디렉토리 관리
### 목록 확인
- `ls`(list)
    - 디렉토리 내용 목록 보여줌 >> 현재 내 위치에 있는 모든 파일/폴더 보여주는 것
- options:
    -  `ls -l`: 파일의 상세 정보 표시
    -  `ls -a`: 숨김 파일 표시
        - `.`으로 시작하는 이름의 파일/폴더는 모두 숨김 표시됨 >> ex. `.git` 폴더

### 폴더 이동
- `cd (이동하려는 위치)`(change delectory, 폴더 변경)
    - 현재 작업하는 디렉토리 변경
    - ex. `cd ..`: 현 폴더의 상위 폴더로 이동
        - `.`: 현재 폴더
        - `..`: 상위 폴더
    - ex. `cd TIL`: TIL 폴더로 이동

#### 주의
- 폴더 너무 많으면 `cd`로 선택하기 어려움
    - Tab: 현 위치 기준, 해당 알파벳으로 시작하는 폴더를 자동완성 입력해줌
    - 근데 같은 알파벳의 폴더가 여러개 있다면?
    - Tab 2번: 어느 폴더로 갈 지 선택하게 해줌

ex. `cd ../../..`: 현재 내 위치에서 3개 상위 폴더로 가겠단 것

### `pwd`(print working directory)
- 현재 작업 중인 디렉토리의 전체 경로 출력

### `mkdir (폴더명)`(make directory): 새 폴더 생성
- ex. `mkdir (markup)`: markup 폴더 생성

### touch (파일명): 파일 생성
- ex. `touch a.txt`: a라는 이름의 텍스트 파일 생성해줌

### `rm`(remove): 파일 삭제
- 파일만 삭제 가능, 폴더는 불가능 >> `-r` 옵션 통해 폴더 삭제 가능
    - 폴더는 내부에 또다른 파일/폴더 있을 수O >> rm만으로는 지우지X
- options:
    - `rm -r (폴더명)`: 폴더 삭제
        - `-r`: 디렉토리와 그 내용을 재귀적으로 삭제
    재귀적: like 액자식 구성 >> 폴더 안에 또다른 폴더 있듯, 재귀 옵션 넣어야 폴더 삭제 가능
ex. rm -r markup: markup 폴더 삭제해줌

### `cat (파일명)`: 파일 내용 출력
ex. `cat README.md`: README.md 파일의 내용을 출력해줌

## 2) github 업로드: `add`-`commit`/`push`-`pull` 반복

- `git init`: TIL 폴더 내에 `.git`이라는 숨김 폴더 생성
    - `.git` 있어야, 하위 데이터 묶어서 github에 업로드 가능
- `git add .`
    - 현 위치 기준, 하위 모든 데이터를 포함해서 staging area로 올림
- `git commit -m "메시지"`: 스냅샷 찍음 + 메시지 입력
    - 누가 작성한 건지 출처 적어줘야 함 >> github 가입한 이메일 입력해야 함
- git remote add origin (링크)
- git push origin master
- git pull origin master

### 수정 시, `add`, `commit`으로 변화량 측정 >> `push`, `pull` 통해 저장/동기화

## 참고자료
[git book](https://git-scm.com/book/ko/v2)
