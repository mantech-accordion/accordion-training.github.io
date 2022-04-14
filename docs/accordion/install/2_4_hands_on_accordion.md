---
layout: default
title: 2.4.4 👨‍💻 실습
nav_order: 5
parent: 2.4 Accordion 설치
grand_parent: 2. Accordion v2
---

# 2.4.4 👨‍💻 [실습]아코디언v2 인스톨
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


---


## 📖 설치 준비사항

<details>
<summary>ssh key 생성, 복사, 접속 확인</summary>
  
{% highlight bash %}


Ansible script 수행을 위해 각 노드에서 ssh로 root 로그인이 가능하도록 설정 변경합니다. (Master&node 서버) 
$ vi /etc/ssh/sshd_config
…
PasswordAuthentication yes
PermitRootLogin yes
…
$ systemctl restart sshd

master서버에서 ssh key를 생성합니다. (Master 서버) (Master서버를 포함하여 적용해야합니다.)
$ ssh-copy-id -i /root/.ssh/id_rsa.pub [노드IP]
The authenticity of host '10.140.0.3 (10.140.0.3)' can’t be established.
ECDSA key fingerprint is 34:b2:38:b8:be:1b:dd:f1:44:d8:ba:ec:92:d1:d6:dc.
Are you sure you want to continue connecting (yes/no)? yes
/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed — if you are prompted now it is to install the new keys
root@10.140.0.3’s password:
Number of key(s) added: 1
Now try logging into the machine, with: "ssh '10.140.0.3'"
and check to make sure that only the key(s) you wanted were added.
(cluster의 구성서버 모두 등록할 때까지 반복해야 합니다.)

SSH Key 설정이 정상적인 확인합니다. (Master 서버) (Master서버를 포함하여 적용해야합니다.)
$ ssh [노드IP]
The authenticity of host 'acc-node1 (10.140.0.3)' can’t be established.
ECDSA key fingerprint is 34:b2:38:b8:be:1b:dd:f1:44:d8:ba:ec:92:d1:d6:dc.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'acc-node1' (ECDSA) to the list of known hosts.
Last failed login: Mon Sep 4 08:17:06 UTC 2017 from 59.49.38.210 on ssh:notty
There was 1 failed login attempt since the last successful login.
Last login: Mon Sep 4 07:18:33 2017
[root@acc-node1 ~] (패스워드 없이 로그인이 가능하면 정상입니다.)

{% endhighlight %}
   
</details>


<details>
<summary>Ansible 설치 (아코디언 설치 패키지에 포함)</summary>
  
{% highlight bash %}
# 각 OS에 맞도록 접속
$ /rpms/rpm_redhat7/0_ansible/install.sh # Redhat 계열 7버전
$ /rpms/rpm_redhat8/0_ansible/install.sh # Redhat 계열 8버전
$ /rpms/rpm_dpkg/0_ansible/install.sh # ubuntu 18버전

{% endhighlight %}
   
</details>

<details>
<summary>/etc/hosts 파일 수정</summary>
  
{% highlight bash %}

$ vi /etc/hosts
10.140.0.2
acc-master
10.140.0.3
acc-node1
10.140.0.4
acc-node2
10.140.0.5
acc-master2
10.140.0.6
acc-master3
…
{% endhighlight %}
   
</details>


**아코디언 설치 설정**
- accordion-installer/hosts 수정
- accordion-installer/group_vars/host.yml 수정


**아코디언 설치 및 확인**
- accordion-installer/install.sh
- accordion-installer/status.sh

**설치 설정**
```bash
$ accordion-installer/install.sh
```

**설치 진행**
```bash
$ accordion-installer/install.sh
End User Software License Agreement

This is a legal agreement between Customer and Man Technology Co., LTD. ("Mantech").  YOU MUST READ AND AGREE TO THE TERMS OF THIS END USER SOFTWARE LICENSE AGREE
MENT ("AGREEMENT") BEFORE ANY SOFTWARE CAN BE DOWNLOADED OR INSTALLED OR USED.  BY CLICKING ON THE "ACCEPT" BUTTON OR TYPING THE "Y" OF THIS AGREEMENT, OR DOWNLOA
DING, INSTALLING OR USING THE SOFTWARE, YOU ARE AGREEING TO BE BOUND BY THE TERMS AND CONDITIONS OF THIS AGREEMENT.  IF YOU DO NOT AGREE WITH THE TERMS AND CONDIT
IONS OF THIS AGREEMENT, THEN YOU SHOULD NOT DOWNLOAD, INSTALL OR USE THE SOFTWARE.  BY DOING SO YOU FORGO ANY IMPLIED OR STATED RIGHTS TO DOWNLOAD OR INSTALL OR U
SE THE SOFTWARE.
...
...
16. Questions.  Should you have any questions concerning the foregoing, please contact Mantech at the following address: Man Technology Co., LTD. 12th Fl, 308-4,
Seongsudong 2ga, Seongdong-gu, Seoul, Korea.
                 Phone : +82-2-2136-6900
                 E-mail : marketing@mantech.co.kr
                 www.mantech.co.kr


DO YOU ACCEPT THE TERMS OF THIS LINCESE AGREEMENT? [y/n] : y
```

**설치 확인**
```bash
$ accordion-installer/status.sh
========================================
 nodes
========================================
NAME         STATUS   ROLES                  AGE    VERSION
acc-master   Ready    control-plane,master   177m   v1.20.8
acc-node1    Ready    worker                 176m   v1.20.8
========================================
 deployments/po/svc
========================================
NAMESPACE     NAME                                           READY   UP-TO-DATE   AVAILABLE   AGE
acc-global    deployment.apps/alert-apiserver                1/1     1            1           162m
acc-global    deployment.apps/authset-manager                1/1     1            1           161m
acc-global    deployment.apps/chartmuseum-chartmuseum        1/1     1            1           163m
acc-global    deployment.apps/cloud-apiserver                1/1     1            1           161m
acc-global    deployment.apps/clusterinfo-manager            1/1     1            1           172m
acc-global    deployment.apps/console                        1/1     1            1           162m
acc-global    deployment.apps/gateway                        1/1     1            1           162m
acc-global    deployment.apps/host-log-apiserver             1/1     1            1           162m
acc-global    deployment.apps/keycloak                       1/1     1            1           163m
acc-global    deployment.apps/keycloak-db                    1/1     1            1           163m
acc-global    deployment.apps/manual-webserver               1/1     1            1           161m
acc-global    deployment.apps/monitoring-apiserver           1/1     1            1           162m
acc-global    deployment.apps/setting-manager                1/1     1            1           163m
acc-global    deployment.apps/thanos-querier                 1/1     1            1           163m
acc-system    deployment.apps/acc-grafana                    1/1     1            1           170m
acc-system    deployment.apps/acc-kube-state-metrics         1/1     1            1           170m
acc-system    deployment.apps/accordion-ingress-controller   1/1     1            1           170m
acc-system    deployment.apps/apm-agent-injector             1/1     1            1           166m
...
...

```

**아코디언 접속 URL**

| URL      | ID    | PW    |
|:---------|:------|:------|
| https://VIP://30000      | admin  | accordion!@# |

![acc-ins-1.png](/assets/images/accordion/acc-ins-1.png){: width="800" }


---


## 라이선스 등록
`글로벌 설정` ➡ `라이선스` ➡ `등록`

![practice-1.png](/assets/images/accordion/practice-1.png)
![practice-2.png](/assets/images/accordion/practice-2.png)
