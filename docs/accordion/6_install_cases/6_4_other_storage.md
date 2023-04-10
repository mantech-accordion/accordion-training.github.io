---
layout: default
title: 2.6.4 Case 4 - 기타 스토리지
nav_order: 4
parent: 2.6 설치 케이스 모음
grand_parent: 2. Accordion v2
---

# Case 4
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## NAS 이외의 별도 스토리지 사용

NFS와 같은 Network를 통한 공유 스토리지를 사용하는 케이스가 아닌, 기타 스토리지를 사용하는 구성입니다.

아래 예시는 Ceph 분산 스토리지를 사용하는 클러스터의 예시입니다.


---
**목적**


---
**아키텍처**

![acc-5.png](/assets/images/accordion/acc-5.png)


---
**인스톨 프로세스**

![acc-5.png](/assets/images/accordion/acc-5.png)


---
**주의 사항**

- 스토리지 연결 및 설정
- CSI를 지원하는 스토리지 여부

![acc-5.png](/assets/images/accordion/acc-5.png)