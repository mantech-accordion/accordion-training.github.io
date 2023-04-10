---
layout: default
title: 2.6.5 Case 5 - vxlan
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


## Calico Backend를 vxlan을 사용

Calico CNI의 Backend 프로토콜로 IP in IP 프로토콜이 아닌 vxlan을 사용하는 예시입니다.

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

- UDP 방화벽

![acc-5.png](/assets/images/accordion/acc-5.png)