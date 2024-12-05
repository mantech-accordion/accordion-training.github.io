---
layout: default
title: 5.5.2 카탈로그 실습2
nav_order: 2
parent: 5.5 실습
grand_parent: 5. 애플리케이션
---

# 카탈로그 
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

## 연습문제

**0. prod-service 네임스페이스를 생성하세요.**
- 아래 조건을 만족하도록 prod-service 네임스페이스에서 작업을 진행합니다.
    - APM 활성화

**1. 아래 내용으로 ConfigMap 생성하세요.**

```
- 컨피그맵 이름: catalog-usecase-conf

- key: context.xml
  value: < 아래 1. context.xml 내용 >
```

`1. context.xml`

```
<?xml version="1.0" encoding="UTF-8"?>
<!--
  Licensed to the Apache Software Foundation (ASF) under one or more
  contributor license agreements.  See the NOTICE file distributed with
  this work for additional information regarding copyright ownership.
  The ASF licenses this file to You under the Apache License, Version 2.0
  (the "License"); you may not use this file except in compliance with
  the License.  You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License.
-->
<!-- The contents of this file will be loaded for each web application -->
<Context>

    <WatchedResource>WEB-INF/web.xml</WatchedResource>
    <WatchedResource>WEB-INF/tomcat-web.xml</WatchedResource>
    <WatchedResource>${catalina.base}/conf/web.xml</WatchedResource>

</Context>
```

**2. 아래 카탈로그를 완성하고 워크로드를 배포하세요.**

일반설정
```
- 이름: catalog-usecase
- 카탈로그 템플릿: acc-tomcat
- 전체 옵션 보기 활성화
- 고급설정 : 배포 클러스터(host-cluster), 네임스페이스 선택
- 컨테이너 이미지 정책 : 레지스트리 user-registry, 보관개수 10
```

파이프라인 설정
```
1. vcs-get
- 테스크 이름: vcs-get
- 테스크 연관 관계: null
    - repo: https://github.com/mantech-accordion/jpetstore-6.git
    - ref: master
    - auth: none
    - cleanWorkspace: true
    - workspace: scm

2. src-build
- 테스크 이름: src-build
- 테스크 연관 관계: vcs-get.Succeeded
    - cmd: mvn clean package -f scm/pom.xml -Duser.timezone=GMT+09:00
    - mavenImage: base.registry.accordions.co.kr:5000/maven:jdk-8-alpine

3. dockerfile-tomcat
- 테스크 이름: dockerfile-tomcat
- 테스크 연관 관계: src-build.Succeeded
- baseImage: tomcat9-jdk8
- workspace: scm

4. 승인 단계 추가
- 테스크 이름: approve
  - 승인자 목록: approve
- 테스크 연관 관계: image-build.Succeeded
```

배포 리소스 설정
```
- 레플리카 파드 수 : 2

- 이미지풀정책: IfNotPresent

- 업데이트전략: RollingUpdate

- 환경변수
  - JAVA_OPTS에 Metaspace 관련 프로퍼티 추가
    ...
    -XX:MetaspaceSize=128M -XX:MaxMetaspaceSize=128M
    ...
- 리소스 설정
  - limits.memory: 2Gi
  - requests.memory: 2Gi

- 노드셀렉터
  - key: node-role.kubernetes.io/worker
    value: ""

- 토폴로지키: kubernetes.io/hostname 선택

- 볼륨
  - ConfigMap 볼륨 추가(context.xml)
    - name: context-xml
      from: configMap
        name: catalog-usecase-conf
        defaultMode: 0644
        items:
        - key: context.xml
          path: context.xml
        volumeMounts:
          mountPath: /usr/local/tomcat/conf/context.xml
          subPath: context.xml
        readOnly: true

  - PVC 볼륨 추가
    - name: log-vol
      from: persistentVolumeClaim
        - name: catalog-usecase-log-vol
          volumeMounts: 
            mountPath: /usr/local/tomcat/logs
            readOnly: false

- 프로브
  - type: readinessProbe
    action: httpGet
    scheme: HTTP
    host: 빈칸(Pod IP 자동 매핑)
    port: 8080
    path: /
    options:
    - periodSeconds: 5
      successThreshold: 2
      failureThreshold: 3
      initialDelaySeconds: 0
      timeoutSeconds: 1

- 서비스타입: ClusterIP
```

**3. 생성된 카탈로그의 배포를 실행하세요.**


**4. 배포된 워크로드 상태를 워크로드 대시보드에서 확인하세요.**


**5.1. 사전 작업으로 kube-system 네임스페이스에 있는 wildcard-certs 시크릿을 복사하세요.**

- [네임스페이스 이동(kube-system)] - [구성] - [시크릿] - wildcard-certs 선택 후 복제 클릭
    - 네임스페이스: prod-service
    - 이름: wildcard-certs-copy


**5.2. 아코디언에서 다음 정보대로 인그레스를 생성하세요.**

```
- 이름: usecase-ing

- 인그레스 클래스명: nginx

- 어노테이션
    - key: nginx.ingress.kubernetes.io/affinity
      value: cookie
    - key: nginx.ingress.kubernetes.io/session-cookie-hash
      value: sha1
    - key: nginx.ingress.kubernetes.io/session-cookie-name
      value: route
    - key: nginx.ingress.kubernetes.io/use-regex
      value: "true"

- 도메인 주소: 'usecase.nip.io'

- 프로토콜: HTTPS

- 시크릿: wildcard-certs-copy

- 경로: /

- 서비스: catalog-usecase

- 포트: 8080/TCP
```

**6. /etc/hosts(linux인 경우) 혹은 window hosts 파일에 아래 내용 등록 후 usecase.nip.io를 저장한 뒤, 생성한 인그레스에 접속해보세요.**

```
...
<IP>  usecase.nip.io
```