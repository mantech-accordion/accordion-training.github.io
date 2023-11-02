---
layout: default
title: 6.3 레플리카셋
nav_order: 3
parent: 6. 워크로드
---

# 레플리카셋
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

## 레플리카셋(ReplicaSet)
레플리카셋(ReplicaSet)는 Kuberenetes에서 주로 사용되는 오브젝트입니다. 
레플리카셋을 정의하는 필드는 획득 가능한 파드를 식별하는 방법이 명시된 셀렉터, 유지해야 하는 파드 개수를 명시하는 레플리카의 개수, 그리고 레플리카 수 유지를 위해 생성하는 신규 파드에 대한 데이터를 명시하는 파드 템플릿을 포함합니다. 그러면 레플리카셋은 필드에 지정된 설정을 충족하기 위해 필요한 만큼 파드를 만들고 삭제합니다.

레플리카셋은 셀렉터를 이용해서 필요한 새 파드를 식별한다. 만약 파드에 OwnerReference가 없거나, OwnerReference가 컨트롤러(Controller)가 아니고 레플리카셋의 셀렉터와 일치한다면 레플리카셋이 즉각 파드를 가지게 됩니다.
레플리카셋은 보통 명시된 동일 파드 개수에 대한 가용성을 보증하는데 사용합니다.

---
## 메뉴이동
`워크로드` ➡ `레플리카셋`

![rs-001.png](/assets/images/workload/rs-001.png)

---

## 화면구성
배포된 디플로이먼트 정보를 제공합니다.

![rs-002.png](/assets/images/workload/rs-002.png){: width="1200" }

---

## 레플리카셋 생성
`+생성` 을 선택하면 나타나는 모달에서 레플리카셋 리소스 정보를 YAML 형태로 입력하여 생성할 수 있습니다.

![rs-003.png](/assets/images/workload/rs-003.png){: width="1200" }

---

## 레플리카셋 삭제
삭제하려는 레플리카셋을 선택하고 우측의 삭제 버튼을 선택합니다.

![rs-004.png](/assets/images/workload/rs-004.png){: width="1200" }

---

## 연습문제

**1. 아래 예제YAML을 참고하여 아래 속성으로 새 레플리카셋을 만드세요.**

```
- name: lab-workload-rs-httpd
  replicas: 3
  image: base.registry.accordions.co.kr:5000/httpd-24-rhel7:2.4-146
```

<details>
<summary>예제 Yaml</summary>
  
{% highlight yaml %}
---
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: frontend
  labels:
    app: guestbook
    tier: frontend
spec:
  replicas: 3
  selector:
    matchLabels:
      tier: frontend
  template:
    metadata:
      labels:
        tier: frontend
    spec:
      containers:
      - name: php-redis
        image: base.registry.accordions.co.kr:5000/httpd-24-rhel7:2.4-146

{% endhighlight %}
   
</details>

**2. 생성한 레플리카셋을 확인하세요.**

**3. 생성한 레플리카셋을 삭제하세요.**