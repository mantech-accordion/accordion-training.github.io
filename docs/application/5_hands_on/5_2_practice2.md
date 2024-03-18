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

**0. 네임스페이스를 `tool`로 이동하세요.**
- 아래 조건을 만족하도록 tool 네임스페이스에서 작업을 진행합니다.

**1. 아래 내용으로 ConfigMap 생성하세요.**

```
- 컨피그맵 이름: egov-conf

- key: server.xml
  value: < 아래 1. server.xml 내용 >

- key: context.xml
  value: < 아래 2. context.xml 내용 >
```

`1. server.xml`
```
<?xml version="1.0" encoding="UTF-8"?>
<Server port="8005" shutdown="SHUTDOWN">
  <Listener className="org.apache.catalina.startup.VersionLoggerListener" />
  <!-- Security listener. Documentation at /docs/config/listeners.html
  <Listener className="org.apache.catalina.security.SecurityListener" />
  -->
  <!-- APR library loader. Documentation at /docs/apr.html -->
  <Listener className="org.apache.catalina.core.AprLifecycleListener" SSLEngine="on" />
  <!-- Prevent memory leaks due to use of particular java/javax APIs-->
  <Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener" />
  <Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener" />
  <Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener" />

  <GlobalNamingResources>
    <Resource name="UserDatabase" auth="Container"
              type="org.apache.catalina.UserDatabase"
              description="User database that can be updated and saved"
              factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
              pathname="conf/tomcat-users.xml" />
  </GlobalNamingResources>

  <Service name="Catalina">
    <!--
    <Executor name="tomcatThreadPool" namePrefix="catalina-exec-"
        maxThreads="${env.MAX_THREADS:200}" minSpareThreads="${env.MIN_THREADS:4}"/>
    -->
    <Connector port="8080" protocol="${tomcat.connector}"
               connectionTimeout="20000"
               redirectPort="8443"
               maxParameterCount="1000"
               />
    <!-- A "Connector" using the shared thread pool-->
    <!--
    <Connector executor="tomcatThreadPool"
               port="8080" protocol="${tomcat.connector}"
               connectionTimeout="20000"
               redirectPort="8443"
               maxParameterCount="1000"
               />
    -->
    <!-- Define an AJP 1.3 Connector on port 8009 -->
    <!--
    <Connector protocol="AJP/1.3"
               address="::1"
               port="8009"
               redirectPort="8443"
               maxParameterCount="1000"
               />
    -->

    <Engine name="Catalina" defaultHost="localhost">
      <!--
      <Cluster className="org.apache.catalina.ha.tcp.SimpleTcpCluster"/>
      -->
      <Realm className="org.apache.catalina.realm.LockOutRealm">
        <!-- This Realm uses the UserDatabase configured in the global JNDI
             resources under the key "UserDatabase".  Any edits
             that are performed against this UserDatabase are immediately
             available for use by the Realm.  -->
        <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
               resourceName="UserDatabase"/>
      </Realm>

      <Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">
        <!--
        <Valve className="org.apache.catalina.authenticator.SingleSignOn" />
        -->
        <Valve className="org.apache.catalina.valves.AccessLogValve" directory="${catalina.logdir}"
               prefix="localhost_access_log" suffix=".txt"
               pattern="%{X-Forwarded-For}i %h %l %u %t &quot;%r&quot; %s %b %{User-Agent}i %F " />
      </Host>
    </Engine>
  </Service>
</Server>
```

`2. context.xml`

```
<?xml version="1.0" encoding="UTF-8"?>

<Context>
    <WatchedResource>WEB-INF/web.xml</WatchedResource>
    <WatchedResource>WEB-INF/tomcat-web.xml</WatchedResource>
    <WatchedResource>${catalina.base}/conf/web.xml</WatchedResource>
</Context>
```

**2. WAR 업로드 방식으로 카탈로그를 완성하고 워크로드를 배포하세요.**

일반설정
```
- 이름: egov
- 카탈로그 템플릿: acc-tomcat
- 전체 옵션 보기 활성화
- 고급설정 : 배포 클러스터(host-cluster), 네임스페이스 선택
- 컨테이너 이미지 정책 : 레지스트리 user-registry, 보관개수 10
```

파이프라인 설정
```
1. upload 테스크 추가
- 테스크 이름: war-upload
- 테스크 연관 관계 : null
- 다른 테스크 템플릿 불러오기 -> 아티팩트 -> 업로드
- 업로드된 파일 목록 : egovframework-all-in-one-war

2. vcs-get 테스크 삭제

3. src-build 테스크 삭제

4. dockerfile-tomcat 테스크 연관 관계 수정
- 테스크 연관 관계 : war-upload.Succeeded
- baseImage: tomcat9-jdk8
- workspace: ./
```

배포 리소스 설정
```
- 레플리카 파드 수 : 1

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
  - ConfigMap 볼륨 추가(server.xml)
    - name: server-xml
      from: configMap
        name: egov-conf
        defaultMode: 0644
        items:
        - key: server.xml
          path: server.xml
      volumeMounts:
        mountPath: /usr/local/tomcat/conf/server.xml
        subPath: server.xml
        readOnly: true

  - ConfigMap 볼륨 추가(context.xml)
    - name: context-xml
      from: configMap
        name: egov-conf
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
        - name: edu-pvc-10g
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

**5. 아코디언에서 다음 정보대로 인그레스를 생성하세요.**

```
- 이름 : egov-ing

- 인그레스 클래스명 : nginx

- 어노테이션
    - key: nginx.ingress.kubernetes.io/affinity
      value: cookie
    - key: nginx.ingress.kubernetes.io/session-cookie-hash
      value: sha1
    - key: nginx.ingress.kubernetes.io/session-cookie-name
      value: route
    - key: nginx.ingress.kubernetes.io/use-regex
      value: "true"

- 도메인 주소: 'egov.nip.io'

- 프로토콜 : HTTPS

- 시크릿: wildcard-certs

- 경로 : /

- 서비스 : egov

- 포트 : 8080/TCP
```

**6. /etc/hosts(linux인 경우) 혹은 window hosts 파일에 아래 내용 등록 후 egov.nip.io를 저장한 뒤, 생성한 인그레스에 접속해보세요.**

```
...
10.140.22.140  egov.nip.io
```