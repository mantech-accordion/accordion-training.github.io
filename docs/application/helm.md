---
layout: default
title: 3-1. Helm
nav_order: 1
parent: 3. 애플리케이션
---

# 3-1. Helm
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Helm 이란?
Helm은 Kubernetes 애플리케이션 관리를 지원합니다. 
Helm 차트는 가장 복잡한 Kubernetes 애플리케이션을 정의, 설치 및 업그레이드하는 데 도움이 됩니다.

![helm-1.png](/assets/images/application/helm-1.png)


[https://helm.sh/](https://helm.sh/)

**복잡성 관리**

차트는 가장 복잡한 앱도 설명하고 반복 가능한 애플리케이션 설치를 제공하며 단일 권한 지점 역할을 합니다.

**쉬운 업데이트**

인플레이스(in-place) 업그레이드 및 사용자 지정 후크를 사용하여 업데이트의 고통을 덜어줍니다.

**간단한 공유**

차트는 공용 또는 개인 서버에서 쉽게 버전을 지정하고 공유하고 호스팅할 수 있습니다.

**롤백**

helm rollback이전 버전의 릴리스로 쉽게 롤백하는 데 사용 합니다.


---

## 아코디언 Helm
Kubernetes 환경에서 Helm을 사용하기 위해서는 `helm cli`을 설치하고 차트를 관리해야합니다.
아코디언은 이러한 준비 과정을 단축시켜 사용자가 바로 앱을 배포할 수 있도록 제공합니다.

![helm-2.png](/assets/images/application/helm-2.png)

- Helm 3.5.1 지원
- 아코디언에서 간편하게 차트 배포
- 효율적인 차트 관리
- 안전한 비공개 저장소

---
## Helm Chart Repository

**차트관리**

아코디언에서는 Helm 을 사용하기 위해서는 먼저 차트 저장소를 등록해야합니다. 기존 사용중이었던 차트 저장소도 간편하게 등록 및 관리 가능합니다.

![helm-repo-1.png](/assets/images/application/helm-repo-1.png)

| 항목        |  설명  |
|:------------|:-------|
| NAME        | 저장소 이름 (필수) | 
| URL         | 저장소 URL (필수)  | 
| ID          | 저장소 아이디 (옵션)  | 
| PASSWORD    | 저장소 패스워드 (옵션)  | 

**아코디언 차트 저장소**

아코디언에서 제공하고 있는 비공개 저장소는 Go(Golang)로 작성된 오픈 소스 Helm 차트 리포지토리 서버입니다.

Google Cloud Storage, Amazon S3, Azure Blob Storage, Openstack Object Storage 를 포함한 클라우드 스토리지 백엔드를 지원합니다.

![helm-repo-2.png](/assets/images/application/helm-repo-2.png)

---
## Helm Chart 배포

**헬름 런치**

메뉴 --> 애플리케이션 --> 헬름 --> 런치 를 클릭하면 헬름 저장소에 등록된 차트를 배포할 수 있습니다.

![helm-3.png](/assets/images/application/helm-3.png)

**README**

차트의 README 파일을 확인할 수 있습니다.

![helm-4.png](/assets/images/application/helm-4.png)

**Value.yaml**

차트의 `value.yaml` 을 편집할 수 있습니다.
배포할 앱 이름을 입력하고 `런치` 를 클릭하면 앱 배포가 시작됩니다.

![helm-5.png](/assets/images/application/helm-5.png)


**헬름 앱**

배포된 앱은 `헬름 앱`에서 확인할 수 있습니다.
네임스페이스, 상태, 차트, 앱버전 정보를 제공합니다.

![helm-6.png](/assets/images/application/helm-6.png)

**헬름 앱 리소스**

`헬름 앱`을 클릭하면 자세한 배포 리소스 정보를 확인할 수 있습니다. 
`헬름 앱 리소스` 에서는 워크로드와 yml 내용을 제공합니다.

![helm-7.png](/assets/images/application/helm-7.png)

---

