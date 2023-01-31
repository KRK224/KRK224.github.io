---
title: '[Git] Git 시작하기 (1) - 버전 관리란?'
author: KRyun
date: 2021-01-07 22:00:00 +0900
categories: [Developing, Git]
tags: [2021년 1월, Git]
---

_Github와 Github blog를 제작하며 공부한 Git 내용을 정리할 예정입니다. 주 reference site는_ `https://git-scm.com/book/ko/v2`_입니다._  

---

### Git 시작하기 - 버전 관리란?
버전 관리 시스템(VCS - Version Control System)은 파일 변화를 시간에 따라 기록했다가 나중에 특정 시점의 버전을 다시 꺼내올 수 있는 시스템.



#### __로컬 버전 관리__
일반적으로 많은 사람들의 버전 관리란, 동일한 파일을 여러 디렉토리에 저장하는 방법이다. 하지만 디렉토리 관리와 수정사항에 대한 관리가 어렵다. <br>
이런 이유로, __간단한 데이터베이스를 사용해서 만든 로컬 VCS__ 로 파일의 변경 정보를 관리하기 시작했다. <br>

<p aligh = "center"><img src ="https://git-scm.com/book/en/v2/images/local.png"></p>

_Figure 1.로컬 버전 관리._<br>
많이 쓰는 VCS 도구 중에 RCS(Revision Control System)는 오늘날까지도 아직 많은 회사가 사용하고 있다. RCS는 기본적으로 Patch Set(파일에서 변경되는 부분)을 관리한다. 그리고 Patch Set을 적용해서 모든 파일을 특정 시점으로 되돌릴 수 있다.

#### __중앙집중식 버전 관리 (CVCS)__
CVCS(중앙집중식 VCS)는 로컬 버전 관리에서 할 수 없는 파일의 공동 작업을 가능하게 한다. CVS, Subversion, Perforce 같은 시스템은 __파일을 관리하는 서버가 별도로 있고, 클라이언트가 중앙 서버에서 파일을 받아서__ 사용(Checkout)한다. <br>

<p aligh = "center"><img src ="https://git-scm.com/book/en/v2/images/centralized.png"></p>

_Figure 2.중앙집중식 버전 관리(CVCS)._<br>
그러나 이 CVCS 환경은 몇 가지 치명적인 결점이 있다. 가장 대표적인 것이 중앙 서버에 발생한 문제다.  __중앙 데이터베이스가 있는 하드디스크에 문제가 생기면 프로젝트의 모든 히스토리를 잃는다.__ 물론 사람마다 하나씩 가진 스냅샷은 보존이 된다.

#### __분산 버전 관리 시스템__ <br>
 CVCS(중앙집중식 버전 관리)은 개인 사용자가 스냅샷 (파일 버전의 한 순간)을 저장하는 반면, DVCS(분산 버전 관리 시스템)는 __서버의 저장소를 히스토리와 더불어 전부 복제(Clone)__ 한다. <br>

 <p aligh = "center"><img src ="https://git-scm.com/book/en/v2/images/distributed.png"></p>

 _Figure 3. 분산 버전 관리 시스템(DVCS)._

따라서, 서버에 문제가 생기면 이 복제물로 다시 작업하고, 서버를 복원할 수 있는 진정한 백업 기능을 제공한다.
