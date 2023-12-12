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
        image: base.registry.accordions.co.kr:5000/busybox:1.28
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
      containers:
      - env:
        - name: JAVA_OPTS
          value: -XX:+UseParallelGC -XX:+UseParallelOldGC -XX:+PrintGCDetails -XX:+HeapDumpOnOutOfMemoryError
            -XX:HeapDumpPath=$CATALINA_HOME/logs/$HOSTNAME/heapdump -verbose:gc -Xloggc:$CATALINA_HOME/logs/$HOSTNAME/gclog/gc-%t.log
            -Djava.security.egd=file:/dev/./urandom -Duser.timezone=GMT+09:00 -Dcatalina.host=$HOSTNAME
            -Dcatalina.logdir=$CATALINA_HOME/logs/$HOSTNAME -Xms1024m -Xmx1024m -Catalina
        image: base.registry.accordions.co.kr:5000/accordion/tomcat:9-jdk8
        imagePullPolicy: Always
        lifecycle:
          preStop:
            exec:
              command:
              - /usr/local/tomcat/bin/shutdown.sh
        name: tomcat
        ports:
        - containerPort: 8080
          name: http-port
          protocol: TCP
        resources:
          limits:
            cpu: "0"
            memory: "0"
          requests:
            cpu: "0"
            memory: "0"
        volumeMounts:
        - mountPath: /etc/localtime
          name: localtime
          readOnly: true
      dnsPolicy: ClusterFirst
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


**2. 배포된 워크로드를 확인하고, 발생하는 이슈를 분석하여 Pod가 정상적으로 기동될 수 있게 적절하게 수정하세요.**


**3. 배포된 워크로드를 삭제하세요.**