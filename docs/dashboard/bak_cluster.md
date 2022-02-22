---
layout: default
title: 3-0. 백업
nav_order: 1
parent: 3. 대시보드
---

# 3-0. 백업
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

<div class="code-example" markdown="1">
Global
{: .label .label-purple }
</div>

## 클러스터
클러스터란 컨테이너화된 애플리케이션을 실행하기 위한 노드의 집합을 의미한다. 컨테이너화된 애플리케이션은 개별 노드에 얽매이지 않고 클러스터에 배포된다.
클러스터는 Host 클러스터 및 하나 이상의 Member 클러스터를 가지며 싱글 클러스터인 경우 Host와 Member 클러스터 역할을 가진다.

클러스터 메뉴에서는 Host Cluster는 하나만 등록이 가능하여 Member Cluster만 관리할 수 있다.

**클러스터 목록**
![3_cluster_overview.png](/assets/images/dashboard/cluster/3_cluster_overview.png)

- 항목별 상세설명

| 항목 | 클러스터 이름 |
|:--:|--|
|Cluster Name|클러스터 이름|
|Provider|Kubernetes Cloud Provider|
|Master Nodes|마스터노드 개수|
|Worker Nodes|워커노드 개수|
|Description|클러스터 설명|
|Namespaces|클러스터에 생성되어있는 namespace 개수|
|Pods|클러스터에 생성되어있는 pods 개수|
|Version|클러스터 버전|
|Created|클러스터 생성시각|
|Phase|클러스터 상태|
|Cores|클러스터 코어 사이즈|
|Memory|클러스터 메모리 사이즈|
|Disk|클러스터 디스크 사이즈|

- Member Cluster 수정/삭제 항목 설명

|분류|설명|
|:--:|--|
|수정|등록한 Member Cluster의 정보를 수정할 수 있다.|
|삭제|Member Cluster를 삭제할 수 있다.|

**Member Cluster 수정**

Cluster 목록에서 등록된 Member Cluster의 [수정]]을 클릭하면 수정 화면으로 이동된다.

- Member Cluster 수정 항목

|분류|설명|
|:--:|--|
|Name|Cluster Name을 입력한다|
|Server|Cluster Server 주소|
|Provider|None,Accordion,EKS,AKS,GKE,VMWawre,Nutanix 등|
|Role|Member만 선택할 수 있다|
|Proxy CA certificate|Kubernetes TLS 인증을 위한 CA 인증서|
|Description|등록할 cluster에 대한 설명을 입력한다|


![3_cluster_member_edit.png](/assets/images/dashboard/cluster/3_cluster_member_edit.png)

**Member Cluster 삭제**

![3_cluster_member_delete.png](/assets/images/dashboard/cluster/3_cluster_member_delete.png)

Cluster 목록에서 등록된 Member Cluster의 [삭제]를 클릭하면 삭제 팝업이 나타난다.

---

## 헬름

## 계정