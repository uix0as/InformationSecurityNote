# Ethernet Frame과 ARP

Ethernet은 LAN 환경에서 널리 사용되는 데이터 링크 계층 프로토콜이다. 같은 네트워크 구간에서 MAC 주소를 기준으로 프레임을 전달한다.

## Ethernet Frame 구조

```text
+----------------+----------------+------+-----------+------+
| Destination MAC| Source MAC     | Type | Payload   | FCS  |
|     6 Byte     |    6 Byte      |2 Byte|46~1500Byte|4 Byte|
+----------------+----------------+------+-----------+------+
```

| 필드 | 크기 | 의미 |
| --- | --- | --- |
| Destination MAC | 6B | 다음에 프레임을 받을 장치의 MAC 주소 |
| Source MAC | 6B | 프레임을 보낸 장치의 MAC 주소 |
| EtherType | 2B | Payload에 들어 있는 프로토콜 종류 |
| Payload | 46~1500B | IP, ARP, IPv6 등의 데이터 |
| FCS | 4B | CRC 기반 오류 검출 값 |

대표적인 EtherType은 다음과 같다.

| 값 | 의미 |
| --- | --- |
| `0x0800` | IPv4 |
| `0x0806` | ARP |
| `0x86DD` | IPv6 |
| `0x8100` | VLAN |

## ARP의 역할

ARP(Address Resolution Protocol)는 IPv4 주소를 MAC 주소로 변환하기 위해 사용된다.

```text
IP 주소 -> ARP 조회 -> MAC 주소
```

예를 들어 내 컴퓨터가 `192.168.0.20`으로 통신하려면 Ethernet 프레임의 Destination MAC을 알아야 한다. 이때 ARP Request를 브로드캐스트로 보내고, 해당 IP를 가진 장치가 ARP Reply로 자신의 MAC 주소를 알려준다.

## ARP Packet 구조

| 필드 | 크기 | 의미 |
| --- | --- | --- |
| Hardware Type | 2B | Ethernet이면 `1` |
| Protocol Type | 2B | IPv4이면 `0x0800` |
| Hardware Size | 1B | MAC 주소 길이, Ethernet은 6 |
| Protocol Size | 1B | IPv4 주소 길이, 4 |
| Opcode | 2B | Request는 1, Reply는 2 |
| Sender MAC | 6B | 보내는 장치의 MAC 주소 |
| Sender IP | 4B | 보내는 장치의 IP 주소 |
| Target MAC | 6B | 대상 MAC 주소 |
| Target IP | 4B | 대상 IP 주소 |

ARP Request에서는 아직 대상 MAC을 모르므로 Target MAC을 `00:00:00:00:00:00`으로 채우고, Ethernet Destination MAC은 브로드캐스트 주소인 `FF:FF:FF:FF:FF:FF`를 사용한다.

## ARP는 IP 안에 들어가지 않는다

ARP는 IP 패킷 안에 들어가는 것이 아니라 Ethernet Payload에 직접 들어간다.

```text
ARP   : Ethernet -> ARP
ping  : Ethernet -> IP -> ICMP
HTTPS : Ethernet -> IP -> TCP -> TLS -> HTTP
```

## MAC은 다음 hop, IP는 최종 목적지

MAC 주소는 같은 링크에서 바로 다음 장비를 가리킨다. 라우터를 지날 때마다 Ethernet 헤더는 새로 만들어지고 MAC 주소도 바뀐다.

반면 IP 목적지는 최종 목적지를 가리키므로 라우팅되는 동안 대체로 유지된다. 다만 NAT 구간에서는 Source IP가 바뀔 수 있다.

관련 문서: [IP, ICMP, TTL](./ip-icmp-ttl.md), [OSI 7계층과 TCP/IP 모델](./osi-vs-tcp-ip.md)
