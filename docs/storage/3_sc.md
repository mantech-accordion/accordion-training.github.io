---
layout: default
title: 9.3 스토리지클래스
nav_order: 3
parent: 9. 스토리지
---

# 스토리지클래스
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

## 스토리지클래스(Storageclass)
스토리지클래스는 관리자가 제공하는 스토리지의 "classes"를 설명할 수 있는 방법을 제공합니다. 
다른 클래스는 서비스의 품질 수준 또는 백업 정책, 클러스터 관리자가 정한 임의의 정책에 매핑될 수 있습니다.

<details>
<summary>예제 Yaml</summary>
  
{% highlight yaml %}

apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: standard
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
reclaimPolicy: Retain
allowVolumeExpansion: true
mountOptions:
  - debug
volumeBindingMode: Immediate

{% endhighlight %}
   
</details>

---
## 메뉴이동
`스토리지` ➡ `스토리지클래스`

![storage-003.png](/assets/images/storage/storage-003.png)

---

## 화면구성
생성된 스토리지클래스 정보를 제공합니다.

![storage-008.png](/assets/images/storage/storage-008.png){: width="1200" }

---

## 스토리지클래스 생성
`+생성`을 클릭 후 내용을 입력하여 스토리지클래스를 생성할 수 있다. 스토리지클래스는 YAML로 입력할 수 있습니다.

![storage-009.png](/assets/images/storage/storage-009.png){: width="1200" }

---

## 스토리지클래스 수정
스토리지클래스 목록에서 특정 스토리지클래스을 클릭하여 우측 YAML에 수정할 내용 입력 후 `수정`버튼을 클릭하면 수정할 수 있습니다.

---

## 스토리지클래스 삭제
`삭제` 버튼 클릭 시 삭제 팝업창이 나타나며 삭제하려는 해당 스토리지클래스 명 입력 후 `Delete` 버튼 클릭 시 스토리지클래스가 삭제됩니다.

![storageclass-delete.png](/assets/images/storage/storageclass-delete.png){: width="1200" }


---
## 연습문제

**1. 예제yaml을 사용하여 PersistentVolumeClaim을 생성하세요.**

```
- name: dynamic-pvc
  accessMode: ReadWriteMany
  capacity: 1Gi
  volumeMode: Filesystem
  storageClassName: nfs-sc
```

<details>
<summary>예제Yaml</summary>
  
{% highlight yaml %}
---
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: dynamic-pvc
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 1Gi
  volumeMode: Filesystem
  storageClassName: nfs-sc

{% endhighlight %}
   
</details>

**2. 새로 생성되는 PV와 PVC의 상태를 확인하세요.**

**3. 생성한 PVC를 아래 예제 YAML을 활용하여 volumtMount 하세요.**

<details>
<summary>예제Yaml</summary>
  
{% highlight yaml %}
---
apiVersion: v1
kind: Pod
metadata:
  labels:
    app: nginx
  name: nginx
spec:
  containers:
  - image: base.registry.accordions.co.kr:5000/nginx:1.20.1-alpine
    imagePullPolicy: Always
    name: nginx
    resources: {}
    volumeMounts:
    - name: nginx-data
      mountPath: /usr/share/nginx/html
  volumes:
  - name: nginx-data
    persistentVolumeClaim:
      claimName: dynamic-pvc

{% endhighlight %}
   
</details>


**4. 생성한 리소스를 모두 삭제하세요.**