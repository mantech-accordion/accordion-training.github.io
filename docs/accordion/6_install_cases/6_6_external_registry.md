---
layout: default
title: 2.6.6 Case 6 - 외부 레지스트리
nav_order: 6
parent: 2.6 설치 케이스 모음
grand_parent: 2. Accordion v2
---

# Case 6
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## 외부 레지스트리 사용

컨테이너 레지스트리는 컨테이너 이미지를 Pull / Push 하기 위하여 사용합니다.
아코디언은 2개의 컨테이너 레지스트리를 사용합니다.
- Base Registry
- User Registry

카탈로그 혹은 파이프라인을 통해 생성된 컨테이너 이미지를 담거나, 사용자가 임의로 사용하기 위한 이미지를 담기 위해 유저 레지스트리를 사용합니다.
만약, 이미 구축되어 있는 컨테이너 레지스트리가 있다면 유저 레지스트리는 외부에 이미 존재하는 레지스트리를 사용할 수 있습니다.

---
## 목적

이미 구축되어 있는 컨테이너 레지스트리를 사용하여 레지스트리 중앙 관리가 가능합니다.


---
## 아키텍처

![acc-5.png](/assets/images/accordion/acc-5.png)


---
## 인스톨 프로세스

![acc-5.png](/assets/images/accordion/acc-5.png)


---
## 주의 사항

- 아코디언의 모든 노드에서 해당 레지스트리로의 방화벽이 오픈되어야합니다.
- 레지스트리로 HTTPS 통신을 위한 인증서 설정이 필요합니다.