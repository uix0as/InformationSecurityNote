# TLS와 HTTPS

TLS(Transport Layer Security)는 네트워크 통신을 보호하기 위한 암호화 프로토콜이다. HTTPS는 HTTP를 TLS로 보호한 형태이다.

```text
HTTPS = HTTP + TLS
```

## TLS가 제공하는 것

| 보안 속성 | 의미 |
| --- | --- |
| 기밀성 | 중간에서 내용을 읽기 어렵게 암호화한다. |
| 무결성 | 통신 중 데이터가 변조되었는지 확인한다. |
| 서버 인증 | 접속한 서버가 인증서의 주체와 일치하는지 확인한다. |
| 선택적 클라이언트 인증 | 환경에 따라 클라이언트 인증서도 사용할 수 있다. |

## HTTPS 캡슐화 구조

```text
Ethernet
└─ IP
   └─ TCP
      └─ TLS
         └─ HTTP
```

Ethernet 프레임의 Payload에 IP 패킷이 들어가고, IP 안에 TCP, TCP 안에 TLS Record, TLS 안에 HTTP 요청/응답 데이터가 들어간다고 이해할 수 있다.

## SSL과 TLS

SSL은 TLS의 이전 세대 이름으로 많이 쓰이지만, 현재 문서에서는 TLS 중심으로 쓰는 것이 정확하다.

- SSLv3는 사용하지 않아야 한다.
- TLS 1.0과 TLS 1.1도 공식적으로 deprecated 처리되었다.
- 현재는 TLS 1.2 이상, 가능하면 TLS 1.3을 기준으로 이해하는 것이 좋다.

## TLS의 위치

TLS가 OSI 몇 계층인지 묻는 질문에는 문맥에 따라 답이 달라질 수 있다. 학습용으로는 전송 계층 위, 응용 계층 아래에서 HTTP 같은 응용 데이터를 보호하는 계층으로 이해하면 좋다.

## 암호학과의 연결

TLS는 공개키 기반 인증서, 키 교환, 대칭키 암호, 메시지 인증 같은 개념을 함께 사용한다. 이 구조는 [하이브리드 암호 시스템](../cryptography/hybrid-encryption.md)과 연결된다.

## 참고

- [RFC 7568: Deprecating SSLv3](https://www.rfc-editor.org/rfc/rfc7568)
- [RFC 8996: Deprecating TLS 1.0 and TLS 1.1](https://www.rfc-editor.org/rfc/rfc8996)
