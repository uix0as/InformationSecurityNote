# TCP, UDP, 포트 번호

TCP와 UDP는 전송 계층 프로토콜이다. IP가 목적지 장치를 찾는다면, 포트 번호는 장치 안에서 어떤 프로그램과 통신할지 구분한다.

## TCP와 UDP 비교

| 구분 | TCP | UDP |
| --- | --- | --- |
| 연결 방식 | 연결 지향 | 비연결 |
| 신뢰성 | 순서 보장, 재전송, 흐름 제어 | 자체적으로 보장하지 않음 |
| 속도/오버헤드 | 상대적으로 무겁다 | 상대적으로 가볍다 |
| 사용 예시 | HTTP, HTTPS, SSH, FTP, SMTP | DNS, DHCP, SNMP, 스트리밍 일부 |

## 포트 번호

| 범위 | 이름 | 설명 |
| --- | --- | --- |
| 0~1023 | System 또는 Well-Known Ports | 잘 알려진 서비스에 할당되는 범위 |
| 1024~49151 | User 또는 Registered Ports | 등록 가능한 사용자 포트 범위 |
| 49152~65535 | Dynamic 또는 Private Ports | 클라이언트 임시 포트 등에 사용 |

IANA는 포트 범위를 `System Ports`, `User Ports`, `Dynamic and/or Private Ports`로 구분한다.

## 주요 포트 예시

| 프로토콜 | 포트 | 전송 계층 |
| --- | --- | --- |
| FTP Data | 20 | TCP |
| FTP Control | 21 | TCP |
| SSH | 22 | TCP |
| Telnet | 23 | TCP |
| SMTP | 25 | TCP |
| DNS | 53 | UDP/TCP |
| DHCP | 67, 68 | UDP |
| TFTP | 69 | UDP |
| HTTP | 80 | TCP |
| POP3 | 110 | TCP |
| IMAP | 143 | TCP |
| SNMP | 161, 162 | UDP |
| HTTPS | 443 | TCP |

## DNS는 UDP와 TCP를 모두 쓴다

일반적인 DNS 조회는 UDP 53을 많이 사용한다. 하지만 응답이 크거나, Zone Transfer, DNSSEC, 일부 운영 환경, DoT/DoH 같은 별도 방식에서는 TCP 또는 TLS/HTTPS 기반 통신도 사용된다.

따라서 “DNS는 현재 TCP 비율이 더 높다”처럼 단정하기보다, 어떤 DNS 사용 사례를 말하는지 구분해서 설명하는 것이 안전하다.

## 참고

- [IANA Service Name and Transport Protocol Port Number Registry](https://www.iana.org/assignments/service-names-port-numbers)
