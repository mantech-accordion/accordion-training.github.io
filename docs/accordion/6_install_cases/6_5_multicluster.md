---
layout: default
title: 2.6.5 Case 5 - 멀티클러스터
nav_order: 5
parent: 2.6 설치 케이스 모음
grand_parent: 2. Accordion v2
---

# Case 5
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## 멀티클러스터 구조

아코디언은 온프레미스, 혹은 다양한 클라우드 환경에 배포된 K8s를 한번에 관리하는 멀티클러스터 관리 기능을 제공합니다.

![6_5_multicluster_intro_1](/assets/images/accordion/6_5_multicluster_intro_1.png)

![6_5_multicluster_intro_2](/assets/images/accordion/6_5_multicluster_intro_2.png)


---
## 목적

아코디언 인스톨러를 이용하여 멀티클러스터를 동시에 설치 및 배포할 수 있습니다.

---
## 아키텍처

![6_5_multicluster_arch](/assets/images/accordion/6_5_multicluster_arch.png)


---
## 인스톨 프로세스

![6_5_multicluster_install_process](/assets/images/accordion/6_5_multicluster_install_process.png)

- **적절하게 accordion-installer/hosts를 작성합니다.**

![6_5_multicluster_install_hosts_1](/assets/images/accordion/6_5_multicluster_install_hosts_1.png)

![6_5_multicluster_install_hosts_2](/assets/images/accordion/6_5_multicluster_install_hosts_2.png)

- **적절하게 accordion-installer/group_vars를 작성합니다.**
  + host cluster 관련한 클러스터 설정은 group_vars/host.yml을 작성합니다.
  + member cluster 관련한 클러스터 설정은 group_vars/member.yml을 작성합니다.

![6_5_multicluster_install_groupvars](/assets/images/accordion/6_5_multicluster_install_groupvars.png)


---
## 주의 사항

- Host-cluster와 Member-cluster간 Agent 통신을 위해 클러스터간 방화벽을 오픈해야합니다.