# Rocky Linux 네트워크 명령어 실습

Rocky Linux에서 네트워크 상태를 확인하기 위해 사용한 명령어와 결과 해석 기준을 정리한다.

## 실습 목적

- 내 IP 주소와 기본 게이트웨이를 확인한다.
- 목적지까지의 경로를 traceroute로 확인한다.
- 열린 포트와 현재 연결 상태를 netstat/ss로 확인한다.
- `* * *`, `LISTEN`, `ESTABLISHED`, `SYN_RECV`, `FIN_WAIT2` 같은 출력의 의미를 이해한다.

## IP 주소 확인

```bash
ip addr
ip route
```

확인할 내용:

- 어떤 인터페이스가 활성화되어 있는가
- 내 사설 IP는 무엇인가
- 기본 게이트웨이는 어디인가

## ping

```bash
ping 8.8.8.8
ping google.com
```

`ping google.com`은 먼저 DNS 조회로 IP를 확인한 뒤 ICMP Echo Request를 보낸다. ping 응답이 막혀도 DNS 조회로 IP가 표시될 수 있다.

## traceroute

```bash
traceroute 8.8.8.8
sudo traceroute -I 8.8.8.8
sudo traceroute -T -p 443 8.8.8.8
```

출력 예시:

```text
1  _gateway (172.16.72.2)  0.485 ms  0.418 ms  0.404 ms
2  10.5.0.1               40.626 ms 40.604 ms 44.984 ms
6  * 63.220.71.207        67.169 ms *
7  * * *
8  * * *
9  8.8.8.8                110.142 ms 110.311 ms 110.297 ms
```

해석:

- 각 줄은 하나의 hop이다.
- 시간 값 3개는 보통 해당 hop에 대해 3번 측정한 결과이다.
- `* * *`는 3번의 probe에 응답이 없었다는 뜻이다.
- 중간 hop이 응답하지 않아도 마지막 목적지에 도착하면 패킷 전달은 계속된 것이다.
- Linux `traceroute`와 Windows `tracert`는 기본 probe 방식이 다를 수 있어 결과가 다르게 보일 수 있다.

## netstat

```bash
netstat -tuna
sudo netstat -tunap
```

옵션:

| 옵션 | 의미 |
| --- | --- |
| `-t` | TCP 보기 |
| `-u` | UDP 보기 |
| `-n` | 숫자 형태로 표시 |
| `-a` | 모든 소켓 보기 |
| `-p` | 프로세스 표시 |

## ss

```bash
ss -tuna
sudo ss -tunap
ss -ant state syn-recv
ss -ant state fin-wait-2
```

`ss`는 최신 Linux에서 `netstat` 대신 자주 사용하는 도구이다.

## TCP 상태 해석

| 상태 | 해석 |
| --- | --- |
| LISTEN | 포트를 열고 접속을 기다리는 중 |
| ESTABLISHED | 연결이 성립되어 통신 중 |
| SYN_RECV | SYN+ACK 이후 마지막 ACK를 기다리는 중 |
| FIN_WAIT2 | 내가 종료 요청을 보냈고 상대의 FIN을 기다리는 중 |

SYN_RECV나 FIN_WAIT2가 잠깐 보이는 것은 정상이다. 하지만 오래 많이 쌓이면 접속 요청 급증, 네트워크 문제, 애플리케이션 종료 처리 문제 등을 확인해야 한다.

관련 문서: [네트워크 확인 명령어 정리](../network/network-commands.md), [Linux에서 네트워크 상태 확인하기](../linux-server/linux-network-check.md)
