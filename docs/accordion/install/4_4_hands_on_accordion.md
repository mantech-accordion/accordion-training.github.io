---
layout: default
title: 2.4.4 👨‍💻 실습
nav_order: 4
parent: 2.4 Accordion 설치
grand_parent: 2. Accordion v2
---

# 2.4.4 👨‍💻 [실습]아코디언v2 인스톨
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 실습 문제

**1. 아래 정보대로 아코디언을 설치하세요.**

```
<노드 정보>
- Host Cluster:
    - Master Node 1
        - hostname: host-master1
          IP: 10.60.100.171
    - Master Node 2
        - hostname: host-master2
          IP: 10.60.100.172
    - Master Node 3
        - hostname: host-master3
          IP: 10.60.100.173
    - Worker Node 1
        - hostname: host-worker1
          IP: 10.60.100.174
    - Worker Node 2
        - hostname: host-worker2
          IP: 10.60.100.175

- Member Cluster:
    - Master Node 1
        - hostname: host-master1
          IP: 10.60.100.177
    - Worker Node 1
        - hostname: host-worker1
          IP: 10.60.100.178
    - Worker Node 2
        - hostname: host-worker2
          IP: 10.60.100.179

- NAS 정보:
    - IP: 10.10.0.85
      PATH: /volume1/tech

- 호스트 클러스터용 LB 정보:
    - IP: 10.140.20.8
- 멤버 클러스터용 LB 정보:
    - IP: 10.140.20.9
    
```

```
1. 호스트 클러스터 설치
    1.1 클러스터 이름: host-cluster
    1.2 마스터 3중화
        1.2.1 마스터 노드에는 일반적인 Pod가 배치되지 않도록 설정
    1.3 외부 L4 VIP: <부여받은 정보>
    1.4 컨테이너 런타임: containerd
    1.5 SELinux permissive 모드로 설치 진행
    1.6 스토리지
        1.6.1 NFS v3 사용
        1.6.2 NFS IP:PATH = <부여받은 정보>
    1.7 유저 레지스트리는 harbor로 설치
    1.8 노드간 같은 대역일 경우 캡슐화를 하지않고, 망이 다를 경우만 캡슐화하도록 설정
    1.9 kube-proxy는 IPVS로 프록시할 수 있게 설정
    1.10 컨테이너, addon 파일, tmp 파일이 쌓일 경로는 /data 아래에 쌓이도록 설정

2. 멤버 클러스터 설치
    2.1 클러스터 이름: member-cluster
    2.2 싱글 마스터
        2.2.1 마스터 노드에는 일반적인 Pod가 배치되지 않도록 설정
    2.3 컨테이너 런타임: containerd
    2.4 SELinux permissive 모드로 설치 진행
    2.5 스토리지
        2.5.1 NFS v3 사용
        2.5.2 NFS IP:PATH = <부여받은 정보>
    2.6 유저 레지스트리는 호스트 클러스터와 별도로 구성하며, harbor로 설치
    2.7 노드간 같은 대역일 경우 캡슐화를 하지않고, 망이 다를 경우만 캡슐화하도록 설정
    2.8 kube-proxy는 iptables로 프록시할 수 있게 설정
    2.9 컨테이너, addon 파일, tmp 파일이 쌓일 경로는 /data 아래에 쌓이도록 설정
```