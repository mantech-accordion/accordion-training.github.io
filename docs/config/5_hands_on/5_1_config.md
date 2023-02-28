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
## 연습문제

**1. 아래 속성으로 새 컨피그맵과 시크릿을 생성하고, 생성한 컨피그맵과 시크릿을 Pod에 사용하세요.**

```
- 컨피그맵 이름 : game-demo
  Pod name: demo-env-pod
  Image name: nginx:latest
```

---

```
(참고)

data:
  # 속성과 비슷한 키; 각 키는 간단한 값으로 매핑됨
  player_initial_lives: "3"
  ui_properties_file_name: "user-interface.properties"

  # 파일과 비슷한 키
  game.properties: |
    enemy.types=aliens,monsters
    player.maximum-lives=5    
  user-interface.properties: |
    color.good=purple
    color.bad=yellow
    allow.textmode=true 
```
---

```
(참고)
env: 
  - name: PLAYER_INITAL_LIVES
    valueFrom: 
      configMapKeyRef:
        name: game-demo
        key: player_initial_lives
  - name: UI_PROPERTIES_FILE_NAME
    valueFrom:
      configMapKeyRef:
        name: game-demo
        key: ui_properties_file_name
```

**2. 1번에서 생성한 컨피그맵을 이용하여 새로운 파드에 마운트하여 사용하세요.**

```
- Pod name: demo-mount-pod
 Image name: nginx
```

---

```
  volumeMounts:
    - name: config
      mountPath: "/config"
      readOnly: true
volumes:
  - name: config
    configMap:
      name: game-demo
      items:
      - key: "game.properties"
        path: "game.properties"
      - key: "user-interface.properties"
        path: "user-interface.properties"
```

**3. 생성한 리소스들을 삭제하세요.**