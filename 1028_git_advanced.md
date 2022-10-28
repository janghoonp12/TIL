# 10월 28일 git advanced

```
$ mkdir git-practice1/

$ git init
Initialized empty Git repository in C:/Users/multicampus/ssafy8/rjpark/git/.git/

$ touch test.md                                      // md 파일 생성

$ git add .
$ git commit -m '1st'
[master (root-commit) f4f8be2] 1st
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test.md

$ git log --oneline                                  // git 상태 출력
f4f8be2 (HEAD -> master) 1st

$ vi test.md                                         // 파일실행

i                                                    // i 눌러서 INSERT
esc                                                  // 텍스트 입력 후 esc 버튼
:wq                                                  // 저장 후 종료
:q                                                   // 저장하지 않고 종료

$ git rm --cached                                    // staging area 작업 되돌리기
$ git rm --

```



```
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   test.md


$ git rm --cached test.md                           // 아직 first commit이 없는 경우
rm 'test.md'


$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.md

nothing added to commit but untracked files present (use "git add" to track)
```

```
$ git add test.md

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   test.md

$ git restore --staged test.md

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   test.md

no changes added to commit (use "git add" and/or "git commit -a")

```

## commit 상태에서 되돌리기

- git commit --amend
  - staging area에 새로 올라온 내용이 없다면, 직전 커밋의 메시지만 수정
  - vim 실행됨.

```
$ git log --oneline
84b7ffa (HEAD -> master) wrong commit
f4f8be2 1st


$ git commit --amend
[master 19ec938] right commit
 Date: Fri Oct 28 09:33:02 2022 +0900
 1 file changed, 2 insertions(+)


$ git log --oneline
19ec938 (HEAD -> master) right commit
f4f8be2 1st

```

```
$ touch b.txt

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git (master)
$ git add .

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   b.txt


SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git (master)
$ git log --oneline
19ec938 (HEAD -> master) right commit
f4f8be2 1st

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git (master)
$ git commit --amend
[master 814b401] modified commit
 Date: Fri Oct 28 09:33:02 2022 +0900
 2 files changed, 2 insertions(+)
 create mode 100644 b.txt

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git (master)
$ git status
On branch master
nothing to commit, working tree clean

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git (master)
$ git log --oneline
814b401 (HEAD -> master) modified commit
f4f8be2 1st

```

## Git reset
- 특정 커밋 상태로 되돌림.
- 특정 커밋으로 되돌아 갔을 때, 해당 커미 이후로 쌓였던 커밋들은 전부 사라짐
- git reset [옵션]
  - --soft
    - 해당 커밋으로 되돌아가고
    - 이후의 파일들은 Staging Area로 돌려놓음
  - --mixed
    - 해당 커밋으로 돌아가고
    - 파일들을 Working Directory로 돌려놓음
  - --hard
    - 돌아가고
    - 돌아간 이후의 파일들은 모두 Working Directory에서 삭제
    - 기존의 Untracked 파일들은 남아있음


- soft

```
SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice
$ cd soft/

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/soft (master)
$ ls -a
./  ../  .git/  1.txt  2.txt  3.txt  untracked.txt

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/soft (master)
$ git log --oneline
20d320d (HEAD -> master) third
1eb059e second
6baf32f first

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/soft (master)
$ git reset --soft 6baf32f

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/soft (master)
$ git log --oneline
6baf32f (HEAD -> master) first

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/soft (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   2.txt
        new file:   3.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        untracked.txt

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/soft (master)
$ git reflog
6baf32f (HEAD -> master) HEAD@{0}: reset: moving to 6baf32f
20d320d HEAD@{1}: commit: third
1eb059e HEAD@{2}: commit: second
6baf32f (HEAD -> master) HEAD@{3}: commit (initial): first

```

- mixed

```
SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/soft (master)
$ cd ../mixed/

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/mixed (master)
$ ls -a
./  ../  .git/  1.txt  2.txt  3.txt  untracked.txt

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/mixed (master)
$ git log --oneline
20d320d (HEAD -> master) third
1eb059e second
6baf32f first

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/mixed (master)
$ git reset 6baf32f

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/mixed (master)
$ git log --oneline
6baf32f (HEAD -> master) first

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/mixed (master)
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        2.txt
        3.txt
        untracked.txt

nothing added to commit but untracked files present (use "git add" to track)

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/mixed (master)
$ git reflog
6baf32f (HEAD -> master) HEAD@{0}: reset: moving to 6baf32f
20d320d HEAD@{1}: commit: third
1eb059e HEAD@{2}: commit: second
6baf32f (HEAD -> master) HEAD@{3}: commit (initial): first

```

- hard

```
SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/mixed (master)
$ cd ../hard/

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/hard (master)
$ ls -a
./  ../  .git/  1.txt  2.txt  3.txt  untracked.txt

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/hard (master)
$ git log --oneline
20d320d (HEAD -> master) third
1eb059e second
6baf32f first

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/hard (master)
$ git reset --hard 6baf32f
HEAD is now at 6baf32f first

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/hard (master)
$ git log --oneline
6baf32f (HEAD -> master) first

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/hard (master)
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        untracked.txt

nothing added to commit but untracked files present (use "git add" to track)

SSAFY@DESKTOP MINGW64 ~/ssafy8/rjpark/git/git-reset-practice/hard (master)
$ git reflog
6baf32f (HEAD -> master) HEAD@{0}: reset: moving to 6baf32f
20d320d HEAD@{1}: commit: third
1eb059e HEAD@{2}: commit: second
6baf32f (HEAD -> master) HEAD@{3}: commit (initial): first


```

## Git revert