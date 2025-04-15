---
layout: single
title: "주요 메신저 앱 기술 비교 정리"
categories: Network
tags: [MQTT, MTProto, WebSocket, SignalProtocol, RabbitMQ, Kafka]
toc: true
author_profile: false
sidebar:
  nav: "docs"
---

# 주요 메신저 앱 기술 비교 정리



## ✅ 정리 목적

- 카카오톡, WhatsApp, Line, Telegram 등 주요 메신저 앱들이 사용하는 **실시간 통신 기술**, **보안 방식**, **메시지 처리 방식**, **프로토콜** 등을 비교하고 정리.





## ✅ 메신저별 기술 비교

| 메신저       | 실시간 통신        | 메시지 큐       | 저장 방식                        | 보안(E2EE)                | 특징                                     |
| ------------ | ------------------ | --------------- | -------------------------------- | ------------------------- | ---------------------------------------- |
| **카카오톡** | MQTT (TCP 위)      | RabbitMQ, Kafka | 서버 저장 (Cassandra, Redis)     | ❌ (일반 채팅은 서버 저장) | 모바일 최적화, 멀티 디바이스 지원        |
| **WhatsApp** | TCP + MQTT         | 내부 큐 시스템  | ❌ (서버 저장 X)                  | ✅ 기본 E2EE               | Signal Protocol 기반, 매우 강력한 보안   |
| **Line**     | WebSocket + HTTP/2 | Kafka, Redis    | 서버 저장 (MySQL, Aerospike)     | 🔄 선택적 (Letter Sealing) | API, Notify, Bot 플랫폼 확장성 우수      |
| **Telegram** | MTProto (TCP 기반) | 자체 분산 처리  | 기본 서버 저장 / Secret Chat은 X | 🔄 Secret Chat만 E2EE      | 속도 빠름, 대용량 전송, 비공개 채널 지원 |





## ✅ 주요 프로토콜 비교

| 프로토콜            | 사용 메신저         | 전송 방식                   | 보안                 | 특징                             |
| ------------------- | ------------------- | --------------------------- | -------------------- | -------------------------------- |
| **MQTT**            | KakaoTalk, WhatsApp | TCP 기반 경량 메시지 전송   | 중간~강함 (QoS 지원) | 모바일/IoT에 최적, 배터리 절약   |
| **Signal Protocol** | WhatsApp            | TCP + E2EE                  | 🔒 매우 강력          | 종단간 암호화 기본 제공          |
| **MTProto**         | Telegram            | TCP 기반 자체 암호화        | 중간~강함            | 고속 전송, 자체 암호화 구조      |
| **WebSocket**       | Line                | HTTP 업그레이드 양방향 통신 | TLS 필요             | 브라우저·앱에 적합한 실시간 통신 |





## ✅ E2EE (종단 간 암호화) 비교

| 메신저       | E2EE 적용                 | 설명                                          |
| ------------ | ------------------------- | --------------------------------------------- |
| **WhatsApp** | ✅ 전체 적용               | Signal Protocol 기반, 메시지 서버 저장 X      |
| **Telegram** | 🔄 선택적                  | 기본은 서버 저장, Secret Chat에서만 E2EE 적용 |
| **카카오톡** | ❌ 기본 채팅은 E2EE 아님   | 서버에 메시지 저장, 일부 비밀채팅 지원        |
| **Line**     | 🔄 선택적 (Letter Sealing) | 일부 기기 및 채팅에만 적용 가능               |





## ✅ MTProto란?

- Telegram이 자체 개발한 고속 고보안 프로토콜
- TCP 위에서 작동
- Secret Chat 시 E2EE, 일반 채팅은 서버 저장
- 메시지 압축, 세션 관리, 멀티 디바이스 동기화에 최적화



### 🔽 MTProto 구조 다이어그램

