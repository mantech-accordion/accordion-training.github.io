---
layout: default
title: 5.4.1 카탈로그 실습
nav_order: 1
parent: 5.4 실습
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

**1. DevSecOps 파이프라인을 이용해서 카탈로그를 완성하고 워크로드를 배포하세요.**

일반설정
```
- name: catalog-practice
- 카탈로그 : acc-tomcat
- 상세설명 : 카탈로그 생성
- 고급설정 : 배포 클러스터(host-cluster), 네임스페이스 선택
- 컨테이너 이미지 정책 : 레지스트리 user-registry, 보관개수 3
```

배포 리소스 설정
```
- 레플리카 파드 수 : 2
- resource.limits.cpu : 1
- resource.limits.memory : 2Gi
- serviceType : NodePort
```

파이프라인 설정
```
1. vcs-get : Git 정보 입력
- repository : https://github.com/mantech-accordion/jpetstore-6.git
- ref(branch): master


2. 코드 분석 테스크 추가
- 다른 테스크 템플릿 불러오기 : acc-src-static-code-analysis
- 테스크 이름 : code-inspection
- 테스크 연관 관계 : src-build.Succeeded


3. 레지스트리 푸시 장소 변경
- additionalCreds: user-registry
- regcred
  - 푸시 레지스트리: user-registry


4. 이미지 서명 테스크 추가
- 다른 테스크 템플릿 불러오기 : image-sign
- 테스크 이름 : image-sign
- 테스크 연관 관계 : image-build.Succeeded
```

**2. 생성된 카탈로그의 배포를 실행하세요.**


**3. 배포된 워크로드 상태를 워크로드 대시보드에서 확인하세요.**