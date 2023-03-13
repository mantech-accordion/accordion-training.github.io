---
layout: default
title: Accordion v2
nav_order: 1
description: "아코디언 교육 소개"
permalink: /
---

# Accordion v2 

![mantech-accordion.svg](/assets/images/mantech-accordion.svg)

Accordion
{: .label .label-purple }

## 강의 소개
이 강의는 Container와 Kubernetes의 기본 이론과 함께 아코디언의을 배울 수 있는 강의입니다. 
본 강의를 통해 전체 시스템에서 운영관리자가 바라봐야할 관점을 이해하고, 서비스 운영을 위한 운영 방법을 익히는 연습을 하실 수 있습니다. 
강의를 마치게 되면, 컨테이너 애플리케이션을 손쉽게 생성하고 관리할 수 있습니다.


---

## 강의 대상
- Container와 Kubernetes 기술 커리어를 시작하고 싶은 사람
- 실제 서비스를 아코디언으로 생성하고 운영해보고 싶은 사람

## 강의를 들어야 하는 이유
- Container와 Kubernetes는 반드시 필요한 기술이고, 아코디언은 빠르게 실무에 적용 가능합니다.
- 단순히 아코디언 사용법을 익히는 것에서 나아가, 운영에서 사용할 수 있는 구조와 스킬들을 익힐 수 있습니다.

## 강의에서 배우는 것들
- 컨테이너 플랫폼 엔지니어가 되기 위해 필요한 기술들은 무엇이 있는지 알 수 있습니다.
- 아코디언을 통해서 컨테이너 기반의 서비스 운영에 필요한 인프라를 구성하고 관리하는 방법에 대해서 배우실 수 있습니다.

## 강의 특징
- 강의 내의 실습은 모든 학습자가 처음부터 시작한다는 가정으로 진행됩니다.
- 강의에서 진행된 모든 명령어는 문서로 정리해서 제공되므로 추후에 혼자 학습하시더라도 내용을 손쉽게 찾아보실 수 있습니다.

## 강의 준비사항
- Container, Kubernetes 에 대한 사전지식
- 사전준비 : ssh client가 설치된 노트북(putty, xshell 등)
- 교육시간 : 10:00 ~ 16:00

## 강의 일정

+ **1일차 - 아코디언 설치 구성**
  - 아코디언v2 소개
  - 아코디언v2 아키텍쳐
  - 아코디언v2 인스톨러 구조 및 설정 방법
  - [실습]아코디언v2 인스톨 & 트러블슈팅

+ **2일차 - 애플리케이션 배포**
  - 아코디언v2 대시보드
  - 아코디언v2 애플리케이션 & 빌드
  - 워크로드, 구성, 네트워크, 접근제어
  - [실습] 헬름 & 카탈로그 배포
  - [실습] 카탈로그 & 태스크 작성

+ **3일차 - 권한 & 모니터링 알림**
  - 멀티 클러스터 계정 권한
  - 모니터링 & 알림
  - [실습]멀티 클러스터 계정 권한
  - [실습]알림 설정
  - 서포트 사이트 사용방법 공유

---

## 실습 문제 링크 정리

+ **1일차 연습 문제 정리**
  - 네임스페이스: [https://training.accordions.co.kr/docs/dashboard/4_ns](https://training.accordions.co.kr/docs/dashboard/4_ns/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
  - 구성
    - 컨피그맵: [https://training.accordions.co.kr/docs/config/1_configmap](https://training.accordions.co.kr/docs/config/1_configmap/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
    - 시크릿: [https://training.accordions.co.kr/docs/config/2_secret](https://training.accordions.co.kr/docs/config/2_secret/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
  - 스토리지
    - 퍼시스턴트볼륨: [https://training.accordions.co.kr/docs/storage/1_pv](https://training.accordions.co.kr/docs/storage/1_pv/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
    - 퍼시스턴트볼륨클레임: [https://training.accordions.co.kr/docs/storage/2_pvc](https://training.accordions.co.kr/docs/storage/2_pvc/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
    - 스토리지클래스: [https://training.accordions.co.kr/docs/storage/3_sc](https://training.accordions.co.kr/docs/storage/3_sc/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
  - 워크로드
    - 파드: [https://training.accordions.co.kr/docs/workload/2_pod](https://training.accordions.co.kr/docs/workload/2_pod/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
    - 디플로이먼트: [https://training.accordions.co.kr/docs/workload/3_deploy](https://training.accordions.co.kr/docs/workload/3_deploy/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
    - 스테이트풀셋: [https://training.accordions.co.kr/docs/workload/4_sts](https://training.accordions.co.kr/docs/workload/4_sts/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
    - 데몬셋: [https://training.accordions.co.kr/docs/workload/5_ds](https://training.accordions.co.kr/docs/workload/5_ds/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
    - 잡: [https://training.accordions.co.kr/docs/workload/6_job](https://training.accordions.co.kr/docs/workload/6_job/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
    - 크론잡: [https://training.accordions.co.kr/docs/workload/7_cj](https://training.accordions.co.kr/docs/workload/7_cj/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
  - 네트워크
    - 서비스: [https://training.accordions.co.kr/docs/network/1_svc](https://training.accordions.co.kr/docs/network/1_svc/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
    - 인그레스: [https://training.accordions.co.kr/docs/network/2_ingress](https://training.accordions.co.kr/docs/network/2_ingress/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
  - 카탈로그: [https://training.accordions.co.kr/docs/application/2_catalog/2_1_catalog](https://training.accordions.co.kr/docs/application/2_catalog/2_1_catalog/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)


+ **2일차 실습 문제 정리**
  - 워크로/구성/네트워크 실습
    - 시크릿 생성/컨피그맵 활용: [https://training.accordions.co.kr/docs/config/5_hands_on/5_1_config](https://training.accordions.co.kr/docs/config/5_hands_on/5_1_config)
    - 네트워크 활용: [https://training.accordions.co.kr/docs/network/4_hands_on/4_1_service](https://training.accordions.co.kr/docs/network/4_hands_on/4_1_service)
  - 카탈로그/파이프라인 실습: [https://training.accordions.co.kr/docs/application/4_hands_on/4_1_catalog_practice](https://training.accordions.co.kr/docs/application/4_hands_on/4_1_catalog_practice)
  - 오토스케일
    - Time-Based: [https://training.accordions.co.kr/docs/workload/8_hands_on/8_1_time_based_autoscale](https://training.accordions.co.kr/docs/workload/8_hands_on/8_1_time_based_autoscale)
    - APM Based: [https://training.accordions.co.kr/docs/workload/8_hands_on/8_2_apm_autoscale](https://training.accordions.co.kr/docs/workload/8_hands_on/8_2_apm_autoscale)

+ **2일차 트러블슈팅 실습 문제 정리**
  - Case 1
    - CrashLoopBackOff 예제: [https://training.accordions.co.kr/docs/troubleshoot/8_hands_on/8_1_hands_on_crashloopbackoff](https://training.accordions.co.kr/docs/troubleshoot/8_hands_on/8_1_hands_on_crashloopbackoff)
  - Case 2
    - Pending 예제: [https://training.accordions.co.kr/docs/troubleshoot/8_hands_on/8_2_hands_on_pending](https://training.accordions.co.kr/docs/troubleshoot/8_hands_on/8_2_hands_on_pending)
  - Case 3
    - ImagePullError 예제: [https://training.accordions.co.kr/docs/troubleshoot/8_hands_on/8_3_hands_on_image_pull_error](https://training.accordions.co.kr/docs/troubleshoot/8_hands_on/8_3_hands_on_image_pull_error)