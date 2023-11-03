---
layout: default
title: 1. 지라 워크매니지먼트
nav_order: 1
parent: appendix. Support
---

# 지라 워크매니지먼트
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


---
## 📍 이슈 티켓팅 워크플로우

![jira_workflow](/assets/images/support/jira_workflow.png){: width="1200" }

- ESCALATED CASE : 이슈 등록
- RESOLVED : 문제 해결 (버그나, 제품에 문제가 있을 때 패치가 돼서 해결한 경우)
- CLOSED CASE : 이슈 Close (가이드 전달, 기술 지원 등 파트너사가 맨텍에게 요청한 일을 해결했을 때)
- REOPEND : 이슈 재 오픈 (이슈를 다시 확인해야 할 때)
- IN PROGRESS : 이슈 처리중
- PENDING : 이슈 보류


---
## Jira Work Management에 계정 요청 방법

파트너 계정 등록은 파트너사에서 사용하는 대표 이메일 주소를 Jira WorkManagement 계정으로 등록합니다.
파트너사는 맨텍 엔지니어에게 파트너 공용 이메일 주소를 전달해주시면 됩니다.


---
## Jira Work Management 이슈 등록 방법

![jira_issue_enrollment](/assets/images/support/jira_issue_enrollment.png){: width="700" }

- 프로젝트(**필수**) : 파트너사 이름입니다.
- 이슈 유형(**필수**)
  +	작업: 고객사 지원 관련된 내용은 `지원` 선택
  + 버그: 제품에 버그가 발견된 경우 `버그` 선택
- 요약: 제목에 대한 요약을 작성
- 설명(**필수**): 이슈 내용을 상세하게 작성할 수록 빠른 원인 파악 및 이슈 처리가 가능합니다.
- 첨부 파일(**필수**): 아래 4가지 정보를 기본으로 첨부하면 빠른 원인 파악 및 이슈 처리가 가능합니다.
  + **장애 상황**
  + **이벤트 로그**
  + **Pod 에러 로그**
  + Pod가 기동된 노드의 messages 로그
  + **비정상 Pod 관련된 환경 설정**
- 아코디언 버전(**필수**) : 이슈 발생한 아코디언 버전을 작성합니다.
- 고객사(**필수**) : 이슈 발생한 고객사를 선택합니다.
- 보고자(**필수**) : 해당 이슈를 등록하는 파트너사 이름을 선택합니다.
- Start date : 시작한 날입니다. (생략 가능)
- 기한 : 정해진 기한을 설정해주시면 됩니다. (생략 가능)
- 범주 : 없음 (생략 가능)
- 우선 순위:
  + High: 서비스 장애가 발생하였고, 당장 해결이 필요한 경우 해당 상태로 등록합니다.
  + Medium: 서비스 장애는 발생하지 않지만, 아코디언의 장애가 발생한 경우 해당 상태로 등록합니다.
  + Low: 제품 버그나, 기타 이슈 등의 이슈는 해당 상태로 등록합니다.