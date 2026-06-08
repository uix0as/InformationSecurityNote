<div align="center">

# Security Study Notes

네트워크와 보안 기초를 연결해서 정리한 정보보안 학습 노트입니다.

<img src="https://img.shields.io/badge/Security-Study-1F2937?style=for-the-badge">
<img src="https://img.shields.io/badge/Network-Basics-2563EB?style=for-the-badge">
<img src="https://img.shields.io/badge/Linux-Command-374151?style=for-the-badge">
<img src="https://img.shields.io/badge/Cryptography-Notes-5B5FC7?style=for-the-badge">
<img src="https://img.shields.io/badge/Markdown-Docs-111827?style=for-the-badge">
<img src="https://img.shields.io/badge/Defensive-Learning-2E8B57?style=for-the-badge">

</div>

## 소개

보안 개념을 네트워크 구조, 패킷 흐름, Linux 명령어 결과와 함께 이해하는 데 초점을 두며,
정보보안 학습 및 방어적 이해를 목적으로 합니다.

허가되지 않은 시스템에 대한 공격, 침투, 스캔을 목적으로 하지 않습니다.

## 다루는 내용

- 보안 기본 개념과 CIA 보안 3요소
- 국내 정보보안 관련 법률의 학습용 개요
- 암호학 기초, 해시, 대칭키/공개키, 인증서와 전자서명
- OSI 7계층, TCP/IP, Ethernet, ARP, IP, ICMP, TCP, UDP
- TLS/HTTPS와 VPN
- Linux 서버에서 네트워크 상태를 확인하는 명령어
- PTES 모의해킹 절차의 방어적 개요
- Rocky Linux 기반 네트워크 명령어 실습 메모 등 

## 폴더 구조

```text
security-study/
├── README.md
├── foundations/
│   ├── security-solutions.md
│   ├── cia-triad.md
│   └── korean-security-laws.md
├── cryptography/
│   ├── cryptography-basics.md
│   ├── hash-functions.md
│   ├── symmetric-asymmetric-encryption.md
│   ├── hybrid-encryption.md
│   └── certificates-digital-signatures.md
├── network/
│   ├── osi-vs-tcp-ip.md
│   ├── ethernet-arp.md
│   ├── ip-icmp-ttl.md
│   ├── tcp-udp-ports.md
│   ├── tcp-header-and-states.md
│   ├── network-commands.md
│   └── vpn.md
├── web-security/
│   └── tls-https.md
├── linux-server/
│   ├── linux-network-check.md
│   └── selinux-vsftpd.md
├── pentest-methodology/
│   └── ptes-overview.md
└── labs/
    ├── README.md
    └── rocky-linux-network-practice.md
```

## 문서 목록

### Foundations

- [보안 솔루션 기본 구조](./foundations/security-solutions.md)
- [CIA 보안 3요소](./foundations/cia-triad.md)
- [국내 정보보안 관련 법률 정리](./foundations/korean-security-laws.md)

### Cryptography

- [암호학 기초 용어](./cryptography/cryptography-basics.md)
- [해시 함수와 무결성 검증](./cryptography/hash-functions.md)
- [대칭키 암호와 공개키 암호](./cryptography/symmetric-asymmetric-encryption.md)
- [하이브리드 암호 시스템](./cryptography/hybrid-encryption.md)
- [인증서와 전자서명](./cryptography/certificates-digital-signatures.md)

### Network

- [OSI 7계층과 TCP/IP 모델](./network/osi-vs-tcp-ip.md)
- [Ethernet Frame과 ARP](./network/ethernet-arp.md)
- [IP, ICMP, TTL](./network/ip-icmp-ttl.md)
- [TCP, UDP, 포트 번호](./network/tcp-udp-ports.md)
- [TCP Header와 연결 상태](./network/tcp-header-and-states.md)
- [네트워크 확인 명령어 정리](./network/network-commands.md)
- [VPN 개념과 계층](./network/vpn.md)

### Web Security

- [TLS와 HTTPS](./web-security/tls-https.md)

### Linux Server

- [Linux에서 네트워크 상태 확인하기](./linux-server/linux-network-check.md)
- [SELinux와 vsftpd 실습 메모](./linux-server/selinux-vsftpd.md)

### Pentest Methodology

- [PTES 모의해킹 절차 개요](./pentest-methodology/ptes-overview.md)

### Labs

- [실습 메모 모음](./labs/README.md)
- [Rocky Linux 네트워크 명령어 실습](./labs/rocky-linux-network-practice.md)

## 참고한 사이트

학습 중 개념 확인과 Markdown 작성에 참고한 문서입니다.

- [GitHub Docs - Markdown 작성 문법](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [GitHub Docs - Mermaid 다이어그램 작성](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-diagrams)
- [Shields.io - README Badge 생성](https://shields.io/)
- [OWASP Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [MDN Web Docs - Web Security](https://developer.mozilla.org/en-US/docs/Web/Security)
- [RFC Editor](https://www.rfc-editor.org/)

## 앞으로 추가할 내용

- DNS 레코드와 캐시 흐름
- UDP Header 구조
- IP Header 주요 필드
- 클라우드 보안 기초: 책임 공유 모델, IAM, 네트워크 보안 그룹
- 가상화와 컨테이너 기초

## 주의사항

- 이 저장소는 학습 노트이며 법률, 보안 진단, 운영 보안에 대한 최종 판단 기준이 아닙니다.
- 법률 문서는 최신 시행일과 조문을 국가법령정보센터에서 다시 확인해야 합니다.
- 실습은 개인 학습 환경 또는 명시적으로 허가된 환경에서만 수행합니다.
- 실제 IP, 계정명, 내부망 정보, 스크린샷 개인정보는 공개 저장소에 올리지 않습니다.

## 체크리스트

- [ ] 기술적으로 틀린 내용이 없는지 확인했다.
- [ ] 확인이 필요한 내용은 `확인 필요`로 따로 표시했다.
- [ ] 위험한 공격 절차가 과하게 포함되어 있지 않은지 확인했다.
- [ ] 학습 및 방어적 이해 목적임을 README에 명확히 적었다.
- [ ] 원본에 없는 실무 경험, 프로젝트 경험, 수상 경력, 자격증을 추가하지 않았다.
- [ ] 파일명과 폴더명이 소문자와 하이픈 기준으로 일관적인지 확인했다.
- [ ] 내부 링크가 깨지지 않는지 확인했다.
- [ ] Mermaid 다이어그램이 GitHub에서 정상 표시되는지 확인했다.
- [ ] 코드블록의 언어 표시가 적절한지 확인했다.
- [ ] 명령어에 공백 오타가 없는지 확인했다.
- [ ] 실제 IP, 계정명, 내부망 정보, 스크린샷 개인정보가 노출되지 않는지 확인했다.
- [ ] Markdown 표가 깨지지 않는지 확인했다.
