---
layout: default
title: 5.4.1 카탈로그 트리거
nav_order: 1
grand_parent: 5. 애플리케이션
parent: 5.4 트리거
---

# 카탈로그 트리거
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



## 카탈로그 트리거 생성
트리거를 생성하기 위해서는 카탈로그가 하나 생성이 되어 있어야 합니다.
![catalog-trigger](/assets/images/application/trigger/catalog-trigger.png){: width="1200" }

**카탈로그 트리거 설정**

트리거를 생성하면 다양한 설정을 진행 할 수 있습니다.
![catalog-option](/assets/images/application/trigger/catalog-trigger-option.png){: width="1000" }


**예약 종류**
- 예약 액션 : 특정 행동이 감지되면 예약도된 시간에 빌드가 이루어지게 할 수 있습니다.
(아무런 행동이 이루어지지 않았다면 빌드는 생략됩니다.)
- 빌드 후 액션 : 예약 액션과 연쇄적인 액션으로, 예약 액션이 실행 된 후 빌드 후 액션이 진행됩니다.

### 예약 액션

- 이름 

    ![reserved-action-name](/assets/images/application/trigger/reserved-action-name.png){: width="600" }

    - trigger 이름을 지정

- 스케줄

    ![reserved-action-schedule](/assets/images/application/trigger/reserved-action-schedule.png){: width="600" }
    
    - cronjob 형태이며 자율적으로 원하는 시간을 설정할 수 있다.
    - 예시    
        ```     
        */5 * * * * # 5분 마다 한번 씩     
        ```

- 특정 행동 종류 
![reserved-action-action](/assets/images/application/trigger/reserved-action-action.png){: width="1000" }
    - 원하는 행동으로 지정해서 사용하면 됩니다.

- 옵션
![reserved-action-option](/assets/images/application/trigger/reserved-action-option.png){: width="1000" }

    - 트리거 수행 서비스 어카운트
        - 트리거를 수행하기 위해서는 service account가 필요합니다.
            - trigger를 수행하는 권한이 있는 계정이라고 생각하면 됩니다.
            - 기존에는 권한이 할당되어 있지 않기 때문에, service account를 새로 생성해서 권한을 부여하거나, 기존 service account에 권한을 부여하는 방법 두 가지가 있습니다.
    - vcs 카테고리 태스크 이름
        - commit을 감지하고자 하는 vcs를 설정한 태스크 이름을 설정하면 됩니다.
            - 기본적으로 맨 처음 설정한 vcs를 감지하기 떄문에, 2개 이상이 아니라면 생략해도 무방합니다.
    - 버전관리 시스템의 저장소 인증 시크릿
        - github 처럼 public repo가 아닌, private한 저장소를 사용할 때 필요한 접근 정보 시크릿을 입력하면 됩니다.

### 빌드 후 액션
- 이름 : 예약 액션 설정할 때 설정했기에 생략
- 특정 행동 종류

    ![post-build-action-kind](/assets/images/application/trigger/post-build-action-kind.png){: width="600" }


    - 원하는 행동으로 지정해서 사용하면 됩니다.

- 옵션
![post-build-action-option](/assets/images/application/trigger/post-build-action-option.png){: width="1000" }
    - 트리거 수행 서비스 어카운트
    - 대상(카탈로그/파이프라인) 종류
        - 예약 액션으로 카탈로그 및 파이프라인이 빌드가 되었을 때, 빌드가 되길 원하는 종류를 지정하면 됩니다.
    - 빌드(배포)를 수행할 대상 지정
        - 대상 종류를 카탈로그로 지정하면, 빌드가 되길 원하는 카탈로그를 선택해주면 됩니다.
        - 대상 종류를 파이프라인으로 지정하면, 빌드가 되길 원하는 파이프라인을 선택해주면 됩니다.
    - 트리거 수행 매칭 조건 빌드 상태 목록
        - 예약액션의 빌드 상태를 선택할 수 있습니다.

### 카탈로그 생성 확인
아래 화면과 같이 생성된 것을 확인할 수 있습니다.
![catalog-trigger-check](/assets/images/application/trigger/catalog-trigger-check.png){: width="1200" }

## 카탈로그 트리거 수정
원하는 트리거의 수정 버튼을 눌러 트리거 수정도 가능합니다.
![catalog-trigger-modify](/assets/images/application/trigger/catalog-trigger-modify.png){: width="1200" }

## 카탈로그 트리거 삭제
삭제할 트리거의 삭제 버튼을 눌러 트리거 삭제도 가능합니다.
![catalog-trigger-delete](/assets/images/application/trigger/catalog-trigger-delete.png){: width="1200" }


---

## 연습문제

**1. 트리거를 이용해서 카탈로그 정기 배포를 수행하세요.**

해당 연습 문제는 아래의 카탈로그 연습 문제를 선행한 뒤 진행합니다.
```5. 애플리케이션 -> 5.2 카탈로그 -> 5.2.1 카탈로그 배포 -> 연습 문제1```

아래 예제YAML을 토대로, tgr-builder ServiceAccount 및 ClusterRoleBinding을 생성합니다.

<details>
<summary>예제 Yaml</summary>
  
{% highlight yaml %}
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: tgr-builder
  namespace: <namespace>

---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: tgr-builder
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: tgr-builder
  namespace: <namespace>

{% endhighlight %}
   
</details>


```
- 예약 액션
- 트리거 이름: tgr-daily-deploy
- 스케쥴: 0 * * * *(Every Hour)
- 트리거 수행 서비스 어카운트: tgr-builder
```

**2. 설정된 트리거 상태를 확인하세요.**