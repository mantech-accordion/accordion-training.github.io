---
layout: default
title: 2-4-1. 시스템 요구사항
nav_order: 4
parent: 2-4. Accordion 설치
grand_parent: 2. Accordion v2
---

# 2-4-1. 시스템 요구사항
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 시스템 요구사항
- Accordion 서버는 가상 시스템이나 물리 시스템에 설치가 가능합니다.
- Accordion 서버를 설치하기 위해서는 Master 서버 3대와 서비스를 수행 할 Node 서버 2대 이상 있어야 합니다.
- Master, Node 서버 간에는 네트워크가 가능해야 하고 인터넷이 가능해야 합니다.(인터넷이 불가한 상황인 경우 별도 설치파일을 다운로드 받아야 합니다.)
- Master 서버와 Node 서버 간에 ssh 접근이 가능해야 합니다. (root 접속필요)
- Master/Node 서버 시간은 동일해야 합니다.


**OS 운영체제**
- CentOS : 7.4 이상 (CentOS 8 미지원)
- RHEL : 7.4 또는 8.4 이상
- Ubuntu: 18.04 이상
- OracleLinux: 7.4 또는 8.4 이상
- RHCK 커널 지원, UEK 커널 미지원

**노드별 시스템 요구사항**

| 구분        | CPU | MEMORY | DISK |
|:-------------|:------------------|:------|:------|:------|
| Master       | 최소 8core | 최소 16GB  | 최소 500GB |
| Node(s)      | 최소 8core   | 최소 16GB | 최소 300GB |

**아코디언 사용 Port**

| 구분         | Port     | 용도 |
|:-------------|:---------|:------|
| Master       | 30000    | 아코디언 Web Admin |
| Node(s)      | 80/443   | 애플리케이션 서비스 용도 (http/https) |