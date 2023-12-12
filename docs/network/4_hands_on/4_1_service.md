---
layout: default
title: 8.4.1 Service 실습
nav_order: 1
parent: 8.4 실습
grand_parent: 8. 네트워크
---

# 서비스
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
## 실습 문제


<details>
<summary>예제1 Yaml</summary>
  
{% highlight yaml %}

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo-success-apache
  labels:
    app: demo-success-apache
spec:
  replicas: 1
  selector:
    matchLabels:
      app: demo-success-apache
  template:
    metadata:
      labels:
        app: demo-success-apache
    spec:
      containers:
      - name: apache
        image: base.registry.accordions.co.kr:5000/httpd-24-rhel7:2.4-146

---
apiVersion: v1
kind: Service
metadata:
   name: demo-success-apache
spec:
  selector:
    app: demo-success-apache
  ports:
  - name: tcp
    port: 8080
    protocol: TCP
    targetPort: 8080
  type: NodePort

{% endhighlight %}
   
</details>

<details>
<summary>예제2 Yaml</summary>
  
{% highlight yaml %}

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo-failed-apache
  labels:
    app: demo-failed-apache
spec:
  replicas: 1
  selector:
    matchLabels:
      app: demo-failed-apache
  template:
    metadata:
      labels:
        app: demo-failed-apache
    spec:
      containers:
      - name: apache
        image: base.registry.accordions.co.kr:5000/httpd-24-rhel7:2.4-146

---
apiVersion: v1
kind: Service
metadata:
   name: demo-failed-apache
spec:
  selector:
    app: wrong-label-apache
  ports:
  - name: tcp
    port: 8080
    protocol: TCP
    targetPort: 8080
  type: NodePort

{% endhighlight %}
   
</details>


**1. 예제1 yaml을 사용하여 Deployment 및 Service를 생성하세요.**

**2. 생성한 서비스를 NodePort로 접근하여 확인하세요.**

```
URL=> http://<IP>:<NodePort>
IP = 강사가 부여해주는 IP로 접근하세요
```

**3. 예제2 yaml을 사용하여 Deployment 및 Service를 생성하세요.**

**4. 생성한 서비스를 NodePort로 접근하여 확인하세요.**

```
URL=> http://<IP>:<NodePort>
IP = 강사가 부여해주는 IP로 접근하세요
```

**5. 접근이 되지 않는 서비스를 찾고, 그 이유를 확인하세요.**

**6. 생성한 deployment 및 Service를 모두 삭제하세요.**