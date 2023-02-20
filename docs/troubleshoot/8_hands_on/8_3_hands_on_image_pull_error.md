---
layout: default
title: 8.3. ImagePullBackOff & ErrImagePull
nav_order: 3
parent: 8. 실습
grand_parent: appendix. 트러블슈팅 가이드
---

# ImagePullError & ErrImagePull
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

<div class="code-example" markdown="1">
Cluster
{: .label .label-green }
</div>

## 실습 문제

**1. 아래 샘플 YAML을 배포하세요.**

<details>
<summary>샘플 Yaml</summary>
  
{% highlight yaml %}
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: practice-trb-3
  labels:
    app: practice-trb-3
spec:
  replicas: 1
  selector:
    matchLabels:
      app: practice-trb-3
  template:
    metadata:
      labels:
        app: practice-trb-3
    spec:
      nodeSelector:
        accordion-role: "test"
      containers:
      - name: nginx
        image: localhost/nginx:latest

---
apiVersion: v1
kind: Service
metadata:
   name: practice-trb-3
spec:
  selector:
    app: practice-trb-3
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  type: ClusterIP
{% endhighlight %}
   
</details>


**2. 배포된 워크로드 상태를 확인하고, 발생하는 이슈를 분석하여 Pod가 정상적으로 기동될 수 있게 적절하게 수정하세요.**


**3. 배포된 워크로드를 삭제하세요.**