---
layout: default
title: 2.5.4 Case 4 - 일반 계정으로 설치 
nav_order: 4
parent: 2.5 설치 이슈 모음
grand_parent: 2. Accordion v2
---

# Case 4. 일반 계정으로 설치
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


---
## 문제 상황

Ansible 플레이북이 수행되지 못하고, Wait connection에서 타임아웃이 발생하는 경우

![5_4_trb_nonroot_user_log](/assets/images/accordion/5_4_trb_nonroot_user_log.png){: width="800" }

- 환경
  + User: mantech


---
## 원인 및 에러 분석 단계

- 아코디언 설치 시 root 권한이 필요합니다.
  + 일반 계정으로 설치하길 원하시는 경우 sudo 권한이 반드시 필요하고, `root` 계정으로 설치 시 `accordion-installer/hosts`를 알맞게 설정해주시면 됩니다.
  + 일반 계정으로 설치하려고하되, `accordion-installer/hosts` 파일을 `root`로 잘못 작성하는 경우 wait connection을 통과하지 못하고 타임아웃이 발생합니다.

- 엔서블 로그 확인

- accordion-installer/hosts 설정 확인

![5_4_trb_nonroot_user_hosts](/assets/images/accordion/5_4_trb_nonroot_user_hosts.png){: width="400" }

---
## 해결 방법

- 일반 계정에 sudo 권한이 부여되어 있는지 확인합니다.
- `accordion-installer/hosts` 파일 중 계정 설정 부분을 일반 계정으로 설정해줍니다.
