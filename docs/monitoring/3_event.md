---
layout: default
title: 6-3. 이벤트 로그
nav_order: 1
parent: 6. 모니터링&알림
---

# 6-3. 이벤트 로그
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

<div class="code-example" markdown="1">
Cluster
{: .label .label-blue }

Namespace
{: .label .label-green }
</div>

## 이벤트 로그
cluster 내의 이벤트 로그를 제공한다. 범위설정에서 설정한 간격으로 통계를 나타내며 개수와 총 개수를 나타내며 Time, Namespace, Name, Count, Kind, Type, Reason, Message 를 제공한다.

| 항목  | 설명 |
|---|---|
| Time   | 날짜 (yyyy-mm-dd HH:mm:ss) |
| Namespace  | Namespace의 이름 |
| Name   | Pod의 이름  |
| Count   | Event의 횟수  |
| Kind   | 리소스의 종류  |
| Type   | Event의 유형  |
| Reason   | 해당 상태에 있는 이유  |
| Message   | 마지막 상태 전환에 대한 세부 정보  |

---

**검색 조건**

검색조건은 아래와 같이 총 6가지에 해당한다.

- namespace
- name
- kind
- type
- reason
- message

**새로고침 주기**

- 새로고침 주기는 초단위(5,10,15)로 설정할 수 있으며 원하는 주기를 선택하면 새로고침 주기가 적용된다.
- 새로고침 주기 설정 좌측 버튼을 클릭하면 즉시 새로고침 된다.

**검색 입력 방법**