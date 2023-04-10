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
- 내부망) 마스터 3대 + 인프라 2대 + 워커 2대
- 외부망) 워커 2대

위와 같은 케이스를 통해, 내부망에는 내부망 서비스용 Pod를 배치하고 외부망 노드에는 외부 서비스용 Pod를 배치하여 운영이 가능합니다.
또한, 필요 시 외부망 노드에 Ingress Controller Pod를 배치하여 내부망 서비스Pod에도 Ingress Controller를 통해 외부 트래픽 유입이 가능한 구조입니다.


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

- 적절한 Affinity 설정

![acc-5.png](/assets/images/accordion/acc-5.png)