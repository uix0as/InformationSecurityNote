# SELinux와 vsftpd 실습 메모

이 문서는 Rocky Linux 실습 중 SELinux와 vsftpd를 함께 다룰 때 헷갈리기 쉬운 부분을 정리한 것이다.

## SELinux

SELinux는 Linux에서 보안 정책을 강제로 적용하는 기능이다. 일반적인 파일 권한이 허용하더라도, SELinux 정책상 허용되지 않은 접근이면 차단될 수 있다.

예를 들어 서버 프로그램이 특정 디렉터리만 읽어야 하는데 다른 위치에 접근하려고 하면 SELinux가 막을 수 있다.

## setenforce

```bash
getenforce
sudo setenforce 0
sudo setenforce 1
```

| 명령어 | 의미 |
| --- | --- |
| `getenforce` | 현재 SELinux 상태 확인 |
| `setenforce 0` | Permissive 모드로 변경 |
| `setenforce 1` | Enforcing 모드로 변경 |

`setenforce 0`은 SELinux를 완전히 끄는 것이 아니라 Permissive 모드로 바꾸는 것이다. 정책 위반을 차단하지 않고 로그만 남기는 진단용 상태로 이해해야 한다.

운영 환경에서 `setenforce 0`을 최종 해결책으로 두면 안 된다. 실습 중 원인 확인에만 사용하고, 문제가 SELinux 때문이라면 context나 boolean을 올바르게 조정한 뒤 Enforcing으로 되돌리는 흐름이 좋다.

## vsftpd

vsftpd는 Very Secure FTP Daemon의 줄임말로, FTP 접속을 받아 파일 업로드/다운로드를 처리하는 서버 daemon이다.

기본 명령 예시:

```bash
sudo dnf install vsftpd
sudo systemctl start vsftpd
sudo systemctl enable vsftpd
sudo systemctl status vsftpd
sudo systemctl restart vsftpd
```

대표 설정 파일:

```text
/etc/vsftpd/vsftpd.conf
```

설정 예시:

```text
anonymous_enable=NO
local_enable=YES
write_enable=YES
```

## FTP 보안 주의

기본 FTP는 계정 정보와 데이터가 평문으로 전송될 수 있어 보안상 위험하다. 실습용으로 개념을 익히는 것과 운영 환경에서 사용하는 것은 구분해야 한다.

- FTP: 기본적으로 평문 전송 위험이 있음
- FTPS: FTP에 TLS를 적용
- SFTP: SSH 기반 파일 전송, FTP와 다른 프로토콜

## 실습 흐름 예시

```bash
getenforce
sudo setenforce 0
# 접속 또는 업로드 테스트
sudo setenforce 1
```

이 흐름은 “SELinux가 원인인지 확인”하기 위한 임시 진단이다.

## 참고

- [setenforce manual](https://man7.org/linux/man-pages/man8/setenforce.8.html)
- [Red Hat SELinux documentation](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/10/html-single/using_selinux/using_selinux)
- [Rocky Linux vsftpd documentation](https://docs.rockylinux.org/guides/file_sharing/secure_ftp_server_vsftpd/)
