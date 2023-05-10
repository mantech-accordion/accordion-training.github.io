---
layout: default
title: 2.5.2 Case 2 - 잘못된 VIP 정보
nav_order: 2
parent: 2.5 설치 이슈 모음
grand_parent: 2. Accordion v2
---

# Case 2. 잘못된 VIP 정보
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


---
## 문제 상황

Ansible 플레이북이 수행되는 도중, 레지스트리에 로그인을 하지 못하여 플레이북이 실패하는 경우

![5_2_trb_incorrect_vip_log](/assets/images/accordion/5_2_trb_incorrect_vip_log.png){: width="800" }

- 환경
  + VIP 정보: 10.140.20.9


---
## 원인 및 에러 분석 단계

아코디언은 이미지 레지스트리의 고가용성 확보를 위해 로드밸런서의 VIP를 레지스트리의 주소로 사용합니다.
허나, 이 VIP를 잘못 작성하거나, 방화벽으로 인해 Server -> LB로의 통신이 불가능한 상황이라면 레지스트리로 통신이 불가능하여 플레이북이 실패합니다.

- 엔서블 로그 확인

- Curl을 통해 직접 호출 확인

![5_2_trb_incorrect_vip_curl_result](/assets/images/accordion/5_2_trb_incorrect_vip_curl_result.png){: width="600" }

- netstat을 통해 레지스트리 포트가 listening 상태인지 확인

```
$ netstat -tnlp | egrep -i "5000|5001"

root@localhost:~# netstat -tnlp | egrep -i "5000|5001"
tcp6       0      0 :::5001                 :::*                    LISTEN      979/registry
```

- 방화벽이 있는지 확인

- group_vars 설정 내용 확인


---
## 해결 방법

- 포트가 리스닝 중인데 통신이 되지 않는 원인은 방화벽에서 해당 포트를 DROP 하거나, VIP 설정이 잘못 기입되어있는 경우 발생합니다.
  + `group_vars/{host | member}.yml`에서 `base_registry_address` 및 `base_registry_port` 를 제대로 작성했는지 확인합니다.
  + `base_registry_address`를 주어진 정보(10.140.20.9)로 기입하고 설치합니다.

![5_2_trb_incorrect_vip_group_vars](/assets/images/accordion/5_2_trb_incorrect_vip_group_vars.png){: width="400" }
