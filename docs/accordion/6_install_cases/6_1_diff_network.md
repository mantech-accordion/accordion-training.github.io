---
layout: default
title: 2.6.1 Case 1 - 노드 간 망이 다를 경우
nav_order: 1
parent: 2.6 설치 케이스 모음
grand_parent: 2. Accordion v2
---

# Case 1
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## 노드 간 망이 다른 환경

내부 정책 혹은 기타 이유로 클러스터를 구성하고 있는 노드간 망이 다른 구성입니다.

(예시)
- 마스터 노드
- 인프라 노드
- 워커 노드


---
## 목적

해당 케이스는 서로 다른 네트워크를 가진 클러스터를 구축 및 운영이 가능합니다.
또한, 필요 시 각 네트워크의 목적 및 설계에 따라 트래픽 유입이 가능한 구조입니다.


---
## 아키텍처

![6_1_diff_network_arch](/assets/images/accordion/6_1_diff_network_arch.png)


---
## 인스톨 프로세스

- **1~8. 서로 같은 대역의 노드만 설정하여 아코디언을 우선 설치합니다.(마스터 노드는 우선 설치 필수)**
- **9. 아코디언 클러스터에 다른 네트워크에 있는 노드를 추가합니다.**

![6_1_diff_network_install_process](/assets/images/accordion/6_1_diff_network_install_process.png)


---
## 주의 사항

- **서로 다른 네트워크에 존재하는 노드 간 PMTU가 다를 경우, PMTU 기준 제일 작은 사이즈로 MTU를 맞춰주어야합니다.**
  + 네트워크간 MTU가 다른 경우, MTU를 맞춰주지 않으면 MTU의 차이로 인해 데이터 전송 시 Drop이 발생할 수도 있습니다.
- **서로 다른 네트워크에 존재하는 VM 혹은 Baremetal에 할당된 NIC 이름이 동일할 경우, 모든 노드를 아코디언 인스톨러를 통해 한번에 설치가 가능합니다.**
- **서로 다른 네트워크에 존재하는 VM 혹은 Baremetal에 할당된 NIC 이름이 다를 경우, 모든 노드를 한번에 설치가 불가능합니다.**
  + 네트워크 대역도 다르고, NIC 이름도 다를 경우 Calico IP_AUTODETECTION_METHOD를 적절하게 수정해주어야 합니다.
  + 마스터 노드 집단만 우선 설치 -> Calico IP_AUTODETECTION_METHOD 수정(Multiple CIDR) -> 인프라 노드, 워커 노드 추가 하는 형태로 설치가 가능합니다.
  + 또한, 아코디언 인스톨러에서 roles/8-weave-kube/templates/calico.yaml 템플릿을 직접 수정 후 설치할 수도 있습니다.