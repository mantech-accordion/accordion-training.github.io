---
layout: default
title: 5.5.1 카탈로그 실습1
nav_order: 1
parent: 5.5 실습
grand_parent: 5. 애플리케이션
---

# 카탈로그 
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

<div class="code-example" markdown="1">
Namespace
{: .label .label-green }
</div>

---

## 연습문제

**1. 커스텀 파이프라인을 이용해서 카탈로그를 완성하고 워크로드를 배포하세요.**

일반설정
```
- name: catalog-practice
- 카탈로그 : acc-tomcat
- 상세설명 : 카탈로그 생성
- 고급설정 : 배포 클러스터(host-cluster), 네임스페이스 선택
- 컨테이너 이미지 정책 : 레지스트리 user-registry, 보관개수 10
```

배포 리소스 설정
```
- 레플리카 파드 수 : 2
- resource.limits.memory : 1.5Gi
- serviceType : ClusterIP
```

파이프라인 설정
```
1. vcs-get: Git 정보 입력
- repository: https://github.com/mantech-accordion/jpetstore-6.git
- ref(branch): master
- auth: none
- cleanWorkspace: true
- workspace: scm


2. echo 테스크 추가
- 다른 테스크 템플릿 불러오기: acc-shell
    - 수행할 명령어: pwd && ls -l *; 
- 테스크 이름: echo
- 테스크 연관 관계: src-build.Succeeded


3. tomcat 버전 선택
- dockerfile-tomcat 테스크에서 baseImage 선택
    - base.registry.accordions.co.kr:5000/tomcat:9-jdk8
- 테스크 연관 관계: echo.Succeeded


4. 승인 테스크 추가
- 다른 테스크 템플릿 불러오기: 승인
    - 승인자 목록: admin
- 테스크 이름: approve
- 테스크 연관 관계: image-build.Succeeded
```

**2. 생성된 카탈로그를 배포하세요.**


**3. 승인 테스크 단계에서 승인을 눌러 다음 단계를 진행하세요.**


**4. 배포된 워크로드 상태를 워크로드 대시보드에서 확인하세요.**