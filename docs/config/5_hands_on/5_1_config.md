---
layout: default
title: 7.5.1 구성 실습
nav_order: 1
parent: 7.5 실습
grand_parent: 7. 구성
---

# 구성 실습
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
## 실습문제

**1. 아래 속성으로 새 시크릿과 컨피그맵을 생성하고, 생성한 시크릿과 컨피그맵을 Pod에 사용하세요.**
- 단, 컨피그맵은 Pod에 볼륨 마운트하고, 시크릿은 Pod에 환경변수로 사용하세요.

- Pod

```
- Pod name: lab-config-demo-pod
  image name: proxy.accordions.co.kr/nginx:latest
```

- 시크릿

```
- 시크릿 이름: lab-config-demo-secret
- key1: player_initial_lives
  value1: "3"

- key2: ui_properties_file_name
  value2: "user-interface.properties"
```

- 컨피그맵

```
- 컨피그맵 이름: lab-config-demo-configmap

key: nginx.conf

value:
  user  nginx;
  worker_processes  auto;
  error_log  /var/log/nginx/error.log notice;
  pid        /var/run/nginx.pid;

  events {
      worker_connections  1024;
  }


  http {
      include       /etc/nginx/mime.types;
      default_type  application/octet-stream;

      log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                        '$status $body_bytes_sent "$http_referer" '
                        '"$http_user_agent" "$http_x_forwarded_for"';
      access_log  /var/log/nginx/access.log  main;
      sendfile        on;
      #tcp_nopush     on;
      keepalive_timeout  65;
      #gzip  on;
      include /etc/nginx/conf.d/*.conf;
  }
```

<details>
<summary>예제 Yaml</summary>

{% highlight yaml %}
---
apiVersion: v1
kind: Pod
metadata:
  name: lab-config-demo-pod
spec:
  containers:
    - name: nginx
      image: proxy.accordions.co.kr/nginx:latest
      env:
        - name: PLAYER_INITIAL_LIVES
          valueFrom:
            secretKeyRef:
              name: lab-config-demo-secret
              key: player_initial_lives
        - name: UI_PROPERTIES_FILE_NAME
          valueFrom:
            secretKeyRef:
              name: lab-config-demo-secret
              key: ui_properties_file_name
      volumeMounts:
      - name: config
        mountPath: "/config"
        readOnly: true
  volumes:
  - name: config
    configMap:
      name: lab-config-demo-configmap

{% endhighlight %}
</details>


**3. Pod에 터미널 접근하여 환경 변수 및 volumeMount한 설정 파일을 확인하세요.**


HINT
```
- 볼륨 마운트 확인 명령어: df -Th && ls -l /config

- 환경 변수 확인 명령어: env | egrep -i "ui_properties|player"
```

**4. 생성한 리소스들을 삭제하세요.**