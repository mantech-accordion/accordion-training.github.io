---
layout: default
title: 12.2 레지스트리
nav_order: 2
parent: 12. 설정
---

# 레지스트리
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

## 레지스트리

레지스트리는 클러스터에서 공통으로 사용할 컨테이너 이미지 저장소를 관리합니다. 이 저장소는 클러스터에 배포된 네임스페이스에서 접근할 수 있습니다. 아코디언에서는 기본으로 인프라 레지스트리와 사용자 레지스트리를 제공합니다.

> 💡 참고 : 인프라 레지스트리는 아코디언 구동에 필요한 인프라 컨테이너 이미지들을 저장하는 용도입니다. 사용자는 사용자 레지스트리만 사용합니다.

![registry-list.png](/assets/images/setting/registry-list.png)

---

## 레지스트리 생성

+생성 을 선택하면 나타나는 모달에서 레지스트리 리소스 정보를 입력하여 생성할 수 있습니다.

![registry-create.png](/assets/images/setting/registry-create.png)

---

## 레지스트리 이미지 태그 보기

보기를 클릭하면 각 이미지에 해당하는 태그 개수를 확인할 수 있습니다.

![registry-tag-info.png](/assets/images/setting/registry-tag-info.png)

---

## 레지스트리 이미지 확인

각 이미지를 클릭하면 해당 이미지 개수, 사이즈, 생성일, 서명 여부 등 이미지에 대한 정보를 확인할 수 있으며,
이미지 삭제, 태그 변경 등의 작업을 수행할 수 있습니다.

- 기본 확인
![registry-image-info.png](/assets/images/setting/registry-image-info.png)

- 상세 확인
![registry-image-info-detail.png](/assets/images/setting/registry-image-info-detail.png)


---
## 레지스트리 수정

수정하려는 레지스트리를 선택하고 우측의 YAML 편집기에서 정보를 변경 후 수정 버튼을 선택하여 반영합니다.

- 이미지 삭제
![registry-remove-image.png](/assets/images/setting/registry-remove-image.png)

- 이미지 태그 변경
![registry-change-image-tag.png](/assets/images/setting/registry-change-image-tag.png)

---
## 레지스트리 삭제

삭제하려는 레지스트리를 선택하고 우측의 삭제 버튼을 선택합니다.

![registry-delete.png](/assets/images/setting/registry-delete.png)

모달에서 레지스트리 이름을 입력하여 삭제합니다.