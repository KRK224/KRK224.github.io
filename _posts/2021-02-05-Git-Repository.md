---
title: '[Git] Git의 기초 (1) - Git 저장소 만들기'
author: KRyun
date: 2021-02-05 22:10:00 +0900
categories: [Developing, Git]
tags: [2021년 2월, Git]
---

### __Git 저장소 만들기__

---

_Github와 Github blog를 제작하며 공부한 Git 내용을 정리하는 Posting 입니다._

`Reference:`  <https://git-scm.com/book/ko/v2>  

---
  + __Git 저장소를 만들기 위해서는 다음과 같은 2가지 방법이 있습니다.__   

> 1. 일반 폴더(버전 관리를 하지 않는 로컬 디렉토리)를 선택하여 Git 저장소를 적용하는 방법.   
> 2. 다른 Git 저장소를 __Clone__ 하는 방법.



#### __1. 기존 폴더에 Git 적용하기__   
버전 관리를 하고 싶은 폴더로 이동합니다.

```
$ cd C:\Users\username\my_project
```
그리고 다음과 같이 입력하면,
```
$ git init
```

현재 폴더에 `.git`이라는 하위 디렉토리가 생성됩니다. (*혹시 안 보이시는 분들은, 숨긴 항목 보기 설정을 해주시면 됩니다.*)   
이 `.git` 디렉토리에는 저장소에 필요한 뼈대 파일(Skeleton)이 들어있다고 합니다... 자세한 사항은 [Git의 내부](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EB%82%B4%EB%B6%80-Plumbing-%EB%AA%85%EB%A0%B9%EA%B3%BC-Porcelain-%EB%AA%85%EB%A0%B9#ch10-git-internals)에서 확인하시면 됩니다. ~~*권장드리진 않아요.*~~   

아직까지는 프로젝트(현재 디렉토리)의 어떤 파일도 관리하지 않습니다. Git이 파일을 관리하게 하려면 `추적(tracking)` 상태로 올려야한다는거 기억하시나요? ([Git 기초](https://krk224.github.io/posts/what-is-Git-(2)/) 에서 한번 언급했는데 이 posts 읽고 다시 읽어보시면 좋아요.😊)   

이제 파일들을 `추적`,`관리`,`staging area에 추가` 해보겠습니다.

```
$ git add *.txt
$ git add .
```

`git add` 명령어를 입력하면 Untracked 파일들을 __Staging Area__ 에 추가할 수 있습니다. 그리고 `git add . ` 명령은 모든 Untracked 파일들을 추가할 수 있어요.

이제 추적 상태의 파일들을 `.git` 저장소에 올리려면 `git commit`이란 명령을 사용합니다.

```
$ git commit -m "my first commit"
```

여기서 `-m "commit message"`는 commit 내용에 대한 설명을 저장할 수 있습니다 (협업 시에 수정 내용을 저장해야 동료들이 이해하겠죠). 이 명령을 생략하면 자동으로 등록된 편집기(저는 `Notepad++`였죠)가 실행되어 메세지를 입력할 수 있습니다.   

#### __2. 기존 저장소 Clone 하기__

[Git 시작하기(1)](https://krk224.github.io/posts/what-is-Git/) posts에서 Git은 분산 버전 관리 시스템이라고 언급을 했습니다. 그리고 __서버의 저장소를 히스토리와 더불어 전부 복제(Clone)__ 한다고 했습니다.   

물론 서버가 아닌 로컬의 다른 Git 저장소도 가능하지만, 협업을 위해서 서버 또는 Github에서 저장소를 복제하는 경우가 많습니다.

```
$ git clone https://github.com/username/repository
```

`git clone` 명령을 통해 Github의 저장소를 복제해왔습니다. 이렇게 통째로 저장소를 복제하는 경우, 그 저장소의 __버전 히스토리 및 저장된 파일들을__ 모두 불러와 바로 작업을 시작할 수 있습니다.

<span style="color=red; font-weight=bold"> Tip. </span>   

  + 위의 명령어를 실행하면 현재 폴더 아래에 `repository` 폴더가 생성됩니다. 만약 다른 폴더 이름을 사용하고 싶으면 아래와 같이 사용하시면 됩니다.

```
$ git clone https://github.com/username/repository "my-project2"
```

+ Github에서 repository url 찾기   
![github_repository](/assets/img/post/202102/20210205_Git_repository_1.png)

---

__이상으로 Posting 마치겠습니다.__
