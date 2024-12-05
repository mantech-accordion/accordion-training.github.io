---
layout: default
title: 6.9.2 APM-based 오토스케일
nav_order: 2
parent: 6.9 실습
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

```
(required) 사전에 [실습] 아코디언 카탈로그 & 파이프라인이 선행되어야 합니다.
사전 수행해야하는 실습 자료 : https://training.accordions.co.kr/docs/application/5_hands_on/5_2_practice2/
```

**1. 생성한 catalog-usecase 디플로이먼트에 아래 설정대로 오토스케일을 설정합니다.**

```
- Min Pods: 2
  Max Pods: 4
  오토스케일 기준: TPS
  TPS: 5
```

**2. 생성한 HPA를 확인하세요.**


**3. 아래 예제 YAML을 토대로 부하 발생기 deployment를 배포한 뒤, 애플리케이션 모니터링(APM) 화면으로 전환하여 모니터링 합니다.**


<details>
<summary>예제 Yaml</summary>
  
{% highlight yaml %}
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: stress-tool
  namespace: default
spec:
  progressDeadlineSeconds: 600
  replicas: 1
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: stress-tool
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: stress-tool
    spec:
      containers:
      - args:
        - |
          while :
          do
            curl -v http://catalog-usecase.prod-service.svc.cluster.local:8080/index.jsp;
            curl -v http://catalog-usecase.prod-service.svc.cluster.local:8080/session.jsp;
            sleep 0.4;
          done
        command:
        - sh
        - -c
        image: docker.io/curlimages/curl:7.76.1
        imagePullPolicy: Always
        name: stress1
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
        volumeMounts:
        - mountPath: /etc/localtime
          name: localtime
          readOnly: true
      - args:
        - |
          while :
          do
            curl -v http://catalog-usecase.prod-service.svc.cluster.local:8080/index.jsp;
            curl -v http://catalog-usecase.prod-service.svc.cluster.local:8080/session.jsp;
            sleep 0.4;
          done
        command:
        - sh
        - -c
        image: docker.io/curlimages/curl:7.76.1
        imagePullPolicy: Always
        name: stress2
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
        volumeMounts:
        - mountPath: /etc/localtime
          name: localtime
          readOnly: true
      - args:
        - |
          while :
          do
            curl -v http://catalog-usecase.prod-service.svc.cluster.local:8080/e2e.jsp;
            sleep 5;
          done
        command:
        - sh
        - -c
        image: docker.io/curlimages/curl:7.76.1
        imagePullPolicy: Always
        name: stress3
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
        volumeMounts:
        - mountPath: /etc/localtime
          name: localtime
          readOnly: true
      dnsPolicy: ClusterFirst
      imagePullSecrets:
      - name: user-registry
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
      volumes:
      - hostPath:
          path: /etc/localtime
          type: ""
        name: localtime

{% endhighlight %}
   
</details>


**4. 부하 발생 후 오토스케일 되는지 확인합니다.**


**5. 생성한 HPA 리소스와 catalog-usecase 카탈로그를 삭제합니다.**