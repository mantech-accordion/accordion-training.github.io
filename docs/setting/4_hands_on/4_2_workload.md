---
layout: default
title: 12-4-2. 실습2.네임스페이스
nav_order: 1
parent: 12-4. 실습
grand_parent: 12. 설정
---

# 12-4-2. 실습2. 네임스페이스
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

<div class="code-example" markdown="1">
Namespace
{: .label .label-green }
</div>

---

## 실습2. 네임스페이스

---

### 1) 타입 : 워크로드(Workload)

1. 알림을 받고자 하는 클러스터 노드 선택
2. 알림 받기 위해 워크로드를 관리하고 있는 네임스페이스 선택
3. 설정 메뉴 선택
4. 알림 정책 선택
5. 알림 정책 생성
6. 알림 정책명: demo-alert-mem-workload 작성
7. 알림 규칙 추가
8. 알림 규칙명: demo-alert-mem-workload 작성
9. 타입을 Workload로 지정 Deployment의 demo에 대한 memory 사용률이 50% 이상일 시 알림 수준을 Warning 수준으로 메일 or 슬랙으로 알림 발송, 알림 발송 시간에 대한 설정은 알림 정책 고급옵션 비활성화로 알림 규칙에 대해 각각에 알림 설정 가능
10. 발송 받을 슬랙 및 메일 추가,설정
11. 처음 알림 오기까지 30초 대기(그룹 대기 시간) 후 3분 간격으로 반복 알림(그룹 반복 시간) 후 1시간 후에 다시 알림 발송(알림 반복 시간) 설정, 알림 발송 제한은 am 02 ~ am 08 시로 설정
12. 알림 규칙 활성화
13. 알림 규칙 설정 완료

![](/assets/images/setting/)
![](/assets/images/setting/)

💡 위 같은 따라하기는 하나의 알림 규칙 만 생성 했기 때문에 여러 가지 알림 규칙을 생성 하려면 6번 과정 부터 사용자가 원하는 노드에 임계치를 설정하여 알림을 받을 수 있습니다.

---

### 2) 타입 : 노드 셀렉터(Node Selector)

타입 Workload Selector 설정 전 사용자가 원하는 label를 설정

> 참고 : 현재 아코디언에서는 container `key=value`에 대한 list를 볼 수 없어 사용자가 직접 node, workload에 대한 `key=value` 값을 찾아서 기입

1. 알림을 받고자 하는 클러스터 노드 선택
2. 알림 받기 위해 워크로드를 관리하고 있는 네임스페이스 선택
3. 설정 메뉴 선택
4. 알림 정책 선택
5. 알림 정책 생성
6. 알림 정책 명: test-type-cpu-node-selector
7. 알림 규칙 명: test-type-cpu-node-selector
8. 타입: Node Selector
9. app=test 작성
10. Selector 추가 
11. test=label-add 작성
12. app=test 설정이 있는 deploy에서 memory 사용률이 70% 이상일 시 알림 수준을 Critical 수준으로 메일 or 슬랙으로 알림 발송, 알림 발송 시간에 대한 설정은 알림 정책 고급옵션 비활성화로 처음 알림 오기까지 30초 대기(그룹 대기 시간) 후 3분 간격으로 반복 알림(그룹 반복 시간) 후 1시간 후에 다시 알림 발송(알림 반복 시간) 설정, 알림 발송 제한은 am 02 ~ am 08 시로 설정
13. 발송 받을 슬랙 및 메일 추가,설정 후 알림 설정에 대한 활성화
14. 알림 정책 설정 완료

![](/assets/images/setting/)
![](/assets/images/setting/)


---

### 3) 타입 : 워크로드(Workload)

1. 알림을 받고자 하는 클러스터 노드 선택
2. 설정 메뉴 선택
3. 알림 정책 선택
4. 알림 정책 생성
5. 알림 정책명: demo-workload-heapused-alert 작성
6. 알림 규칙 추가
7. 알림 규칙명: demo-workload-heapused-alert 작성
8. 타입을 Expresstion으로 지정 클러스터 pod에 대한 heapused 사용량이 0 이상일 시 알림 수준을 critical 수준으로 메일 or 슬랙으로 알림 발송, 알림 발송 시간에 대한 설정은 알림 정책 고급옵션 활성화
EX) apm_HeapUsed{namespace="demo"}
9. 발송 받을 슬랙 및 메일 추가,설정
10. 처음 알림 오기까지 30초 대기(그룹 대기 시간) 후 3분 간격으로 반복 알림(그룹 반복 시간) 후 1시간 후에 다시 알림 발송(알림 반복 시간) 설정, 알림 발송 제한은 am 03 ~ am 08 시로 설정
11. 알림 규칙 활성화
12. 알림 규칙 설정 완료

![](/assets/images/setting/)

![](/assets/images/setting/)

---

**노드 관련 PromQL 리소스 메트릭 예시**

```bash
apm_ActiveService
```

```bash
apm_ElapsedTime
```

```bash
apm_GcCount
```

```bash
apm_GcTime
```

```bash
apm_ErrorRate
```

```bash
apm_HeapUsed
```

```bash
apm_PermUsed
```

```bash
apm_ServiceCount

```bash
apm_TPS
```

```bash
apm_RecentUser
```