```
[Client App]
    ↓ TCP 연결 (TLS optional)
[MTProto 암호화 메시지 전송]
    ↓
[Telegram 서버: 단순 중계 only]
    ↓
[상대방 Client App → 복호화]
```



### 🔽 MTProto 기반 Secret Chat 시나리오

```
사용자 A (보낸 사람)
  └─> 메시지 입력 및 암호화 (기기에서만 수행)
    └─> TCP 연결로 암호화된 메시지 전송
      └─> Telegram 서버는 암호문을 중계만 함
        └─> 사용자 B (받는 사람)의 기기가 메시지 수신 및 복호화
```





## ✅ MQTT란?

- TCP 기반 경량 메시지 프로토콜
- WhatsApp, KakaoTalk에서 실시간 통신에 사용
- QoS 보장 (0, 1, 2), reconnect 용이, 배터리 절약



### 🔽 MQTT 동작 구조

```
[Client A]
    ⇄ TCP 연결
    ⇄ MQTT publish("/chat/userB", message)
       ↓
     [MQTT Broker]
       ↓
    ⇄ MQTT subscribe("/chat/userB")
[Client B]
```



### 🔽 MQTT 기반 메시지 전송 시나리오

```
사용자 A가 메시지를 보냄
  └─> MQTT publish (토픽: /chat/userB, 내용: "안녕!")
    └─> MQTT 브로커가 메시지를 수신
      └─> 사용자 B가 해당 토픽을 subscribe 중이라면
        └─> 실시간으로 메시지 수신
```





## ✅ 멀티 디바이스 동기화 흐름도 (Telegram/Line 등)

```
사용자 A가 PC에서 메시지 전송
  └─> 서버에 메시지 저장 (클라우드 기반 채팅)
    └─> 서버는 메시지를 모든 기기로 push
      ├─> 사용자 A의 모바일 → 동기화
      └─> 사용자 B의 모든 디바이스에 전송됨
```



## ✅ 푸시 알림 흐름도 (WhatsApp, KakaoTalk, Line 등)

```
사용자 A가 메시지를 보냄
  └─> 서버에서 수신자 B가 오프라인 상태임을 확인
    └─> 메시지는 서버에 저장됨
      └─> 서버는 FCM/APNs 등 외부 푸시 서비스에 알림 요청
        └─> 사용자 B 기기에서 알림 수신
          └─> 앱 열기 후 메시지 다운로드 및 복호화
```



## ✅ 주요 아키텍처 흐름도 (공통 구성 예시)

```
[Client App]
   ├── 사용자 입력 (메시지, 파일 등)
   └── 실시간 전송
        ↓
     [전송 계층: MQTT / WebSocket / MTProto]
        ↓
     [서버 처리 계층]
        ├── MQ 발행 (Kafka, RabbitMQ 등)
        ├── 메시지 저장 (DB, NoSQL)
        ├── 푸시 알림 전송 (FCM, APNs)
        └── 동기화 처리
            ↓
     [수신자 디바이스들]
        └── 동기화 및 복호화 수행
```





## ✅ 질문 요약 및 답변

1. **채팅 기능에 WebSocket 외 다른 대안은?**
   - Polling, Long Polling, SSE, WebRTC, Firebase, GraphQL Subscription 등
2. **MQ 사용 이유는?**
   - 대규모 메시지 비동기 처리, 유실 방지, 분산 시스템 확장성 확보
3. **카카오톡과 라인은 MQ 사용?**
   -  사용함 (Kafka, RabbitMQ 등)
4. **E2EE란?**
   - 송신자 → 수신자 간 **암호화된 메시지 전송**
   - 서버도 메시지 내용을 열람 불가
5. **TCP + MQTT란?**
   - TCP 연결 위에서 MQTT 메시지를 실시간 주고받는 구조
   - WhatsApp, KakaoTalk 등에 사용
6. **MTProto란?**
   - Telegram 전용 프로토콜 (TCP 기반)
   - 속도/압축/보안에 최적화, Secret Chat에서는 E2EE 적용