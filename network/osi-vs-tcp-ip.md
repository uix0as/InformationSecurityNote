# OSI 7계층과 TCP/IP 모델

OSI 모델은 네트워크 통신을 여러 계층으로 나누어 이해하기 위한 참조 모델이다. 단순히 계층 이름을 외우기보다, 각 계층이 어떤 문제를 해결하는지 보는 것이 중요하다.

## OSI 모델이 등장한 이유

초기 네트워크는 제조사마다 방식이 달라 서로 호환되지 않는 경우가 많았다. OSI 모델은 통신 과정을 계층별로 나누어 각 계층의 역할을 분명하게 만들기 위해 제안되었다.

웹사이트 접속 과정에는 신호 전송, MAC 주소 처리, IP 라우팅, TCP 연결, TLS 암호화, HTTP 요청이 함께 사용된다. 이 복잡한 과정을 계층으로 나누면 어느 부분에서 문제가 생겼는지 더 쉽게 추적할 수 있다.

## OSI 7계층

| 계층 | 이름 | 해결하는 문제 | 예시 |
| --- | --- | --- | --- |
| L1 | Physical | 비트를 실제 신호로 어떻게 보낼 것인가 | 케이블, 허브, 전파 |
| L2 | Data Link | 같은 네트워크에서 누구에게 전달할 것인가 | Ethernet, MAC, Switch |
| L3 | Network | 다른 네트워크까지 어떻게 찾아갈 것인가 | IP, ICMP, Router |
| L4 | Transport | 어떤 프로세스와 통신할 것인가 | TCP, UDP, Port |
| L5 | Session | 통신 상태를 어떻게 관리할 것인가 | 세션 관리 |
| L6 | Presentation | 데이터를 어떤 형식으로 표현할 것인가 | 인코딩, 압축, 암호화 관점 |
| L7 | Application | 사용자 서비스는 무엇인가 | HTTP, DNS, SMTP, SSH |

## TCP/IP 모델

| TCP/IP 계층 | OSI 대응 | 예시 |
| --- | --- | --- |
| Link 또는 Network Access | L1~L2 | Ethernet, Wi-Fi |
| Internet | L3 | IP, ICMP |
| Transport | L4 | TCP, UDP |
| Application | L5~L7 | HTTP, DNS, SMTP |

## 캡슐화

상위 계층 데이터는 하위 계층으로 내려가면서 헤더가 붙는다.

```text
HTTP Data
-> TLS
-> TCP Header
-> IP Header
-> Ethernet Header
-> Physical Signal
```

수신 측에서는 반대로 각 계층의 헤더를 해석하고 제거하면서 원래 데이터를 복원한다. 이를 디캡슐화라고 한다.

## TLS의 위치

TLS가 OSI 몇 계층인지는 문맥에 따라 다르게 설명될 수 있다. 학습 단계에서는 전송 계층 위, 응용 계층 아래에서 HTTP 같은 응용 데이터를 보호하는 보안 계층으로 이해하면 좋다.

관련 문서: [TLS와 HTTPS](../web-security/tls-https.md), [Ethernet Frame과 ARP](./ethernet-arp.md)
