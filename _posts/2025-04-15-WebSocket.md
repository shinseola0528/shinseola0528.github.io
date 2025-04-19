---
title: "웹소켓"
date: 2025-04-15 13:34
categories: Network
tag: [WebSocket, Network, Protocol, Realtime, STOMP, Spring]
layout: single
toc: true
author_profile: false
sidebar:
  nav: "docs"
---

## 1. 웹소켓(WebSocket)이란?

웹소켓(WebSocket)은 클라이언트와 서버 간에 양방향 통신을 실시간으로 수행할 수 있는 통신 프로토콜임. HTTP를 통해 초기 핸드셰이크(handshake)가 이루어진 후, Persistent(지속적인) 연결을 유지하여 데이터가 빠르고 효율적으로 전송됨.

## 2. 특징

1. 양방향 통신: 클라이언트와 서버가 서로 데이터를 주고받을 수 있음
2. 실시간성: 즉각적인 데이터 전송 가능
3. 경량 프로토콜: HTTP보다 오버헤드 적음
4. Persistent 연결: 연결이 유지되며 추가 요청 불필요
5. Full-Duplex 통신: 동시에 송수신 가능

## 3. 웹소켓의 동작 방식

1. 초기 핸드셰이크:
   - 클라이언트 → 서버 HTTP 업그레이드 요청
   - 서버 → WebSocket 업그레이드 응답
2. 양방향 데이터 통신:
   - 프레임 단위로 지속적인 메시지 전송
3. 연결 종료:
   - 클라이언트 또는 서버가 연결 종료 가능

## 4. 웹소켓의 장점

- 효율성: 반복적인 HTTP 오버헤드 제거
- 실시간 업데이트: 채팅, 알림 등에 적합
- 단순한 구현: HTTP 기반 시스템과 호환

## 5. 사용 사례

1. 채팅 애플리케이션
2. 실시간 알림 시스템
3. 온라인 게임
4. 주식/암호화폐 실시간 시세

## 6. 웹소켓과 HTTP의 차이점

| 특징              | HTTP                  | WebSocket                          |
| ----------------- | --------------------- | ---------------------------------- |
| 연결 방식         | 요청/응답 기반        | 핸드셰이크 이후 연결 유지          |
| 데이터 전송 방향  | 단방향                | 양방향                             |
| 프로토콜 오버헤드 | 매 요청마다 헤더 포함 | 프레임 기반 전송으로 오버헤드 감소 |
| 실시간성          | 낮음                  | 높음                               |
| 사용 사례         | 정적 콘텐츠, REST API | 채팅, 알림, 게임, 실시간 정보      |

## 7. Spring에서의 웹소켓 구현

### 7.1 의존성 추가

```groovy
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-websocket'
}
```

### 7.2 WebSocket 설정

```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {
    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry) {
        registry.addEndpoint("/ws").setAllowedOrigins("*").withSockJS();
    }

    @Override
    public void configureMessageBroker(MessageBrokerRegistry config) {
        config.enableSimpleBroker("/topic");
        config.setApplicationDestinationPrefixes("/app");
    }
}
```

### 7.3 메시지 컨트롤러

```java
@Controller
public class WebSocketController {

    @MessageMapping("/sendMessage")
    @SendTo("/topic/messages")
    public String sendMessage(String message) {
        return message;
    }
}
```

### 7.4 클라이언트 예제

```javascript
const socket = new SockJS("/ws");
const stompClient = Stomp.over(socket);

stompClient.connect({}, () => {
  stompClient.subscribe("/topic/messages", (response) => {
    console.log("Received: ", response.body);
  });

  stompClient.send("/app/sendMessage", {}, "Hello, WebSocket!");
});
```

## 8. wss:// 프로토콜

### 8.1 wss://란?

- `wss://`는 WebSocket Secure의 약자
- TLS/SSL을 적용하여 암호화된 WebSocket 통신을 제공
- 민감한 데이터 통신 시 보안 필수

### 8.2 ws:// vs wss://

| 구분 | ws://          | wss://                             |
| ---- | -------------- | ---------------------------------- |
| 보안 | 없음           | TLS 암호화                         |
| 포트 | 80             | 443                                |
| 용도 | 테스트, 내부망 | 실서비스, 모바일, 공개 네트워크 등 |

## 9. STOMP란?

- STOMP (Simple Text Oriented Messaging Protocol)는 WebSocket 위에서 작동하는 경량 메시징 프로토콜
- 메시지를 주제 기반(pub/sub)으로 송수신 가능

### 9.1 STOMP 메시지 구조 예시

```text
SEND
destination:/app/sendMessage
content-type:text/plain

Hello, STOMP!
```

### 9.2 STOMP가 필요한 이유

| WebSocket 단독             | WebSocket + STOMP                    |
| -------------------------- | ------------------------------------ |
| 데이터 구조 직접 정의 필요 | 목적지(destination) 기반 메시지 전송 |
| 송수신 분리 어려움         | 구독(subscribe), 발행(send) 명확     |
| 사용자별 라우팅 직접 처리  | STOMP가 자동으로 라우팅 가능         |

## 10. 한계와 고려사항

1. 브라우저 호환성: 최신 브라우저는 대부분 지원
2. 보안: 반드시 `wss://`로 암호화 적용 필요
3. 서버 부하: 연결 수가 많아질수록 리소스 관리 중요
