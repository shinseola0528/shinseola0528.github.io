---
layout: single
title: "[Docker 기초 02] Docker 컨테이너 구조 및 커맨드 사용법 - 이론편"
date: 2025-04-29
categories:
  - Docker
tags:
  - Docker
  - Container
  - 명령어
  - 가상화
toc: true
author_profile: false
sidebar:
  nav: docs
---

### Docker 컨테이너 구조 및 커맨드 강의 영상

<iframe width="560" height="315" src="https://www.youtube.com/embed/M25Pl0tX8yw" frameborder="0" allowfullscreen></iframe></iframe>

### 도커 컨테이너 구조

- 도커 컨테이너는 **컨테이너 레이어(Container Layer)** 와 **이미지 레이어(Image Layers)** 로 구성됩니다.

![도커 컨테이너 구조](../../images/2025-04-29-docker-basic-02/docker-container-structure-01.png)

- **컨테이너 레이어**: 읽기/쓰기 가능한 계층으로, 실행 중 변경사항이 저장됩니다.
- **이미지 레이어**: 읽기 전용 계층, 다른 컨테이너와 공유 가능합니다.

<br>

### 도커 컨테이너 레이어가 공유되는 구조

- 컨테이너 레이어는 각각 독립적이지만, **이미지 레이어는 여러 컨테이너가 공유**합니다.

![도커 공유 구조](../../images/2025-04-29-docker-basic-02/docker-container-structure-02.png)

<br>

### 도커 명령어 구조

- 도커의 모든 명령어는 다음 패턴을 따릅니다.

```plaintext
docker {대상} {커맨드} {옵션} {인자}
```

- 주 커맨드 대상:
  `container`
  `image`
  `volume`
  `network`
  <br>

### 도커 명령어 확인 방법

- 터미널에 `docker` 입력 시 도움말 명령어 리스트를 확인할 수 있습니다.
- `docker [command 대상] --help`로 고급 명령 설명도 가능합니다.

![도커  커멘드](../../images/2025-04-29-docker-basic-02/docker-command.png)
<br>

### Container 관련 주 커맨드

| 커맨드 | 설명                                       | 주 옵션                        |
| :----- | :----------------------------------------- | :----------------------------- |
| start  | 컨테이너 실행                              | -i                             |
| stop   | 컨테이너 정지                              |                                |
| create | 컨테이너 생성                              | --name, -e, -p, -v             |
| run    | 이미지를 다운로드 후 컨테이너 생성 및 실행 | --name, -e, -p, -v, -d, -i, -t |
| rm     | 컨테이너 삭제                              | -f, -v                         |
| exec   | 컨테이너에서 프로그램 실행                 | -i, -t                         |
| ls     | 컨테이너 목록 출력                         | -a                             |
| cp     | 컨테이너와 호스트 간 파일 복사             |                                |
| commit | 컨테이너를 이미지로 변환                   |                                |

<br>

### Image 관련 주 커맨드

| 커맨드 | 설명                         | 주 옵션 |
| :----- | :--------------------------- | :------ |
| pull   | 이미지를 다운로드            |         |
| rm     | 이미지 삭제                  |         |
| ls     | 가지고 있는 이미지 목록 출력 |         |
| build  | 이미지 생성                  | -t      |

<br>

### 주요 옵션 설명

| 옵션   | 설명                       |
| :----- | :------------------------- |
| --name | 컨테이너 이름 지정         |
| -p     | 포트 번호 지정             |
| -v     | 볼륨 설정                  |
| -e     | 환경 변수 설정             |
| -d     | 백그라운드 실행            |
| -i     | 컨테이너에 터미널 연결     |
| -t     | 특수 키 사용 가능하게 설정 |
