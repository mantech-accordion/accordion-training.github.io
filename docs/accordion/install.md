---
layout: default
title: 2-2. Accordion 설치
nav_order: 2
parent: 2. Accordion 소개
---

# 2-2. Accordion 설치
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 아코디언 설치 - 시스템 요구사항
- Accordion 서버는 가상 시스템이나 물리 시스템에 설치가 가능합니다.
- Accordion 서버를 설치하기 위해서는 Master 서버 3대와 서비스를 수행 할 Node 서버 2대 이상 있어야 합니다.
- Master, Node 서버 간에는 네트워크가 가능해야 하고 인터넷이 가능해야 합니다.(인터넷이 불가한 상황인 경우 별도 설치파일을 다운로드 받아야 합니다.)
- Master 서버와 Node 서버 간에 ssh 접근이 가능해야 합니다. (root 접속필요)
- Master/Node 서버 시간은 동일해야 합니다.


### OS 운영체제
- CentOS : 7.4 이상 (CentOS 8 미지원)
- RHEL : 7.4 또는 8.4 이상
- Ubuntu: 18.04 이상
- OracleLinux: 7.4 또는 8.4 이상
- RHCK 커널 지원, UEK 커널 미지원

### 노드별 시스템 요구사항

| 구분        | CPU | MEMORY | DISK |
|:-------------|:------------------|:------|:------|:------|
| Master       | 최소 8core | 최소 16GB  | 최소 500GB |
| Node(s)      | 최소 8core   | 최소 16GB | 최소 300GB |

### 아코디언 사용 Port

| 구분         | Port     | 용도 |
|:-------------|:---------|:------|
| Master       | 30000    | 아코디언 Web Admin |
| Node(s)      | 80/443   | 애플리케이션 서비스 용도 (http/https) |



---

## 아코디언v2 인스톨러 구조 및 설정 방법

!!!!!!!!!구조사진 필요


### 설치 준비사항
- ssh key 생성, 복사, 접속 확인
- Ansible 설치 (아코디언 설치 패키지에 포함)
- /etc/hosts 파일 수정

### 아코디언 설치 설정
- accordion-installer/hosts 수정
- accordion-installer/group_vars/host.yml 수정

### 아코디언 설치 및 확인
- accordion-installer/install.sh
- accordion-installer/status.sh

## 설치 설정
```bash
$ accordion-installer/install.sh
```

## 설치 진행
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

## 설치 확인
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

## 아코디언 접속 URL

| URL      | ID    | PW    |
|:---------|:------|:------|
| https://VIP://30000      | admin  | accordion!@# |

![acc-ins-1.png](/assets/images/accordion/acc-ins-1.png)



## [실습]아코디언v2 인스톨(3H) - 멀티 클러스터 구성

## 트러블슈팅 