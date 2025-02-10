# 리눅스 기본 명령어

## 0. 리눅스 명령어의 기본 형식

```
command [options] [arguments]
```

command: 실행할 명령어 or 프로그램 -> ex. python, git...
    띄어쓰기 붙이면 하나의 명령어로 인식하므로, 띄어쓰기 중요
    ex. `python-v` (x)

options: 명령어의 옵션 -> 보통 options엔 마이너스 붙음

arguments: 명령어에 전달할 인자 -> 실제 활용하는 데이터

ex. `python`: command, `-V`: options

## 1. 파일 및 디렉토리(폴더) 관리
### ls(list): 디렉토리 내용 목록 보여줌 >> 현재 내 위치에 있는 모든 파일/폴더 보여주는 것
- options:
   -  `-l`: 파일의 상세 정보 표시
   -  `-a`: 숨김 파일 표시

.: 현재 폴더 의미
..: 상위 폴더 의미

.으로 시작한 파일/폴더는 모두 숨김 표시됨 >> -a 옵션 붙여야 전부 보여줌

ls 했을 때,
    파랑: 폴더, 하양: 파일

### cd(change delectory, 폴더 변경): 현재 작업 디렉토리를 변경함
```
cd 이동하려는위치
```
`cd ..`: til 폴더에서, ..을 하면 그 상위 폴더인 DAMF2 폴더로 이동

`cd TIL`: DAMF2 폴더에서 하위 폴더인 TIL 폴더로 이동하겠다는 것 -> 마우스로 클릭하는 걸 키보드 코딩으로 하는 것

- 폴더 엄청 많으면 cd로 선택하기 어려움
그래서 탭 누르면 현재 내 위치 중에서 해당 알파벳으로 시작하는 폴더를 자동완성 입력해주는 기능 있음

- 근데 같은 알파벳의 폴더가 여러개 있다면?
탭 두번 누르면 마크 업 or 다운 중 어느 폴더로 갈 건지 선택하게 해줌

`cd ../../..`: 현재 내 위치에서 3개 상위 폴더로 가겠단 것


`cd (target-directory)`
target-directory: 탭을 통한 자동완성 기능 활용해 찾기

### pwd(print working directory): 현재 작업 중인 디렉토리의 전체 경로 출력
```
`pwd`
```
### mkdir(make directory): 새 디렉토리를 생성하는 명령어
```
`mkdir (폴더명)`
```
ex. `mkdir (markup)`: markup 폴더 새로 만들어줌
    () 안에는 새로 만드려는 폴더명 입력

### touch: 파일 생성
```
touch (파일명)
```
ex. `touch a.txt`: a라는 이름의 텍스트 파일 생성해줌

### rm(remove): 파일 및 폴더 삭제
- rm: 파일 지우기 가능, 폴더는 불가능
    폴더: 그 안에 또다른 파일/폴더 있을 수 있기에 rm만으로는 못하는 것
    
- 폴더 지울 때는 options으로 `-r` 입력해야 함

`-r`: 디렉토리와 그 내용을 재귀적으로 삭제
    재귀적: like 액자식 구성 >> 폴더 안에 또다른 폴더 있듯, 재귀 옵션 넣어야 폴더 삭제 가능

ex. rm -r markup: markup 폴더 삭제해줌

### cat: 파일의 내용 출력
ex. `cat README.md`: README.md 파일의 내용을 출력해줌


## git init: TIL 폴더 내에 .git이라는 숨김 폴더 생김

이걸 만듦으로써 zip 파일로 묶어서 git hub에 올리려는 것

cf. [git book](https://git-scm.com/book/ko/v2)

git: 파일 내 변화량을 트래킹하기 편한 툴임