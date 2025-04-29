---
layout: single
title: "[Docker 기초 03] Docker 컨테이너 구조 및 커맨드 사용법 - 실전편"
categories: Docker
tags: [Docker, CLI, Container]
toc: true
author_profile: false
sidebar:
  nav: "docs"
---

### Docker 커맨드 강의 영상

<iframe width="560" height="315" src="https://www.youtube.com/embed/prohMhNwZF0?si=X_Mkbf5uhbg676lo" frameborder="0" allowfullscreen></iframe>

### 1. Docker 커맨드 구조

- `docker` 명령어 입력 시, 사용 가능한 커맨드 목록이 표시됨
- 환경변수가 설정되지 않은 경우, 명령어 입력이 정상적으로 되지 않을 수 있음

### 2. 주요 커맨드 사용 예시

#### 2.1 `docker container`

```bash
docker container ls
docker container run httpd
```

- `run` 명령어는 새 컨테이너를 실행
- `-d` 옵션이 없으면 터미널에 묶임

#### 2.2 컨테이너 상태 확인 및 종료

```bash
docker container ls
docker container ls -a
docker container stop [컨테이너명]
```

- `docker container ls`: 실행 중인 컨테이너 목록만 출력
- `docker container ls -a`: **모든 컨테이너(종료된 것 포함)** 출력
- `docker container stop [컨테이너명]`: 지정한 컨테이너를 중지
- 자동 이름 부여 (네임 옵션 없을 경우)

#### 2.3 옵션과 함께 실행

```bash
docker container run --name test -d -p 580:80 httpd
```

- `--name`: 이름 지정
- `-d`: 백그라운드 실행
- `-p`: 포트 연결

### 3. 컨테이너 삭제

```bash
docker container stop test
docker container rm test
```

- `docker container stop [컨테이너명]` : 컨테이너 멈춤
- `docker container rm [컨테이너명]` : 컨테이너 삭제

### 4. 이미지 관련 커맨드

```bash
docker image ls
docker image rm nginx
```

- `docker image ls`: 이미지 목록 보기
- `docker image rm [이미지명]`: 이미지 삭제
- 이미지 ID, 생성일, 용량까지 확인 가능
  <br>
