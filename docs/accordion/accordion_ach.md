---
layout: default
title: 2-2. Accordion 아키텍쳐
nav_order: 2
parent: 2. Accordion v2
---

# 2-1. 아코디언v2 아키텍쳐
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---


## 아코디언v2 아키텍쳐
![acc-5.png](/assets/images/accordion/acc-5.png){: width="800" }

![acc-6.png](/assets/images/accordion/acc-6.png){: width="800" }


---

## 아코디언v1와 차이점

## 멀티클러스터 통합 관리
개발, 테스트, 운영, 외부 클라우드, 분리된 네트워크 망 등에 분산 구성된 K8S 클러스터를 단일 콘솔로 관리할 수 있고 Host Cluster를 통해 K8S 클러스터를 매우 쉽게 배포할 수 있습니다.

![acc-7.png](/assets/images/accordion/acc-7.png){: width="800" }


- Host-Member 구조
- Single GUI
- K8S Cluster 자동 배포
- Cluster간 앱 배포
- 통합 권한 설정
- 통합 모니터링

---

## 멀티 클라우드 환경 지원
AWS, Azure, GKE, NCP, VMware등 여러 CSP들이 K8S 서비스를 제공하지만 구성과 관리 방식이 제각각 입니다. 아코디언을 통해 단일화된 메뉴로 클러스터를 배포하고 통합 관리할 수 있습니다.

![acc-8.png](/assets/images/accordion/acc-8.png){: width="800" }
{: .mb-lg-4 }

---

## 다양한 앱 이미지 번들
개발에 필요한 환경과 앱의 구성에 소요되는 시간을 단축할 수 있어 개발 생산성을 극대화 할 수 있습니다. 앱에 대한 전문 지식이 없어도 카탈로그에서 쉽게 앱을 배포합니다.

![acc-9.png](/assets/images/accordion/acc-9.png){: width="800" }

---

## CI/CD pipeline
내장된 CI/CD pipeline을 통해 멀티 클라우드 환경에서 컨테이너를 쉽게 배포할 수 있으며, 다양한 배포 템플릿 제공으로 별도의 전문 개발 비용을 상당히 절감할 수 있습니다.

![acc-10.png](/assets/images/accordion/acc-10.png){: width="800" }


GUI를 통해 복잡한 스크립트나 개발 필요없이 쉽게 CI/CD Pipeline을 생성하고 과정을 가시화 할 수 있으며, 멀티 테넌시의 지원으로 민감한 배포 과정의 전략에 대한 보안을 유지할 수 있습니다. 

![acc-11.png](/assets/images/accordion/acc-11.png){: width="800" }

---

## 멀티 클러스터 간 빌드/배포 자동화
Cluster to Cluster Deploy : 개발기, 검증기, 운영기 등 서로 다른 클러스터 환경에서 앱을 자동으로 배포할 수 있습니다.

## Auto Scaling
CPU, Memory 사용량에 따른 Pod 자동 확장/축소를 지원하며 
Thread, TPS, GCtime, Elapsed time 등 다양한 메트릭 기준으로 Auto Scale in/out 지원합니다.

## 다양한 K8S 클러스터에 대한 통합 모니터링
분리된 K8S 클러스터와 CSP별로 모니터링 콘솔을 여러 개 띄울 필요가 없습니다. K8S 클러스터, 시스템, 노드, 네임스페이스, 워크로드, 애플리케이션, 감사 로그를 단일 콘솔에서 모니터링 할 수 있습니다.

## 더 세밀해진 애플리케이션 모니터링
내장된 APM을 통해 Active service, X log, TPS, 응답시간, 쓰레드 등의 더 세밀한 앱 성능 모니터링을 제공합니다.

## 통합 인증 / 권한
다중 테넌트 관리를 위해 통합 인증을 제공합니다. Cluster, Namespace, User 별로 권한을 
상세히 설정할 수 있으며, 쿠버네티스의 RBAC와 자동 연동 설정 됩니다.

## 컨테이너에 대한 보안 취약성 검사
아코디언은 Sonarqube와 Anchore를 통해 빌드 전 소스코드 검사, 배포전 POD에 대한 검사를 통해 보안 취약한 소스와 앱을 걸러낼 수 있으며, 3rd party 툴과의 연계 또한 가능합니다.

## 보안 취약한 앱의 배포 차단
코드 및 컨테이너 보안 취약성 검사 단계를 CI/CD Pipeline의 단계에 적용함으로써 보안 정책에 위배된 앱을 배포 단계에서 원천 차단할 수 있습니다.
감사로그를 통해서 외부 침입을 추적하고, 모든 활동을 시간 별로 자동 기록합니다.

## 다양한 알림 기능
이메일, SMS, 슬랙을 통해 주요 이벤트에 대한 알람 수신을 받을 수 있습니다.


