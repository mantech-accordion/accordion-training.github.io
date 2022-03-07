---
layout: default
title: 2-4-2. 인스톨러 구조
nav_order: 4
parent: 2-4. Accordion 설치
grand_parent: 2. Accordion v2
---

# 2-4-2. Accordion 설치
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 인스톨러 구조

### accordion-installer
```bash
accordion-installer/
|-- roles           # 디렉토리  
|-- group_vars      # 디렉토리
|-- hosts           # cluster구성할 hosts 설정
|-- install.sh      # 설치 
|-- uninstall.sh    # 삭제
|-- status.sh       # 설치 후 상태확인
|-- add-aks.sh
|-- add-eks.sh
|-- add-kubeconfig.sh
|-- addaks.yml
|-- addeks.yml
|-- addkubeconfig.yml
|-- addmaster.sh
|-- addmember.sh
|-- addmember.yml
|-- addnode.sh
|-- all.retry
|-- all.yml
|-- ansible.cfg
|-- getconfig.yml
|-- kube-teardown.retry
|-- kube-teardown.yml
|-- lic.txt
|-- master.yml
|-- node.yml
|-- remove-aks.sh
|-- remove-eks.sh
|-- removeaks.yml
|-- removeeks.yml
|-- removemember.sh
|-- removemember.yml
|-- removenode.sh
|-- restore.sh
|-- restore.yml
|-- run_role.yml
`-- THIRDPARTYLICENSE.txt
```

- group_vars
```bash
group_vars/
|-- host.yml
|-- all.yml
|-- config.yml
|-- aks.yml
|-- eks.yml
|-- etcd-master-cluster-manager.yml
|-- etcd-master-cluster-member.yml
`-- member.yml
```

- roles
```bash
roles/
|-- 0-rpms-install
|-- 1-add-uid-gid
|-- 2-nfs
|-- 3-kube-prerequisite
|-- 4-add-containerd
|-- 4-containerd
|-- 4-cri-o
|-- 5-kube-install
|-- 6-kube-init-join
|-- 6-kube-init-join-cluster
|-- 6-kube-init-join-cluster-single
|-- 7-node-label
|-- 8-weave-kube
|-- 9-acc-registry
|-- 10-crd
|-- 11-acc-system
|-- 12-acc-global
|-- 13-acc-global-after
|-- 14-backup
|-- add-aks
|-- add-eks
|-- add-gpu
|-- add-kubeconfig
|-- add-master
|-- add-node
|-- cloud-acc-system
|-- cloud-crd
|-- kube-teardown
|-- member-info
|-- remove-aks
|-- remove-eks
|-- remove-node
|-- restore-etcd
`-- restore-etcd-single
```

---

**설치 준비사항**
- ssh key 생성, 복사, 접속 확인
- Ansible 설치 (아코디언 설치 패키지에 포함)
- /etc/hosts 파일 수정

**아코디언 설치 설정**
- accordion-installer/hosts 수정
- accordion-installer/group_vars/host.yml 수정

**아코디언 설치 및 확인**
- accordion-installer/install.sh
- accordion-installer/status.sh

**설치 설정**
```bash
$ accordion-installer/install.sh
```

**설치 진행**
```bash
$ accordion-installer/install.sh
End User Software License Agreement

This is a legal agreement between Customer and Man Technology Co., LTD. ("Mantech").  YOU MUST READ AND AGREE TO THE TERMS OF THIS END USER SOFTWARE LICENSE AGREE
MENT ("AGREEMENT") BEFORE ANY SOFTWARE CAN BE DOWNLOADED OR INSTALLED OR USED.  BY CLICKING ON THE "ACCEPT" BUTTON OR TYPING THE "Y" OF THIS AGREEMENT, OR DOWNLOA
DING, INSTALLING OR USING THE SOFTWARE, YOU ARE AGREEING TO BE BOUND BY THE TERMS AND CONDITIONS OF THIS AGREEMENT.  IF YOU DO NOT AGREE WITH THE TERMS AND CONDIT
IONS OF THIS AGREEMENT, THEN YOU SHOULD NOT DOWNLOAD, INSTALL OR USE THE SOFTWARE.  BY DOING SO YOU FORGO ANY IMPLIED OR STATED RIGHTS TO DOWNLOAD OR INSTALL OR U
SE THE SOFTWARE.
...
...
16. Questions.  Should you have any questions concerning the foregoing, please contact Mantech at the following address: Man Technology Co., LTD. 12th Fl, 308-4,
Seongsudong 2ga, Seongdong-gu, Seoul, Korea.
                 Phone : +82-2-2136-6900
                 E-mail : marketing@mantech.co.kr
                 www.mantech.co.kr


DO YOU ACCEPT THE TERMS OF THIS LINCESE AGREEMENT? [y/n] : y
```

**설치 확인**
```bash
$ accordion-installer/status.sh
========================================
 nodes
========================================
NAME         STATUS   ROLES                  AGE    VERSION
acc-master   Ready    control-plane,master   177m   v1.20.8
acc-node1    Ready    worker                 176m   v1.20.8
========================================
 deployments/po/svc
========================================
NAMESPACE     NAME                                           READY   UP-TO-DATE   AVAILABLE   AGE
acc-global    deployment.apps/alert-apiserver                1/1     1            1           162m
acc-global    deployment.apps/authset-manager                1/1     1            1           161m
acc-global    deployment.apps/chartmuseum-chartmuseum        1/1     1            1           163m
acc-global    deployment.apps/cloud-apiserver                1/1     1            1           161m
acc-global    deployment.apps/clusterinfo-manager            1/1     1            1           172m
acc-global    deployment.apps/console                        1/1     1            1           162m
acc-global    deployment.apps/gateway                        1/1     1            1           162m
acc-global    deployment.apps/host-log-apiserver             1/1     1            1           162m
acc-global    deployment.apps/keycloak                       1/1     1            1           163m
acc-global    deployment.apps/keycloak-db                    1/1     1            1           163m
acc-global    deployment.apps/manual-webserver               1/1     1            1           161m
acc-global    deployment.apps/monitoring-apiserver           1/1     1            1           162m
acc-global    deployment.apps/setting-manager                1/1     1            1           163m
acc-global    deployment.apps/thanos-querier                 1/1     1            1           163m
acc-system    deployment.apps/acc-grafana                    1/1     1            1           170m
acc-system    deployment.apps/acc-kube-state-metrics         1/1     1            1           170m
acc-system    deployment.apps/accordion-ingress-controller   1/1     1            1           170m
acc-system    deployment.apps/apm-agent-injector             1/1     1            1           166m
...
...

```

**아코디언 접속 URL**

| URL      | ID    | PW    |
|:---------|:------|:------|
| https://VIP://30000      | admin  | accordion!@# |

![acc-ins-1.png](/assets/images/accordion/acc-ins-1.png){: width="800" }


