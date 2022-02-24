---
layout: default
title: 7-2. 시크릿
nav_order: 2
parent: 7. 구성
---

# 시크릿
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

## 시크릿(Secret)
시크릿은 암호, 토큰 또는 키와 같은 소량의 중요한 데이터를 포함하는 오브젝트입니다.
이를 사용하지 않으면 중요한 정보가 파드 명세나 컨테이너 이미지에 포함될 수 있습니다.
시크릿을 사용한다는 것은 사용자의 기밀 데이터를 애플리케이션 코드에 넣을 필요가 없음을 뜻합니다.

시크릿은 컨피그맵과 유사하지만 특별히 기밀 데이터를 보관하기 위한 것입니다.

**시크릿 대표적인 용도**

- 비밀번호, 
- OAuth 토큰
- Docker Registry
- SSH 키

---

## 메뉴이동
`구성` ➡ `시크릿`

![config-002.png](/assets/images/config/config-002.png)

---

## 화면구성
생성된 시크릿 정보를 제공합니다.

![config-sc-001.png](/assets/images/config/config-sc-001.png){: width="800" }

---

## 시크릿 생성
`+생성`을 클릭 후 내용을 입력하여 시크릿을 생성할 수 있다. 시크릿은 FORM/YAML로 입력할 수 있습니다.

![config-sc-002.png](/assets/images/config/config-sc-002.png){: width="800" }

- Name
- Secret Type
- Data


**Secret Type**

| Secret Type         |         사용처    | 
|:-------------|:------------------|
| Opaque	| 임의의 사용자 정의 데이터 |
| kubernetes.io/service-account-token	| 서비스 어카운트 토큰 |
| kubernetes.io/dockercfg	 | 직렬화 된(serialized) ~/.dockercfg 파일 |
| kubernetes.io/dockerconfigjson	| 직렬화 된 ~/.docker/config.json 파일 | 
| kubernetes.io/basic-auth	| 기본 인증을 위한 자격 증명(credential) | 
| kubernetes.io/ssh-auth	| SSH를 위한 자격 증명 |
| kubernetes.io/tls	| TLS 클라이언트나 서버를 위한 데이터 |
| bootstrap.kubernetes.io/token  |	부트스트랩 토큰 데이터 |

---

## 시크릿 수정
시크릿 목록에서 특정 시크릿을 클릭하여 우측 YAML에 수정할 내용 입력 후 `수정`버튼을 클릭하면 수정할 수 있습니다.

---
## 시크릿 삭제
`삭제` 버튼 클릭 시 삭제 팝업창이 나타나며 삭제하려는 해당 네임스페이스/시크릿 명 입력 후 `Delete` 버튼 클릭 시 시크릿이 삭제됩니다.

![secret-delete.png](/assets/images/config/secret-delete.png){: width="800" }