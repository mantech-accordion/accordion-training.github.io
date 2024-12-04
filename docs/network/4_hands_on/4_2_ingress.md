---
layout: default
title: 8.4.2 ingress 실습
nav_order: 2
parent: 8.4 실습
grand_parent: 8. 네트워크
---

# 인그레스
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

**1. 예제 yaml을 참고하여 demo-apache를 배포하고, 아코디언 콘솔에서 다음 정보대로 인그레스를 생성하세요.**

```
- 이름 : demo-ingress
- 인그레스 클래스명 : nginx
- 도메인 주소: '*.nip.io'
- 프로토콜 : HTTP
- 경로 : /
- 서비스 : demo-apache, demo-nginx
- 포트 : 80/TCP, 80/TCP
```

<details>
<summary>예제 Yaml</summary>

{% highlight yaml %}
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo-apache
  labels:
    app: demo-apache
spec:
  replicas: 1
  selector:
    matchLabels:
      app: demo-apache
  template:
    metadata:
      labels:
        app: demo-apache
    spec:
      containers:
      - name: apache
        image: base.registry.accordions.co.kr:5000/httpd-24-rhel7:2.4-146

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo-nginx
  labels:
    app: demo-nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: demo-nginx
  template:
    metadata:
      labels:
        app: demo-nginx
    spec:
      containers:
      - name: nginx
        image: base.registry.accordions.co.kr:5000/nginx:1.20.1-alpine

---
apiVersion: v1
kind: Service
metadata:
   name: demo-apache
spec:
  selector:
    app: demo-apache
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  type: ClusterIP

---
apiVersion: v1
kind: Service
metadata:
   name: demo-nginx
spec:
  selector:
    app: demo-nginx
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  type: ClusterIP

---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: demo-ingress
  annotations:
    nginx.ingress.kubernetes.io/use-regex: "true"
    nginx.ingress.kubernetes.io/affinity: cookie
spec:
  ingressClassName: nginx
  rules:
  - host: 'demo-apache.nip.io'
    http:
      paths:
      - backend:
          service:
            name: demo-apache
            port:
              number: 80
        path: /
        pathType: Prefix
  - host: 'demo-nginx.nip.io'
    http:
      paths:
      - backend:
          service:
            name: demo-nginx
            port:
              number: 80
        path: /
        pathType: Prefix

              
{% endhighlight %}
   
</details>

**2. 각자 PC의 hosts 파일에 아코디언 접속 IP로 demo-apache.nip.io를 저장한 뒤, 생성한 인그레스에 접속해보세요.**

**3. 각자 PC의 hosts 파일에 아코디언 접속 IP로 demo-nginx.nip.io를 저장한 뒤, 생성한 인그레스에 접속해보세요.**

**4. 생성한 인그레스에 ingressClassName을 test로 변경한 후, demo-apache.nip.io에 접속해보세요.**

**5. 생성한 인그레스를 확인하고 삭제하세요.**