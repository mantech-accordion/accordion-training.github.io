---
layout: default
title: 6.9.2 APM-based 오토스케일
nav_order: 2
parent: 6.9 실습
grand_parent: 6. 워크로드
---

# 실습
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

## 실습 문제

```
(required) 사전에 [실습] 아코디언 카탈로그 & 파이프라인이 선행되어야 합니다.
사전 수행해야하는 실습 자료 : https://training.accordions.co.kr/docs/application/5_hands_on/5_1_catalog_practice/
```

**1. 생성한 devsecops 디플로이먼트에 아래 설정대로 오토스케일을 설정합니다.**

```
- Min Pods: 2
  Max Pods: 4
  오토스케일 기준: APM TPS
  TPS: 5
```

**2. 생성한 HPA를 확인하세요.**

**3. 애플리케이션 모니터링(APM) 화면으로 전환하고, 부하 발생 후 오토스케일 되는지 확인합니다.**

**4. 생성한 HPA 리소스와 DevSecOps 카탈로그를 삭제합니다.**