# IP, ICMP, TTL

IP는 목적지 네트워크까지 패킷을 전달하기 위한 네트워크 계층 프로토콜이다. ICMP는 네트워크 상태나 오류를 알려주는 제어 메시지 프로토콜이고, TTL은 패킷이 무한히 떠도는 것을 막기 위한 IP 헤더의 필드이다.

## IP의 역할

IP 주소는 장치가 어느 네트워크에 있는지 나타내는 주소이다. MAC 주소가 같은 링크에서 다음 장비를 찾는 데 쓰인다면, IP 주소는 최종 목적지까지 라우팅하는 데 쓰인다.

```text
Source IP      = 출발지 주소
Destination IP = 최종 목적지 주소
TTL            = 남은 hop 수
Protocol       = IP 안에 들어 있는 상위 프로토콜
```

`Protocol` 필드는 IP Payload에 TCP, UDP, ICMP 중 무엇이 들어 있는지 알려준다.

## ICMP

ICMP(Internet Control Message Protocol)는 데이터를 전달하는 주 프로토콜이라기보다, 네트워크 상태와 오류를 알려주는 신호 역할을 한다.

대표 메시지:

- Echo Request
- Echo Reply
- Destination Unreachable
- Time Exceeded

`ping`은 ICMP Echo Request와 Echo Reply를 사용한다. ICMP는 TCP/UDP처럼 포트 번호를 사용하지 않는다.

## TTL

TTL(Time To Live)은 이름과 달리 실제로는 패킷이 지날 수 있는 최대 hop 수처럼 이해하면 쉽다. 라우터를 하나 지날 때마다 TTL은 1 감소한다.

```text
출발 TTL 5
라우터 1 -> TTL 4
라우터 2 -> TTL 3
라우터 3 -> TTL 2
```

TTL이 0이 되면 라우터는 패킷을 폐기하고 보통 ICMP Time Exceeded 메시지를 보낸다.

## traceroute와 TTL

traceroute는 TTL을 1부터 늘려 가며 패킷을 보내 중간 라우터를 추적한다.

```text
TTL=1 -> 첫 번째 라우터에서 만료
TTL=2 -> 두 번째 라우터에서 만료
TTL=3 -> 세 번째 라우터에서 만료
...
```

TTL을 이용한 경로 추적은 [네트워크 확인 명령어 정리](./network-commands.md)에서 함께 다룬다.

## ping 결과의 TTL

예를 들어 다음 결과가 있다고 하자.

```text
Reply from 8.8.8.8: bytes=32 time=40ms TTL=113
```

여기서 `TTL=113`은 응답 패킷이 내 컴퓨터에 도착했을 때 남아 있던 TTL이다. 상대가 처음에 TTL 128로 보냈다고 추정하면 돌아오는 경로에서 약 15 hop을 지났다고 추정할 수 있다. 다만 가는 길과 오는 길이 다를 수 있으므로 traceroute 결과와 정확히 일치하지 않을 수 있다.
