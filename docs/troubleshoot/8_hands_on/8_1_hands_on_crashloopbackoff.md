---
layout: default
title: 8.1 CrashLoopBackOff
nav_order: 1
parent: 8. 실습
grand_parent: appendix. 트러블슈팅 가이드
---

# CrashLoopBackOff 트러블슈팅
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

## 실습 문제

**1. 아래 샘플 YAML을 배포하세요.**

<details>
<summary>샘플 Yaml</summary>
  
{% highlight yaml %}
---
kind: Deployment
apiVersion: apps/v1
metadata:
  name: practice-trb-1
  labels:
    app: practice-trb-1
spec:
  replicas: 1
  selector:
    matchLabels:
      app: practice-trb-1
  template:
    metadata:
      labels:
        app: practice-trb-1
    spec:
      volumes:
        - name: timezone
          hostPath:
            path: /etc/localtime
            type: ''
      containers:
        - name: apache
          image: docker.io/library/httpd:2.4
          resources: {}
          volumeMounts:
            - name: timezone
              readOnly: true
              mountPath: /etc/localtime

---
apiVersion: v1
kind: Service
metadata:
   name: practice-trb-1
spec:
  selector:
    app: practice-trb-1
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  type: ClusterIP
{% endhighlight %}
   
</details>


**2. 배포된 워크로드를 확인하고, 발생하는 이슈를 분석하여 Pod가 정상적으로 기동될 수 있게 적절하게 수정하세요.**


**3. 배포된 워크로드를 삭제하세요.**