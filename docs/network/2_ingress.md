---
layout: default
title: 8.2 인그레스
nav_order: 2
parent: 8. 네트워크
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

## 인그레스(Ingress)
인그레스는 클러스터 외부에서 클러스터 내부 서비스로 HTTP와 HTTPS 경로를 노출합니다. 트래픽 라우팅은 인그레스 리소스에 정의된 규칙에 의해 컨트롤됩니다.

**인그레스가 모든 트래픽을 하나의 서비스로 보내는 간단한 예시**

![ingress.png](/assets/images/network/ingress.png){: width="800" }

---

## 메뉴이동
`네트워크` ➡ `인그레스`

![network-002.png](/assets/images/network/network-002.png)

---

## 화면구성
생성된 인그레스 정보를 제공합니다.

![network-006.png](/assets/images/network/network-006.png){: width="1200" }

---

## 인그레스 생성
`+생성`을 클릭 후 내용을 입력하여 인그레스를 생성할 수 있다. 인그레스는 YAML로 입력할 수 있습니다.


![network-007.png](/assets/images/network/network-007.png){: width="800" }

---
## 인그레스 수정
인그레스 목록에서 특정 인그레스를 클릭하여 우측 YAML에 수정할 내용 입력 후 `수정`버튼을 클릭하면 수정할 수 있습니다.


---

## 인그레스 삭제
`삭제` 버튼 클릭 시 삭제 팝업창이 나타나며 삭제하려는 해당 네임스페이스/인그레스 명 입력 후 `Delete` 버튼 클릭 시 인그레스가 삭제됩니다.

![ingress-delete.png](/assets/images/network/ingress-delete.png){: width="1200" }

---

## 연습문제

**1. 예제 yaml을 참고하여 demo-apache를 배포하고, 아코디언 콘솔에서 다음 정보대로 인그레스를 생성하세요.**

```
- 이름 : lab-network-ingress-apache
- 인그레스 클래스명 : user-ingress-class
- 도메인 주소: 'demo-apache.example.com'
- 프로토콜 : HTTP
- 경로 : /
- 서비스 : demo-apache
- 포트 : 80
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
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
    nginx.ingress.kubernetes.io/use-regex: "true"
    nginx.ingress.kubernetes.io/affinity: cookie
spec:
  ingressClassName: user-ingress-class
  rules:
  - host: 'example.com'
    http:
      paths:
      - backend:
          service:
            name: app
            port:
              number: 80
        path: /
        pathType: Prefix
              
{% endhighlight %}
   
</details>

**2. 생성한 인그레스를 확인하고 삭제하세요.**