---
layout: default
title: 8.1 서비스
nav_order: 1
parent: 8. 네트워크
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

## 서비스(Service)
파드 집합에서 실행중인 애플리케이션을 네트워크 서비스로 노출하는 추상화 방법입니다.

Kubernetes를 사용하면 익숙하지 않은 서비스 디스커버리 메커니즘을 사용하기 위해 애플리케이션을 수정할 필요가 없습니다. Kubernetes는 파드에게 고유한 IP 주소와 파드 집합에 대한 단일 DNS 명을 부여하고, 그것들 간에 로드밸런스를 수행할 수 있습니다.

![k8s_svc_diagram.png](/assets/images/network/k8s_svc_diagram.png){: width="800" }

---

## 메뉴이동
`네트워크` ➡ `서비스`

![network-001.png](/assets/images/network/network-001.png)

---

## 화면구성
생성된 서비스 정보를 제공합니다.

![network-004.png](/assets/images/network/network-004.png){: width="1200" }

---

## 서비스 생성
`+생성`을 클릭 후 내용을 입력하여 서비스를 생성할 수 있습니다. 서비스는 FORM/YAML로 입력할 수 있습니다.

![network-005.png](/assets/images/network/network-005.png){: width="800" }

**서비스 필수 요구값**

- Name
- Namespace
- Selector(key,value)
- ServiceType
  + ClusterIP
  + NodePort
  + LoadBalancer
- ClusterIP
  + PortName
  + Port
  + Protocotol(TCP,UDP)
  + Target Port

---

## 서비스 수정
서비스 목록에서 특정 서비스를 클릭하여 우측 YAML에 수정할 내용 입력 후 `수정`버튼을 클릭하면 수정할 수 있다.

---

## 서비스 삭제
`삭제` 버튼 클릭 시 삭제 팝업창이 나타나며 삭제하려는 해당 네임스페이스/서비스 명 입력 후 `Delete` 버튼 클릭 시 서비스가 삭제된다.

![service-delete.png](/assets/images/network/service-delete.png){: width="1200" }

---

## 연습문제

**1. 예제1 yaml을 참고하여 아래 내용에 맞는 Deployment 및 Service를 생성하세요.**

```
- 디플로이먼트
  name: lab-network-svc-apache
  image: base.registry.accordions.co.kr:5000/httpd-24-rhel7:2.4-146
  replicas: 1

- 서비스
  name: lab-network-svc-apache
  port: 80
  target port: 80
  type: ClusterIP
  protocol: TCP
```

<details>
<summary>예제Yaml</summary>
  
{% highlight yaml %}
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: apache
  labels:
    app: apache
spec:
  replicas: 1
  selector:
    matchLabels:
      app: apache
  template:
    metadata:
      labels:
        app: apache
    spec:
      containers:
      - name: apache
        image: base.registry.accordions.co.kr:5000/httpd-24-rhel7:2.4-146

---
apiVersion: v1
kind: Service
metadata:
   name: apache
spec:
  selector:
    app: apache
  ports:
  - port: 8888
    protocol: TCP
    targetPort: 8087
  type: ClusterIP

{% endhighlight %}
   
</details>

**2. 생성한 서비스를 NodePort로 접근하여 확인하세요.**

**3. 생성한 deployment 및 Service를 모두 삭제하세요.**