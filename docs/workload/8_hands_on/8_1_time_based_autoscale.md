---
layout: default
title: 6.8.1 Time-based 오토스케일
nav_order: 1
parent: 6.8 실습
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

**1. 아래 예제YAML을 참고하여 아래 속성으로 새 디플로이먼트를 만드세요.**

```
- name: workload-lab-tb-autoscale
  replicas: 2
  image: nginx:latest
```

<details>
<summary>예제 Yaml</summary>
  
{% highlight yaml %}
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.20-alpine
        ports:
        - containerPort: 80

{% endhighlight %}
   
</details>

**2. 생성한 디플로이먼트에 Time-based 오토스케일(CronHPA)을 설정하세요.**

```
- [워크로드] -> [디플로이먼트]
- "오토스케일" 버튼
- 현재 시간 +2분 뒤에 오토스케일이 수행될 수 있도록 설정
(TIP: 초 / 분 / 시 / 일 / 월 / 요일)

ex) 현재 시간 = 16시 20분일 경우 -> * 22 16 * * *
```

**3. 생성한 CronHPA와 디플로이먼트를 삭제하세요.**