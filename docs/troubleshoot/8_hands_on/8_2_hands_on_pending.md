---
layout: default
title: 8.2. Pending
nav_order: 2
parent: 8. 실습
grand_parent: appendix. 트러블슈팅 가이드
---

# Pending 트러블슈팅
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

## 실습 문제1

**1. 아래 샘플1 YAML을 배포하세요.**

<details>
<summary>샘플1 Yaml</summary>
  
{% highlight yaml %}
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: practice-trb-2-1
  labels:
    app: practice-trb-2-1
spec:
  replicas: 1
  selector:
    matchLabels:
      app: practice-trb-2-1
  template:
    metadata:
      labels:
        app: practice-trb-2-1
    spec:
      nodeSelector:
        accordion-role: "test"
      containers:
      - name: nginx
        image: base.registry.accordions.co.kr:5000/nginx:1.20.1-alpine

---
apiVersion: v1
kind: Service
metadata:
   name: practice-trb-2-1
spec:
  selector:
    app: practice-trb-2-1
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  type: ClusterIP
{% endhighlight %}
   
</details>


**2. 배포된 워크로드 상태를 확인하고, 발생하는 이슈를 분석하여 Pod가 정상적으로 기동될 수 있게 적절하게 수정하세요.**


**3. 배포된 워크로드를 삭제하세요.**


---

## 실습 문제2

**1. 아래 샘플2 YAML을 배포하고, 발생하는 이슈를 분석하여 Pod가 정상적으로 기동될 수 있게 적절하게 수정하세요.**

<details>
<summary>샘플2 Yaml</summary>
  
{% highlight yaml %}
---
kind: Deployment
apiVersion: apps/v1
metadata:
  name: practice-trb-2-2
  labels:
    app: practice-trb-2-2
spec:
  replicas: 1
  selector:
    matchLabels:
      app: practice-trb-2-2
  template:
    metadata:
      labels:
        app: practice-trb-2-2
    spec:
      volumes:
        - name: timezone
          hostPath:
            path: /etc/localtime
            type: ''
        - name: pending-vol
          persistentVolumeClaim:
            claimName: pending-vol
      containers:
        - name: apache
          image: base.registry.accordions.co.kr:5000/httpd-24-rhel7:2.4-146
          resources: {}
          volumeMounts:
            - name: timezone
              readOnly: true
              mountPath: /etc/localtime
            - name: pending-vol
              mountPath: /usr/local/apache2/htdocs

---
apiVersion: v1
kind: Service
metadata:
   name: practice-trb-2-2
spec:
  selector:
    app: practice-trb-2-2
  ports:
  - port: 8080
    protocol: TCP
    targetPort: 8080
  type: ClusterIP
{% endhighlight %}
   
</details>


**2. 배포된 워크로드의 상태를 확인하고, 발생하는 이슈를 분석하여 Pod가 정상적으로 기동될 수 있게 적절하게 수정하세요.**


**3. 배포된 워크로드를 삭제하세요.**