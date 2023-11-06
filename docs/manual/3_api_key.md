---
layout: default
title: 13.3 API KEY 사용 가이드
nav_order: 3
parent: 13. 메뉴얼
---

# 13.3 API KEY 사용 가이드
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 📖 API KEY 사용 가이드

아코디언 버전 `v2.6.0 릴리즈 이후`부터 `아코디언 API`를 사용하기 위한 KEY 발급 기능을 제공하고 있습니다.

아코디언 API KEY 발급받는 방법은 아코디언 대시보드 우측 상단에 있는 `API KEY` 버튼을 클릭합니다.

![3_api_key.png](/assets/images/manual/3_api_key.png){: width="1200" }

---

API KEY 발급 화면에서 `생성` 버튼을 클릭하여 `만료일`, `KEY 이름`을 입력 후 생성합니다.

![3_create_api_key_1.png](/assets/images/manual/3_create_api_key_1.png){: width="1200" }

![3_create_api_key_2.png](/assets/images/manual/3_create_api_key_2.png){: width="1200" }

생성한 KEY를 복사하여 API 호출에 사용합니다.
![3_create_api_key_3.png](/assets/images/manual/3_create_api_key_3.png){: width="800" }

---

## **API KEY 사용 예시**

curl을 통해 아코디언 이벤트 로그를 조회하는 예시입니다.

- 아코디언 URL 알맞게 입력
```
$ ACC="10.140.0.150:30000"
```

- API KEY 토큰 값 알맞게 입력
```
$ TOKEN="acc-JlxTvn_cLFqLAeZwREgO0fEnCYKJTxONvd66G338nKI"
```

- 호출
```
$ curl -v \
       -X GET \
       -H 'Accept: application/json' \
       -H "Authorization: Bearer $TOKEN" \
       -k https://$ACC/apis/k8s/log.accordions.co.kr/v1beta1/logineventlogs
```

```
<결과 값>
{
  "kind": "LoginEventLogList",
  "apiVersion": "log.accordions.co.kr/v1beta1",
  "metadata": {
    "continue": "MTAw"
  },
  "items": [
    {
      "metadata": {
        "name": "admin",
        "creationTimestamp": "2023-11-06T00:13:16Z"
      },
      "spec": {
        "type": "login",
        "userId": "2c57fec6-da15-4590-a149-94973973e6e4",
        "sessionId": "eb1a23ff-d409-480e-b1a3-48d2ac1fae7c",
        "ipAddress": "10.10.255.250"
      }
    },
    {
      "metadata": {
        "name": "admin",
        "creationTimestamp": "2023-11-03T07:47:34Z"
      },
      "spec": {
        "type": "login",
        "userId": "2c57fec6-da15-4590-a149-94973973e6e4",
        "sessionId": "f83f9c9a-7157-4b2c-8453-95c5d89b64f1",
        "ipAddress": "10.10.178.46"
      }
    }
    ... 중략 ...
}
```


보다 자세한 API 메뉴얼을 확인하고자 하는 경우 `om@mantech.co.kr`에 문의주시기 바랍니다.