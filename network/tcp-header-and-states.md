# TCP Header와 연결 상태

TCP는 연결 지향 프로토콜이다. 데이터를 순서대로 전달하고, 손실을 감지하고, 필요한 경우 재전송하며, 흐름 제어와 혼잡 제어를 수행한다.

## TCP Segment 구조

```text
  0                   15 16                  31
+----------------------+----------------------+
|     Source Port      |   Destination Port   |
+----------------------+----------------------+
|                Sequence Number              |
+---------------------------------------------+
|             Acknowledgment Number           |
+----+---+------------------------------------+
|HLEN|RSV| Flags                              |
+----+---+------------------------------------+
|              Window Size                    |
+---------------------------------------------+
|              Checksum                       |
+---------------------------------------------+
|             Urgent Pointer                  |
+---------------------------------------------+
|                Options                      |
+---------------------------------------------+
|                 Data                        |
+---------------------------------------------+
```

TCP 헤더의 최소 크기는 20 Byte이고, Options가 있으면 더 커질 수 있다.

## 주요 필드

| 필드 | 역할 |
| --- | --- |
| Source Port | 출발지 애플리케이션 포트 |
| Destination Port | 목적지 애플리케이션 포트 |
| Sequence Number | 현재 세그먼트 데이터의 첫 번째 바이트 번호 |
| Acknowledgment Number | 다음에 받고 싶은 바이트 번호 |
| Header Length | TCP 헤더 크기 |
| Flags | SYN, ACK, FIN, RST, PSH, URG 등 제어 비트 |
| Window Size | 수신 가능한 데이터 양을 알려주는 흐름 제어 값 |
| Checksum | TCP 헤더와 데이터 오류 검출 |
| Urgent Pointer | URG 플래그가 있을 때 긴급 데이터 위치 |
| Options | MSS, Window Scale, SACK, Timestamp 등 |

## Sequence Number와 ACK Number

Sequence Number는 데이터의 순서를 맞추기 위한 번호이다. 인터넷에서는 패킷이 보낸 순서대로 도착한다는 보장이 없으므로, TCP는 이 번호를 이용해 재조립, 중복 제거, 손실 감지를 수행한다.

ACK Number는 “받은 번호”가 아니라 “다음에 받고 싶은 번호”이다.

```text
상대가 SEQ=1000부터 100 Byte 전송
수신자는 ACK=1100 전송
의미: 1000~1099까지 받았고, 1100부터 보내라
```

## 3-Way Handshake

```text
Client                      Server
SYN, SEQ=100        ->
                     <-    SYN+ACK, SEQ=500, ACK=101
ACK, ACK=501        ->

TCP 연결 성립
```

## TCP 상태

| 상태 | 의미 |
| --- | --- |
| LISTEN | 서버가 접속을 기다리는 중 |
| SYN_RECV | SYN을 받고 SYN+ACK를 보낸 뒤 마지막 ACK를 기다리는 중 |
| ESTABLISHED | 연결이 성립되어 통신 중 |
| FIN_WAIT1 | 내가 FIN을 보내고 ACK를 기다리는 중 |
| FIN_WAIT2 | 내 FIN에 대한 ACK를 받았고 상대의 FIN을 기다리는 중 |
| TIME_WAIT | 종료 후 지연된 패킷 처리를 위해 잠시 대기 |
| CLOSE_WAIT | 상대가 종료 요청을 보냈고 내 애플리케이션 정리를 기다리는 중 |

## 상태 확인 예시

```bash
netstat -ant | grep SYN_RECV
netstat -ant | grep FIN_WAIT2

ss -ant state syn-recv
ss -ant state fin-wait-2
```

SYN_RECV가 잠깐 보이는 것은 정상이다. 하지만 매우 많이 쌓이면 접속 요청 급증, 네트워크 문제, SYN flood 가능성, backlog 부족 등을 점검할 수 있다.

FIN_WAIT2가 오래 남거나 많이 쌓이면 상대 프로그램이 연결을 제대로 닫지 않거나 애플리케이션/네트워크 문제가 있을 수 있다.

관련 문서: [Linux에서 네트워크 상태 확인하기](../linux-server/linux-network-check.md)
