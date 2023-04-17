---
layout: default
title: 2.6.8 Case 8 - Managed K8s
nav_order: 8
parent: 2.6 설치 케이스 모음
grand_parent: 2. Accordion v2
---

# Case 8
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## Managed K8s 환경

아코디언은 On-premise, Private Cloud, Public Cloud 등등 환경의 제약을 받지 않고 K8s 클러스터가 구성되어 있는 모든 플랫폼에서 설치가 가능합니다.
EKS, AKS, NKS 등 다양한 Managed Kubernetes 환경에서도 마찬가지로 아코디언 설치가 가능합니다.


---
## 목적

Managed Kubernetes 환경에서 아코디언을 설치하여 다양한 클라우드 환경에서도 아코디언을 통해 K8s 클러스터 관리 및 모니터링 등 관리 기능을 제공합니다.

---
## 아키텍처

- **EKS 아키텍처**

![6_8_managed_k8s_arch_eks](/assets/images/accordion/6_8_managed_k8s_arch_eks.png){: width="800" }

- **AKS 아키텍처**

![6_8_managed_k8s_arch_aks](/assets/images/accordion/6_8_managed_k8s_arch_aks.png){: width="800" }

- **NKS 아키텍처**

![6_8_managed_k8s_arch_nks](/assets/images/accordion/6_8_managed_k8s_arch_nks.png){: width="800" }


---
## 인스톨 프로세스

- 현재 아코디언 인스톨러에서는 멤버클러스터로의 Join 과정만 지원하고 있습니다.
- 추후 클러스터 프로비저닝 단계부터 설치하는 것도 지원 예정에 있습니다.


---
## 주의 사항

- 호스트 클러스터와 멤버클러스터 조인하는 Managed K8s 클러스터간 방화벽이 오픈되어야 합니다.