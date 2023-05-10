---
layout: default
title: 2.5.3 Case 3 - 잘못된 NIC 이름
nav_order: 3
parent: 2.5 설치 이슈 모음
grand_parent: 2. Accordion v2
---

# Case 3. 잘못된 NIC 이름
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


---
## 문제 상황

Ansible 플레이북이 수행되는 도중, `AnsibleUndefinedVariable` 에러로 인해 플레이북이 실패하는 경우

![5_3_trb_incorrect_nic_log](/assets/images/accordion/5_3_trb_incorrect_nic_log.png){: width="800" }

- 환경
  + NIC 이름(공통): ens192


---
## 원인 및 에러 분석 단계

Calico CNI에서 사용할 클러스터 트래픽을 위한 NIC을 각 노드마다 정해주어야합니다.
허나, 이 NIC 이름을 잘못 작성하거나, 노드마다 다른 경우 `IP_AUTODETECTION_METHOD=cidr`로 지정해주면 됩니다.

- 엔서블 로그 확인

- 각 노드의 NIC(Network Card Interface)명 확인

```
root@localhost:/opt/accordion-installer# ansible -i hosts host-cluster -m shell -a "ip -c -br -4 a s | egrep -v 'cilium|lo'"
c-ostack-acc-ha-master-2 | CHANGED | rc=0 >>
ens192             UP             10.60.100.2/16
c-ostack-acc-ha-wrk-3 | CHANGED | rc=0 >>
ens192             UP             10.140.20.6/16
c-ostack-acc-ha-wrk-1 | CHANGED | rc=0 >>
ens192             UP             10.140.20.4/16
c-ostack-acc-ha-ifr-3 | CHANGED | rc=0 >>
ens192             UP             10.140.20.9/16
c-ostack-acc-ha-ifr-2 | CHANGED | rc=0 >>
ens192             UP             10.140.20.8/16
c-ostack-acc-ha-ifr-1 | CHANGED | rc=0 >>
ens192             UP             10.140.20.7/16
c-ostack-acc-ha-master-3 | CHANGED | rc=0 >>
ens192             UP             10.60.100.3/16
c-ostack-acc-ha-wrk-2 | CHANGED | rc=0 >>
ens192             UP             10.140.20.5/16
c-ostack-acc-ha-master-1 | CHANGED | rc=0 >>
ens192             UP             10.140.20.3/16
```

- group_vars 설정 내용 확인


---
## 해결 방법

- 노드가 실제 사용 중인 NIC 이름으로 `group_vars/{host | member}.yml`에서 `acc_interface` 값을 변경해줍니다.
