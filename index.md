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

+ **1일차 실습 문제 정리**
  - "1. 네임스페이스"
  - "2. 구성"
    - [실습 문제 2-1 - 컨피그맵](https://training.accordions.co.kr/docs/config/1_configmap/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
    - [실습 문제 2-2 - 시크릿](https://training.accordions.co.kr/docs/config/2_secret/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
  - "3. 스토리지"
    - [실습 문제 3-1 - 스토리지클래스](https://training.accordions.co.kr/docs/storage/3_sc/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
  - "4. 워크로드"
    - [실습 문제 4-1 - 파드](https://training.accordions.co.kr/docs/workload/2_pod/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
    - [실습 문제 4-2 - 디플로이먼트](https://training.accordions.co.kr/docs/workload/3_deploy/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
    - [실습 문제 4-3 - 스테이트풀셋](https://training.accordions.co.kr/docs/workload/4_sts/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
    - [실습 문제 4-4 - 데몬셋](https://training.accordions.co.kr/docs/workload/5_ds/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
    - [실습 문제 4-5 - 잡](https://training.accordions.co.kr/docs/workload/6_job/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
    - [실습 문제 4-6 - 크론잡](https://training.accordions.co.kr/docs/workload/7_cj/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
  - "5. 네트워크"
    - [실습 문제 5-1 - 서비스](https://training.accordions.co.kr/docs/network/1_svc/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
    - [실습 문제 5-2 - 인그레스](https://training.accordions.co.kr/docs/network/2_ingress/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)
  - "6. 카탈로그"
    - [실습 문제 6-1 - 카탈로그](https://training.accordions.co.kr/docs/application/2_catalog/2_1_catalog/#%EC%97%B0%EC%8A%B5%EB%AC%B8%EC%A0%9C)


+ **2일차 실습 문제 정리**
  - "7. 워크로드/구성/네트워크"
    - [실습 문제 7-1 - 시크릿/컨피그맵 활용](https://training.accordions.co.kr/docs/config/5_hands_on/5_1_config)
    - [실습 문제 7-2 - 네트워크 활용](https://training.accordions.co.kr/docs/network/4_hands_on/4_1_service)
  - "8. 카탈로그/파이프라인"
    - [실습 문제 8-1 - 카탈로그/파이프라인](https://training.accordions.co.kr/docs/application/4_hands_on/4_1_catalog_practice)
  - "9. 오토스케일"
    - [실습 문제 9-1 - Time-Based 오토스케일](https://training.accordions.co.kr/docs/workload/8_hands_on/8_1_time_based_autoscale)
    - [실습 문제 9-2 - APM Based 오토스케일](https://training.accordions.co.kr/docs/workload/8_hands_on/8_2_apm_autoscale)
  - "apx. 트러블슈팅"
    - [Case 1 - CrashLoopBackOff 트러블슈팅](https://training.accordions.co.kr/docs/troubleshoot/8_hands_on/8_1_hands_on_crashloopbackoff)
    - [Case 2 - Pending 트러블슈팅](https://training.accordions.co.kr/docs/troubleshoot/8_hands_on/8_2_hands_on_pending)
    - [Case 3 - ImagePullError 트러블슈팅](https://training.accordions.co.kr/docs/troubleshoot/8_hands_on/8_3_hands_on_image_pull_error)