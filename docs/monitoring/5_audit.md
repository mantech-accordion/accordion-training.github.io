---
layout: default
title: 6-5. 감사 로그
nav_order: 1
parent: 6. 모니터링&알림
---

# 6-5. 감사 로그
{: .no_toc }

범위설정에서 설정한 간격으로 통계를 나타내며 개수와 총 개수를 나타내며 Node, Namespace, Pod, Container 의 이름과 로그를 제공한다.

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

| 항목  | 설명 |
|---|---|
| Time   | 날짜 (yyyy-mm-dd HH:mm:ss) |
| Namespace   | Namespace의 이름 |
| Verb   | get, list, create, update, patch, watch, delete 와 같은 리소스 요청에 사용하는 API 동사 |
| Status   | 작업상태를 의미하고 Success, Failure 둘중 한가지만 올수 있다. |
| Code   | HTTP 상태코드 |
| Pod Ip  | 요청이 시작된 소스 IP 및 중간 프록시 |
| User Name   | impersonatedUser의 이름 |
| Message   | 감사로그의 상세 설명 |


**검색 조건**

- namespace : namespace 이름

- resourceType : resource 타입

- resourceName : resource 이름

- userName : impersonatedUser의 이름

- verb : get, list, create, update, patch, watch, delete 와 같은 리소스 요청에 사용하는 API 동사

- statusCode : HTTP 상태코드