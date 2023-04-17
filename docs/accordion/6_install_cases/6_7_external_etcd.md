---
layout: default
title: 2.6.7 Case 7 - 외부 ETCD
nav_order: 7
parent: 2.6 설치 케이스 모음
grand_parent: 2. Accordion v2
---

# Case 7
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## 외부 ETCD

Etcd는 Key-Value 형태의 데이터를 저장하는 스토리지입니다.
K8s 클러스터의 상태나 설정 정보들을 저장하는 역할을 합니다.
Etcd가 다운된다면 K8s 클러스터는 정상 동작을 하지 않게 됩니다.

대규모 클러스터일 수록 K8s 클러스터에서 API 처리를 담당하는 kube-apiserver와 그에 맞는 상태, 설정 정보를 저장하는 Etcd는 많은 부하를 받게 됩니다.
따라서, 마스터 노드의 부하에 영향을 덜 받게하면서, 보다 안정적인 구성을 위해 Etcd를 별도의 노드로 구성을 할 수 있습니다.

---
## 목적

- Etcd 외부 구성을 통해 보다 안정적인 Etcd의 가용성을 보장할 수 있습니다.
- 마스터 노드에 발생하는 부하에 영향을 받지 않을 수 있습니다.


---
## 아키텍처

![6_7_external_etcd_arch](/assets/images/accordion/6_7_external_etcd_arch.png){: width="1000" }


---
## 인스톨 프로세스

- hosts 파일 수정
  + etcd host 추가
  + host-etcd 그룹에 추가

- group_vars/host.yml 파일 수정
  + etcd_external  “yes”로 수정
  + group_vars/etcd-master-cluster-host.yml 수정 (host etcd external설정 시)
  + etcd_count : etcd 서버의 개수 설정
  + etcd_hostname : etcd hostname
  + etcd_ip: etcd ip


---
## 주의 사항

- Etcd 클러스터와 마스터 노드간 방화벽이 오픈되어야 합니다.
- 외부 Etcd 클러스터도 마찬가지로 고가용성 구성을 위해선 Quorum Policy를 만족시켜야합니다. (홀 수 노드)