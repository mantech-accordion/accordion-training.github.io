---
layout: default
title: 12-4-1. 실습1.
nav_order: 1
parent: 12-4. 실습
grand_parent: 12. 설정
---

# 12-4-1. 실습1.
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

<div class="code-example" markdown="1">
Cluster
{: .label .label-blue }
</div>

---

## 실습1. 클러스터

---


### 1) 타입 : 노드(Node)

---

### 2) 타입 : 노드 셀렉터(Node Selector)

---

### 3) 타입 : 표현식(Expression)

1. 알림을 받고자 하는 클러스터 노드 선택
2. 설정 메뉴 선택
3. 알림 정책 선택
4. 알림 정책 생성
5. 알림 정책명: demo-alert 작성
6. 알림 규칙 추가
7. 알림 규칙명: test-disk-alert 작성
8. 타입을 Expresstion으로 지정 클러스터 node에 대한 CPU 사용량이 이상일 시 알림 수준을 critical 수준으로 메일 or 슬랙으로 알림 발송, 알림 발송 시간에 대한 설정은 알림 정책 고급옵션 활성화
EX) sum(rate(container_cpu_usage_seconds_total{container_name!="POD",namespace!=""}[5m])) by (node)

9⃣.발송 받을 슬랙 및 메일 추가,설정
1⃣0⃣. 처음 알림 오기까지 30초 대기(그룹 대기 시간) 후 3분 간격으로 반복 알림(그룹 반복 시간) 후 1시간 후에 다시 알림 발송(알림 반복 시간) 설정, 알림 발송 제한은 am 03 ~ am 08 시로 설정
1⃣1⃣. 알림 규칙 활성화
1⃣2⃣. 알림 규칙 설정 완료

![](/assets/images/setting/)

![](/assets/images/setting/)

위 같은 따라하기는 하나의 알림 규칙 만 생성 했기 때문에 여러 가지 알림 규칙을 생성 하려면 6⃣번 과정 부터 사용자가 원하는 노드에 임계치를 설정하여 알림을 받으면 된다.

**노드 관련 PromQL 리소스 메트릭 예시**

- Resource Metric: Kubernetes 컨테이너 CPU 사용량

```bash
container_cpu_usage_seconds_total
sum(rate(container_cpu_usage_seconds_total{container_name!="POD",namespace!=""}[5m])) by (node)
```

- Resource Metric: Kubernetes 네임스페이스 CPU 사용량

```bash
sum(rate(container_cpu_usage_seconds_total{container_name!="POD",namespace!=""}[5m])) by (namespace)
```

- Resource Metric: Kubernetes CPU 요청

```bash
sum(kube_pod_container_resource_requests_cpu_cores)
```

- Resource Metric: Kubernetes Pod CPU 요청

```bash
sum(kube_pod_container_resource_requests_cpu_cores) by (pod)
```

- Resource Metric: Kubernetes 네임스페이스 CPU 요청

```bash
sum(kube_pod_container_resource_requests_cpu_cores) by (namespace)
```

- Resource Metric: Kubernetes CPU 제한

```bash
sum(kube_pod_container_resource_limits_cpu_cores)
```

- Resource metric: Kubernetes 네임스페이스 CPU 제한

```bash
sum(kube_pod_container_resource_limits_cpu_cores) by (namespace)
```

- Resource Metric: Kubernetes 메모리 사용량

```bash
sum(kube_pod_container_resource_requests_memory_bytes)
```

- Resource Metric: Kubernetes 노드 메모리 사용량

```bash
sum(kube_pod_container_resource_requests_memory_bytes) by (node)
```

- Resource Metric: Kubernetes 메모리 요청

```bash
sum(kube_pod_container_resource_limits_memory_bytes)
```

- Resource Metric: Kubernetes 노드 메모리 요청

```bash
sum(kube_pod_container_resource_limits_memory_bytes) by (node)
```

- 클러스터 및 네임스페이스당 포드 수 확인

```bash
sum by (namespace) (kube_pod_info)
```

- CPU 제한이 없는 클러스터 및 네임스페이스별 컨테이너 수 확인

```bash
count by (namespace)(sum by (namespace,pod,container)(kube_pod_container_info{container!=""}) unless sum by (namespace,pod,container)(kube_pod_container_resource_limits{resource="cpu"}))

count by (node)(sum by (namespace,pod,container)(kube_pod_container_info{container!=""}) unless sum by (namespace,pod,container)(kube_pod_container_resource_limits{resource="cpu"}))
```

모든 종류의 문제가 있는 모든 Pod 확인

sum by (namespace) (kube_pod_status_ready{condition="false"})

CPU 오버 커밋

sum(kube_pod_container_resource_limits{resource="cpu"}) - sum(kube_node_status_capacity_cpu_cores)

메모리 오버 커밋 sum(kube_pod_container_resource_limits{resource="memory"}) - 

sum(kube_node_status_capacity_memory_bytes)

클러스터 별 준비된 노드 수

sum(kube_node_status_condition{condition="Ready", status="true"}==1) by (node)

클러스터 별 사용하지 않는 CPU core 확인

sum((rate(container_cpu_usage_seconds_total{container!="POD",container!=""}[30m]) - on (namespace,pod,container) group_left avg by (namespace,pod,container)(kube_pod_container_resource_requests{resource="cpu"})) * -1 >0 by (node))

클러스터 별 사용하지 않는 memory 확인

sum((container_memory_usage_bytes{container!="POD",container!=""} - on (namespace,pod,container) avg by (namespace,pod,container)(kube_pod_container_resource_requests{resource="memory"})) * -1 >0 ) / (102410241024)

Ready 상태가 아닌 node 확인

sum(kube_node_status_condition{condition="NotReady",status="true"})

클러스터 수준에서 CPU 사용량

sum (rate (container_cpu_usage_seconds_total{image!=""}[1m])) by (node)
