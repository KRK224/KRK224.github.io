---
title: '[Git] Git의 기초 (2) - 수정하고 저장소에 저장하기'
author: KRyun
date: 2021-02-13 11:10:00 +0900
categories: [Developing, Git]
tags: [2021년 2월, Git]
---

### __수정하고 저장소에 저장하기__

---

_Github와 Github blog를 제작하며 공부한 Git 내용을 정리하는 Posting 입니다._

`Reference:`  <https://git-scm.com/book/ko/v2>  

---

+ __파일의 라이프사이클__

지난 포스팅에서 현재 디렉토리에 Git 저장소를 만들고 master branch (default)를  워킹 디렉토리에 checkout 한 상태까지 진행했습니다. (*아직 branch와 checkout이 뭔지는 모르고 넘어가셔 됩니다.* 😊)

워킹 디렉토리(로컬 폴더에서 보이는 상태)의 모든 파일은 크게 __Tracked__(관리대상)와 __Untracked__(관리대상 아님)으로 나뉩니다. (벌써 여러 번 반복했지만 중요하니 한번 더 하겠습니다.)   

+ Tracked 파일은 이미 Git 저장소의 스냅샷에 포함(Commit 된 상태)되어있는 파일입니다.   

+ Commit 이후에 모든 Tracked 파일은 __Unmodified__ 상태에 있다가 수정이 된 순간 __Modified__ 상태로 변하게 됩니다.   

+ 추적 및 관리 대상이 아닌 __Untracked__ 파일은 `git add` 명령을 통해 __Staging Area__ 에 올리고 다음 Commit으로 Git 저장소에 저장할 수 있습니다.   

+ __Modified 상태의 Tracked 파일들__ 또한 `git add` 명령을 통해 __Staging Area__ 올린 후 Commit 해야합니다.   

![파일의 라이프 사이클](https://git-scm.com/book/en/v2/images/lifecycle.png)



#### __파일의 상태 확인하기.__

위에서 이야기한 것을 정리하면 파일은 크게 4가지 상태로 존재합니다.   
+ Untracked
+ Tracked
  - Modified
  - Unmodified
+ Staged

그리고 `git status` 명령은 현재 워킹 디렉토리의 파일 상태를 보여줍니다. Clone 및 Commit 한 후, 바로 이 명령을 실행하면,

```
$ git status

On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working directory clean
```

위의 내용은 마지막 스냅샷 이후에 수정된 파일이 하나도 없다는 것을 의미합니다. origin/mater는 default로 생성된 이름이라고 이해하시고 지금은 넘어가시면 됩니다.👉👉👉   

 프로젝트에 `README` 파일을 만들고, `git status` 명령을 실행하면,

```
$ echo 'My Project' > README
$ git status

On branch master
Your branch is up-to-date with 'origin/master'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)

    README

nothing added to commit but untracked files present (use "git add" to track)
```

Untracked files 목록에 `README` 파일이 추가된 것을 확인할 수 있습니다. 그 위에는 `git add <file>` 하면 Staging Area에 추가된다는 친절한 설명도 볼 수 있네요.   

#### __파일을 새로 추적하기__

이미 위에서 `git add` 명령으로 추적, 관리 상태로 변환 및 Staging Area에 올릴 수 있다고 했습니다. 명령을 입력하면,

```
$ git add README

$ git status

On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README
```
__Untracked files__ 목록에서 __Changes to be Committed__ 목록으로 바뀌는 것을 확인할 수 있습니다.

#### __Modified 상태의 파일을 Stage 저장하기__

다음은 `CONTRIBUTING.md`라는 파일이 이미 Commit된 Tracked 파일인데 수정했을 시의 `git status` 명령 결과 입니다.

```
$ git status

On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
```

Staging Area에 올라있는 README 파일과 다르게 __Changes not staged for commit__ 목록에 있습니다. 마찬가지로 `git add` 명령을 실행하면,

```
$ git add CONTRIBUTING.md
$ git status

On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README
    modified:   CONTRIBUTING.md
```

이제 두 파일 모두 Staged 상태에 있네요. 그런데 여기서 다시 CONTRIBUTING.md 파일을 수정하면 어떻게 될까요?

```
$ git status

On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README
    modified:   CONTRIBUTING.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
```

CONTRIBUTING.md 파일의 상태가 __Staged인 동시에 Unstaged (Modified)__ 임을 확인할 수 있습니다... 여기서 Commit을 하면 __마지막 수정 상태(Modified 상태, 워킹 디렉토리에서 실제로 보이는 상태)가 아닌(!!), Staging Area에 올린 상태__ 만이 Git 저장소에 저장됩니다.   

#### __파일 상태를 짤막하게 확인하기__

`git status -s` 또는 `git status --short`명령어는 `git status`명령으로 확인할 수 있는 내용을 간략하게 보여줍니다.

```
$ git status -s

 M README
MM Rakefile
A  lib/git.rb
M  lib/simplegit.rb
?? LICENSE.txt
```

| Staged      | Working Tree | Status                                                         |
|:-----------:|:------------:|:---------------------------------------------------------------|
|A            |              |Staged 상태에 새로 추가한 파일 (Untracked => __Staged__ )         |
|M            |              |기존의 Tracked 파일을 staged 상태로 올림 (Modified => __Staged__) |
|             |M             | __Modified__                                                   |
|M            |M             | __Staged__ 인 동시에 __Modified__                               |
|?            |?             | __Untracked__                                                  |




---

__이상으로 Posting 마치겠습니다.__
