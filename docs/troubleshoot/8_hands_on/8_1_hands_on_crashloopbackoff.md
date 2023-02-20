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

## 실습 문제1

**1. 아래 샘플1 YAML을 배포하세요.**

<details>
<summary>샘플1 Yaml</summary>
  
{% highlight yaml %}
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: practice-trb-1-1
spec:
  replicas: 1
  selector:
    matchLabels:
      app: practice-trb-1-1
  template:
    metadata:
      labels:
        app: practice-trb-1-1
    spec:
      volumes:
      - name: logs
        emptyDir: {}
      initContainers:
      - name: init
        image: bash:5.0.11
        command: ['bash','-c','echo init > /var/log/cleaner/cleaner.log']
        volumeMounts:
        - name: logs
          mountPath: /var/log/cleaner
      containers:
      - name: cleaner-con
        image: bash:5.0.11
        args: ['bash','-c','while true; do echo `date`: "remove random file" >> /var/log/cleaner/cleaner.log; sleep 1; done']
        volumeMounts:
        - name: logs
          mountPath: /var/log/cleaner
      - name: logger-con
        image: busybox:1.31.0
        command: ["sh","-c","tail -f /var/log/cleaner/cleaner"]
        volumeMounts:
        - name: logs
          mountPath: /var/log/cleaner
{% endhighlight %}
   
</details>


**2. 배포된 워크로드를 확인하고, 발생하는 이슈를 분석하여 Pod가 정상적으로 기동될 수 있게 적절하게 수정하세요.**


**3. 배포된 워크로드를 삭제하세요.**

---

## 실습 문제2

**1. 아래 샘플2 YAML을 배포하세요.**

<details>
<summary>샘플2 Yaml</summary>
  
{% highlight yaml %}
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: practice-trb-1-2
spec:
  replicas: 1
  selector:
    matchLabels:
      app: practice-trb-1-2
  template:
    metadata:
      labels:
        app: practice-trb-1-2
    spec:
      volumes:
      - name: logs
        emptyDir: {}
      initContainers:
      - name: init
        image: bash:5.0.11
        command: ['bash','-c','echo init > /var/log/cleaner/cleaner.log']
        volumeMounts:
        - name: logs
          mountPath: /var/log/cleaner
      containers:
      - name: cleaner-con
        image: bash:5.0.11
        args: ['bash','-c','while true; do echo `date`: "remove random file" >> /var/log/cleaner/cleaner.log; sleep 1; done']
        volumeMounts:
        - name: logs
          mountPath: /var/log/cleaner
      - name: logger-con
        image: busybox:1.31.0
        command: ["sh","-c","tail -f /var/log/cleaner/cleaner"]
        volumeMounts:
        - name: logs
          mountPath: /var/log/cleaner
{% endhighlight %}
   
</details>


**2. 배포된 워크로드를 확인하고, 발생하는 이슈를 분석하여 Pod가 정상적으로 기동될 수 있게 적절하게 수정하세요.**


**3. 배포된 워크로드를 삭제하세요.**