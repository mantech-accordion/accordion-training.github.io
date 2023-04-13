---
layout: default
title: 2.6.4 Case 4 - Calico vxlan
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


## Calico Backend를 vxlan을 사용

일반적으로 IANA(Internet Assigned Numbers Authority)에서는 아래 정보대로 프로토콜 번호를 정의하고 있습니다.
- ICMP = 1
- IPIP = 4
- TCP = 6
- UDP = 17

ICMP/TCP/UDP를 제외한 다른 프로토콜을 정책상 허용할 수 없는 환경에서는 IPIP를 통한 encapsulation을 할 수가 없습니다.
따라서, Calico에서 IPIP가 아닌 다른 프로토콜을 사용하여야하는데, 이때 vxlan을 사용할 수 있습니다.


---
## 목적

Calico CNI의 Backend 프로토콜로 IPIP 프로토콜이 아닌 vxlan을 사용하여, IPIP 프로토콜을 오픈하지않아도 아코디언을 설치할 수 있습니다.


---
## 아키텍처

![6_4_calico_vxlan_arch](/assets/images/accordion/6_4_calico_vxlan_arch.png){: width="1000" }


---
## 인스톨 프로세스

- Calico Mode를 vxlan으로 변경하고, 나머지는 동일한 설치 프로세스로 진행합니다.

![6_4_calico_vxlan_option](/assets/images/accordion/6_4_calico_vxlan_option.png){: width="500" }


---
## 주의 사항

- vxlan을 위한 UDP 방화벽 오픈 필요합니다.
- Pod CIDR가 노드의 CIDR와 중복되지 않도록 주의해야합니다.