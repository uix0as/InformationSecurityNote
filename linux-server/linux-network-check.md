# Linux에서 네트워크 상태 확인하기

Linux 서버에서는 IP 주소, 라우팅, 열린 포트, 현재 연결 상태를 명령어로 확인할 수 있어야 한다.

## IP 주소 확인

```bash
ip addr
```

확인할 수 있는 것:

- 네트워크 인터페이스 이름
- IPv4/IPv6 주소
- MAC 주소
- 인터페이스 상태

## 기본 게이트웨이 확인

```bash
ip route
```

예시:

```text
default via 192.168.10.1 dev eth0
```

이 경우 외부 네트워크로 나갈 때 `192.168.10.1` 게이트웨이를 사용한다는 뜻이다.

## 열린 포트와 연결 상태 확인

```bash
netstat -tuna
ss -tuna
```

프로세스까지 보려면 관리자 권한이 필요할 수 있다.

```bash
sudo netstat -tunap
sudo ss -tunap
```

## 자주 보이는 상태

| 상태 | 의미 |
| --- | --- |
| LISTEN | 포트를 열고 접속을 기다리는 중 |
| ESTABLISHED | 연결이 성립되어 통신 중 |
| TIME_WAIT | 연결 종료 후 잠시 대기 |
| CLOSE_WAIT | 상대가 종료 요청을 보냈고 로컬 애플리케이션 정리 대기 |
| SYN_RECV | 연결 요청에 응답했고 마지막 ACK를 기다리는 중 |
| FIN_WAIT2 | 내가 종료 요청을 보냈고 상대의 FIN을 기다리는 중 |

## 자주 보이는 주소

| 주소 | 의미 |
| --- | --- |
| `0.0.0.0` | 모든 IPv4 인터페이스에서 접속을 받음 |
| `127.0.0.1` | 내 컴퓨터 자기 자신, 외부 접속 불가 |
| `::` | 모든 IPv6 인터페이스 |

## netstat과 ss

`netstat`은 오래된 도구이고, 최신 Linux에서는 `ss`가 더 빠르고 권장되는 경우가 많다. 하지만 학습 단계에서는 두 명령어를 함께 익히면 문서와 실습 자료를 읽기 쉽다.

관련 문서: [네트워크 확인 명령어 정리](../network/network-commands.md), [TCP Header와 연결 상태](../network/tcp-header-and-states.md)
