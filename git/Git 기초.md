# Git 기초

> Git은 분산형 버전관리시스템(DVCS)이다.

Git을 윈도우에서 활용하기 위해서는 [git bash](https://gitforwindows.org/)를 설치해야 한다.

## 1. 저장소 초기화

```bash
$ git init
Initialized empty Git repository in C:/Users/i/Desktop/TIL/.git/

(master) $
```

* 로컬 저장소를 만들고 나면, `.git/` 폴더가 생성되고, bash에 `(master)` 라고 표기 된다.
* 반드시 저장소를 만들기 전에 원하는 디렉토리인지 확인하는 습관을 가지고, 저장소 내부에 저장소를 만들지는 말자.
  * 예) Desktop -> git 저장소, TIL -> 다른 git 저장소 (X) 

## 2. `add`

작업한 내용을 커밋 대상 목록에 추가한다.

```bash
$ git add .             # 현재 디렉토리(하위 디렉토리 포함)
$ git add a.html		# 특정 파일
$ git add b.html c.html # 특정 다수 파일
$ git add blog/			# 특정 폴더
```

```bash
# 작업 후 상태
$ git status
On branch master

No commits yet
# Untracked files => Git으로 관리된 적 없는 파일
Untracked files:
# 커밋 될 것들에 포함시키기 위해서는 add 명령어를 써라
  (use "git add <file>..." to include in what will be committed)
        markdown-images/
        markdown.md
# 총평 
# 커밋될 곳에 없다(nothing)
# 하지만, 새로 생성한 파일(untracked files)은 존재한다.
nothing added to commit but untracked files present (use "git add" to track)

```

```bash
$ git add .
```

```bash
# add 명령어 후 상태
$ git status
On branch master

No commits yet
# 커밋이 될 변경 사항들
# Working directory X
# Staging area O
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   "markdown-images/\354\272\241\354\262\230.PNG"
        new file:   markdown.md

```

## 3. `commit`

```bash
$ git commit -m 'Add markdown.md'
[master (root-commit) 2472e6f] Add markdown.md
 2 files changed, 87 insertions(+)
 create mode 100644 "markdown-images/\354\272\241\354\262\230.PNG"
 create mode 100644 markdown.md
```

* 커밋은 버전(이력)을 기록하는 명령어이다.

* 커밋 메시지는 해당하는 이력을 나타낼 수 있도록 작성 하여야 한다.

* 커밋 이력을 확인하기 위해서는 아래의 명령어를 사용한다.

  ```bash
  $ git log
  commit 2472e6f7d10202d2b67724ca515a9ffa68d275fc (HEAD -> master)
  Author: edutak <edutak.ssafy@gmail.com>
  Date:   Thu Aug 20 14:58:03 2020 +0900
  
      Add markdown.md
  $ git log -1
  $ git log --oneline
  2472e6f (HEAD -> master) Add markdown.md
  $ git log --oneline -1
  ```

  ```bash
  $ git status
  On branch master
  # WD X
  # Staging area X
  nothing to commit, working tree clean
  ```

  

## 4. 기타 명령어

### 1) `restore`

작업공간(working directory)의 변경 사항을 버린다.

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  # 힌트!
  (use "git restore <file>..." to discard changes in working directory)
        modified:   CLI.txt

no changes added to commit (use "git add" and/or "git commit")
$ git restore CLI.txt
```

* `--staged` 옵션을 활용하면, staging area를 취소(`add` 명령어의 반대)

  ```bash
  $ git status
  On branch master
  Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
          modified:   CLI.txt
  ```

  ```bash
  $ git restore --staged CLI.txt
  $ git status
  On branch master
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
          modified:   CLI.txt
  
  no changes added to commit (use "git add" and/or "git commit -a")
  ```

### 2) 커밋 메시지 변경

```bash
$ git commit --amend
```

* vim 편집기가 실행된다.

* `i` : 편집 모드로 변경되어서 메시지 변경 가능

* `esc` + `:wq` : 저장하고 종료

* **주의!!** 공개된 커밋은 절대 변경 금지.

  ```bash
  $ git log --oneline
  00a6259 (HEAD -> master) TEest
  f7dc503 First commit
  
  $ git commit --amend
  [master 4d42f0f] Test
   Date: Fri Aug 21 16:17:42 2020 +0900
   1 file changed, 1 insertion(+)
  
  $ git log --oneline
  4d42f0f (HEAD -> master) Test
  f7dc503 First commit
  ```

  * 커밋시 특정 파일을 빠트린 경우 아래와 같이 활용할 수 있다.

    ```bash
    $ git add omit.html
    $ git commit --amend
    ```

### 3) reset vs revert

1. `revert` : 되돌렸다는 커밋이 발생된다.

   ```bash
   $ git revert 특정시점
   $ git log --oneline
   520c668 (HEAD -> master) Revert "Add 3 files"
   8a97ad4 Add 3 files
   4d42f0f Test
   f7dc503 First commit
   ```

2. `reset` : 커밋 자체를 지운다. (원격저장소에 공개된 이력의 경우 주의!)

   ```bash
   $ git reset 특정시점
   $ git log --oneline
   4d42f0f (HEAD -> master) Test
   f7dc503 First commit
   ```

   * `--mixed` : 기본 설정
     * 해당 커밋 이후 변경사항을 staging area 내용 보관
   * `--hard`
     * 해당 커밋 이후 변경사항을 모두 삭제
   * `--soft` 
     * 해당 커밋 이후 변경사항 및 working directory 내용 보관











