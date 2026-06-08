# 네트워크 확인 명령어 정리

네트워크 명령어는 “무슨 IP를 알고 싶은가” 또는 “무슨 상태를 확인하려는가”에 따라 선택해야 한다.

## 목적별 명령어 선택

| 확인하려는 것 | 명령어 |
| --- | --- |
| 내 컴퓨터의 사설 IP | `ipconfig`, `ifconfig`, `ip addr` |
| 내 공인 IP | 포털 사이트에서 `내 IP` 또는 `what is my IP` 검색 |
| 도메인의 IP | `nslookup`, `dig`, `ping` |
| 목적지까지의 중간 라우터 | `tracert`, `traceroute` |
| 현재 연결 중인 상대 IP와 포트 | `netstat`, `ss` |
| 기본 게이트웨이와 라우팅 | `ip route`, `route print` |

## ping

`ping`은 상대가 네트워크 응답을 하는지 확인하는 명령어이다.

```bash
ping naver.com
ping 8.8.8.8
```

도메인으로 ping을 실행하면 먼저 DNS 조회가 일어난다. 그래서 ICMP 응답이 차단되어도 도메인의 IP 주소는 화면에 보일 수 있다.

```text
도메인 입력
-> DNS 조회
-> IP 주소 확인
-> ICMP Echo Request 전송
-> ICMP Echo Reply 수신 시 성공
```

## tracert와 traceroute

목적지까지 가는 경로의 중간 hop을 확인한다.

```powershell
tracert 8.8.8.8
```

```bash
traceroute 8.8.8.8
sudo traceroute -I 8.8.8.8
sudo traceroute -T -p 443 8.8.8.8
```

Windows의 `tracert`는 기본적으로 ICMP를 사용하고, Linux의 `traceroute`는 환경에 따라 UDP probe를 기본으로 사용하는 경우가 많다. 그래서 같은 목적지라도 결과가 다르게 보일 수 있다.

`* * *`는 해당 hop에 대해 보통 3번 시도했지만 응답이 없었다는 뜻이다. 반드시 장애를 의미하지는 않는다. 중간 라우터가 응답하지 않아도 패킷 전달은 계속될 수 있다.

## nslookup

DNS 레코드를 조회한다.

```bash
nslookup naver.com
nslookup -type=mx google.com
```

| 레코드 | 의미 |
| --- | --- |
| A | IPv4 주소 |
| AAAA | IPv6 주소 |
| CNAME | 별칭 |
| MX | 메일 서버 |
| NS | 네임서버 |

## ipconfig, ifconfig, ip addr

Windows에서는 다음 명령을 사용한다.

```powershell
ipconfig
ipconfig /all
```

Linux에서는 다음 명령을 많이 사용한다.

```bash
ip addr
ip route
```

`ifconfig`도 사용할 수 있지만, 최신 Linux에서는 `ip addr`과 `ip route`를 함께 익히는 것이 좋다.

## netstat와 ss

현재 연결 상태와 열린 포트를 확인한다.

```bash
netstat -tuna
sudo netstat -tunap

ss -tuna
sudo ss -tunap
```

| 옵션 | 의미 |
| --- | --- |
| `-t` | TCP 보기 |
| `-u` | UDP 보기 |
| `-n` | 주소와 포트를 숫자로 표시 |
| `-a` | 모든 소켓 보기 |
| `-p` | 프로세스 정보 표시 |

`netstat`은 오래된 도구이고, 요즘 Linux에서는 `ss`를 더 권장하는 경우가 많다.

관련 문서: [IP, ICMP, TTL](./ip-icmp-ttl.md), [TCP Header와 연결 상태](./tcp-header-and-states.md)
