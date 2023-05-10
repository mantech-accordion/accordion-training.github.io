---
layout: default
title: 2.5.1 Case 1 - 잘못된 NAS 정보
nav_order: 1
parent: 2.5 설치 이슈 모음
grand_parent: 2. Accordion v2
---

# Case 1. 잘못된 NAS 정보
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


---
## 문제 상황

Ansible 플레이북이 수행되는 도중, 레지스트리에 로그인을 하지 못하여 플레이북이 실패하는 경우

![5_1_trb_incorrect_nas_log](/assets/images/accordion/5_1_trb_incorrect_nas_log.png){: width="800" }

- 환경
  + NAS 정보: oss-tech-nas.test.local:/volume1/tech/hwpark/clusters
  + nfs_setup: external


---
## 원인 및 에러 분석 단계

아코디언은 카탈로그 및 이미지 레지스트리 데이터의 기본 저장소로 NFS 프로토콜을 사용하는 NAS를 저장소로 사용하고 있습니다.
허나, 이 경로를 잘못 작성하거나, NAS 서버와의 통신이 불가능한 경우 Registry Volume을 생성하지 못하고 레지스트리가 기동되지 못하여 플레이북이 실패합니다.


- 엔서블 로그 확인

- Podman 로그 확인

```
Apr  6 10:04:29 c-acc-training-master1 podman[669930]: Error: unable to start container c837f0962773e656b676e53402e174fdf602735525781d0153af7929c9b82d67: error mounting volume registry_vol for container c837f0962773e656b676e53402e174fdf602735525781d0153af7929c9b82d67: mount.nfs: mounting oss-tech-nas.test.local:/volume1/tech/hwpark1/clusters/tests/accordion-registry failed, reason given by server: No such file or directory
```

NAS 서버에서 export한 경로 `oss-tech-nas.test.local:/volume1/tech/hwpark/clusters` 와 `accordion-installer/group_vars/host.yml` 설정이 서로 차이가 나는 부분을 확인합니다.


---
## 해결 방법

- `group_vars/{host | member}.yml`에서 `nfs_path`를 제대로 작성했는지 확인합니다.
  + `nfs_path`를 주어진 정보대로 정확하게 입력하고 설치합니다.

![5_1_trb_incorrect_nas_yml](/assets/images/accordion/5_1_trb_incorrect_nas_yml.png){: width="400" }