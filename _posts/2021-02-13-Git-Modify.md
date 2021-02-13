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

지난 포스팅에서 현재 디렉토리에 Git 저장소를 만들고 master branch (default)를  워킹 디렉토리에 checkout 한 상태까지 진행했습니다. (*아직 branch가 무엇인지 설명드리지 않았으니 넘어가시면 됩니다.*)

그리고 워킹 디렉토리(로컬 폴더에서 보이는 상태)의 모든 파일은 크게 __Tracked__(관리대상)와 __Untracked__(관리대상 아님)으로 나뉩니다. (벌써 여러 번 반복했지만 중요하니 한번 더 하겠습니다.)   

Tracked 파일은 이미 Git 저장소의 스냅샷에 포함(Commit 된 상태)되어있는 파일입니다.   

Commit 이후에 모든 Tracked 파일은 __Unmodified__ 상태에 있다가 수정이 된 순간 __Modified__ 상태로 변하게 됩니다.   

추적 및 관리 대상이 아닌 __Untracked__ 파일은 `git add` 명령을 통해 __Staging Area__ 에 올리고 다음 Commit으로 Git 저장소에 저장할 수 있습니다.   

참고로, Modified 상태의 Tracked 파일들 또한 `git add` 명령을 통해 __Staging Area__ 올린 후 Commit 해야합니다.

![파일의 라이프 사이클](https://git-scm.com/book/en/v2/images/lifecycle.png)
__파일의 라이프 사이클__


#### 파일의 상태 확인하기.

위에서 이야기한 것을 정리하면 파일은 크게 4가지 상태로 존재합니다.   
+ Untracked
+ Tracked
  - Modified
  - Unmodified
+ Staged

그리고 `git status` 명령은 현재 워킹 디렉토리의 파일 상태를 보여줍니다. Clone 및 Commit 한 후에 바로 이 명령을 실행하면,

```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working directory clean
```

위의 내용은 마지막 스냅샷 이후에 수정된 파일이 하나도 없다는 것을 의미합니다. origin/mater는 default로 생성된 값으로 이해하고 지금은 넘어가시면 됩니다.

이제 프로젝트에 `README` 파일을 만들고, `git status` 명령을 실행하면,

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

Untracked files 목록에 `README` 파일이 추가된 것을 확인할 수 있습니다. 그 위에는 친절하게 `git add <file>` 하면 Staging Area에 추가된다는 설명도 볼 수 있네요.
