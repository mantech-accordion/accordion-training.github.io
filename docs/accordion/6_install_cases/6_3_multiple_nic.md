---
layout: default
title: 2.6.3 Case 3 - Multiple NIC
nav_order: 3
parent: 2.6 설치 케이스 모음
grand_parent: 2. Accordion v2
---

# Case 3
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## Multiple NIC 환경

해당 케이스는 네트워크 라인별 목적을 두고 다수의 네트워크 인터페이스 카드(NIC)를 노드에 할당하는 Multiple NIC 구성입니다.
- Cluster Network: K8s 클러스터내 SDN 환경에서 API를 주고 받을 네트워크
- Service Network: K8s 클러스터 외부에서 발생하는 트래픽을 처리할 네트워크
- Storage Network: K8s 클러스터에서 사용할 볼륨, 혹은 노드에서 사용할 스토리지를 연결하기 위한 네트워크


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

- Calico 설정

![acc-5.png](/assets/images/accordion/acc-5.png)