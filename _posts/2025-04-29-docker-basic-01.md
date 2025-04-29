---
layout: single
title: "[Docker 기초 01] 도커 기초 강의"
date: 2025-04-29
categories: Docker
tags:
  - Docker
  - Container
  - 설치
  - 가상화
toc: true
author_profile: false
sidebar:
  nav: docs
---

### Docker 강의 영상
<iframe width="560" height="315" src="https://www.youtube.com/embed/p1-wm-ThnTI" frameborder="0" allowfullscreen></iframe>

<br>

### Docker란?

- Docker는 **컨테이너 기반**의 오픈소스 가상화 플랫폼입니다.
- 프로그램을 외부 환경과 **격리**하여 구동할 수 있게 해주는 **소프트웨어**입니다.

<br>

### 컨테이너란?

- 컨테이너란 **OS 상에 논리적인 영역**을 만들어, 애플리케이션이 필요한 요소들을 모아 **독립적으로 동작**하게 하는 것입니다.
- 필요한 요소만 포함되어 **오버헤드가 최소화**됩니다.

<br>

### 컨테이너 구성 예시

컨테이너는 다음과 같은 구조로 이루어져 있습니다.

![컨테이너 구조도](../../images/2025-04-29-docker-basic-01/docker-container-structure.png)


- App A, App B, App C 등 여러 애플리케이션이 Docker를 통해 독립적으로 관리됩니다.
- Docker는 Host 운영체제 위에 설치되며, 그 아래 인프라가 있습니다.

<br>

### Docker 설치하기

- 공식 링크: [https://docker.com/get-started/](https://docker.com/get-started/)
- 설치 방법
  - **Docker Desktop** 설치 (Windows / Mac(Intel/Apple 칩) / Linux용 제공)
  - **Docker Hub** 가입 필요 (애플리케이션 이미지 저장 및 팀 협업)

