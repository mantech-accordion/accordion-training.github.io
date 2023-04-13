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
## 목적

해당 케이스는 다양한 네트워크 설계가 가능하며 네트워크 목적별로 구분하여 성능 향상을 기대할 수 있습니다.


---
## 아키텍처

![6_3_multiple_nic_arch](/assets/images/accordion/6_3_multiple_nic_arch.png)


---
## 인스톨 프로세스

![6_3_multiple_nic_install_process](/assets/images/accordion/6_3_multiple_nic_install_process.png)

- **group_vars/host.yml 파일 내용을 수정합니다. (멤버 클러스터인 경우 member.yml을 수정합니다.)
  + acc_interface 옵션에 Cluster Network로 사용할 NIC 이름을 적고, 클러스터를 설치합니다.**

![6_3_multiple_nic_install_option](/assets/images/accordion/6_3_multiple_nic_install_option.png)


---
## 주의 사항

- K8s 클러스터 SDN 네트워크로 사용할 대역 선정이 필요합니다. 즉, Cluster Network로 지정할 NIC으로 Calico의 설정이 필요합니다.
- 다수의 네트워크 인터페이스 카드가 존재하기 때문에, 노드에서 적절한 라우팅 테이블 설정이 선행되어야 합니다.