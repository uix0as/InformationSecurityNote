# VPN 개념과 계층

VPN(Virtual Private Network)은 공용망에서 사설망처럼 안전하게 통신하기 위한 기술이다. 핵심은 터널링, 인증, 암호화, 무결성이다.

## 핵심 개념

| 개념 | 의미 |
| --- | --- |
| Tunneling | 원래 패킷을 다른 패킷 안에 캡슐화해 운반 |
| Authentication | 사용자나 장비가 누구인지 확인 |
| Encryption | 통신 내용을 암호화해 도청을 방지 |
| Integrity | 통신 내용이 변조되었는지 확인 |

## 계층별 예시

| 방식 | 주로 보는 계층 | 설명 |
| --- | --- | --- |
| IPsec VPN | L3 | IP 패킷을 보호한다. IKE, AH, ESP 등이 관련된다. |
| L2TP/IPsec | L2/L3 | L2TP로 PPP 프레임을 터널링하고, 보통 IPsec과 함께 보호한다. |
| TLS VPN | L4~L7 관점 | TLS를 이용해 사용자나 애플리케이션 접근을 보호한다. |
| PPTP | L2 | 오래된 방식이며 현재 보안상 권장되지 않는다. |

## L2TP 주의점

L2TP 자체는 강한 암호화를 제공하는 보안 프로토콜로 보기보다, PPP 프레임을 터널링하는 프로토콜로 이해하는 편이 정확하다. 그래서 실제 VPN 설명에서는 보통 `L2TP/IPsec` 형태로 함께 다룬다.

## PPTP 주의점

PPTP는 오래된 방식이고 알려진 보안 약점이 있어 새 구성에서는 사용하지 않는 것이 좋다.

## 참고

- [RFC 2661: Layer Two Tunneling Protocol](https://www.rfc-editor.org/info/rfc2661)
