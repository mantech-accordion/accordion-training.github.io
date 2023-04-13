---
layout: default
title: 2.6.2 Case 2 - 내부망+외부망
nav_order: 2
parent: 2.6 설치 케이스 모음
grand_parent: 2. Accordion v2
---

# Case 2
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## 내부망 클러스터 + 외부망 Worker 노드

해당 케이스는 내부망에 아코디언 클러스터가 존재하고, 외부망에 Worker 노드를 별도 배치하는 구성입니다.

(예시)
- 내부망) 마스터 3대 + 인프라 2대 + 워커 3대
- 외부망) 워커 3대


---
## 목적

해당 케이스는 내부망에는 내부망 서비스용 Pod를 배치하고 외부망 노드에는 외부 서비스용 Pod를 배치하여 운영이 가능합니다.
또한, 필요 시 외부망 노드에 Ingress Controller를 배치하여 내부망 서비스에도 Ingress Controller를 통해 외부 트래픽 유입이 가능한 구조입니다.


---
## 아키텍처

![6_2_ext_node_arch](/assets/images/accordion/6_2_ext_node_arch.png)


---
## 인스톨 프로세스

- **1~8. 아코디언 인스톨러를 알맞게 설정하고 설치합니다.**
- **9. 아코디언 클러스터에 외부망 노드를 추가합니다.**

![6_2_ext_node_addnode_process](/assets/images/accordion/6_2_ext_node_addnode_process.png)


---
## 주의 사항

- 내부망/외부망에 적절하게 Pod가 배치될 수 있도록 적절한 Affinity 설정이 필요합니다.
- Nginx Ingress Controller의 구분이 필요합니다.
- 외부망 워커 노드에도 스토리지를 연결해야할 경우, 내부망 스토리지를 연결할 수 없다면 별도의 스토리지클래스 및 NFS 프로비저너 설정이 필요합니다.
- 외부망 워커 노드와 내부망 노드간 NIC 이름이 다를 경우, Calico IP_AUTODETECTION_METHOD를 CIDR로 변경하거나, Interface를 추가해주어야 합니다.