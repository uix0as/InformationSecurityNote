# CIA 보안 3요소

CIA는 정보보안에서 자주 사용하는 기본 기준이다. Confidentiality, Integrity, Availability의 약자이며 각각 기밀성, 무결성, 가용성을 뜻한다.

| 요소 | 의미 | 대표 위협 | 대표 대응 |
| --- | --- | --- | --- |
| Confidentiality | 허가된 대상만 정보에 접근할 수 있어야 한다. | Sniffing, Eavesdropping | 암호화, 접근통제 |
| Integrity | 정보가 허가 없이 변조, 삭제, 위조되지 않아야 한다. | 변조, 악성코드 | 해시, 전자서명, 감사 로그 |
| Availability | 필요한 시점에 시스템과 정보를 사용할 수 있어야 한다. | DoS/DDoS, 장애 | 이중화, 백업, 방화벽, 레이트 리밋 |

## 기밀성

기밀성은 데이터를 볼 수 있는 사람을 제한하는 성질이다. 네트워크에서 데이터가 노출될 수 있다면 암호화를 적용하고, 시스템에서는 계정 권한과 접근 제어를 설정한다.

기밀성은 [대칭키 암호와 공개키 암호](../cryptography/symmetric-asymmetric-encryption.md), [TLS/HTTPS](../web-security/tls-https.md)와 연결된다.

## 무결성

무결성은 데이터가 원래 상태 그대로 유지되었는지 확인하는 성질이다. 해시 함수는 파일이나 메시지가 바뀌었는지 확인하는 데 사용되고, 전자서명은 누가 서명했는지도 함께 검증할 수 있게 한다.

무결성은 [해시 함수](../cryptography/hash-functions.md), [인증서와 전자서명](../cryptography/certificates-digital-signatures.md)과 연결된다.

## 가용성

가용성은 시스템이 정상적으로 동작하고 필요한 사용자가 접근할 수 있는 상태를 말한다. 서비스 거부 공격, 장비 장애, 과부하, 설정 오류는 모두 가용성에 영향을 줄 수 있다.

보안은 세 요소 중 하나만 보는 것이 아니라, 상황에 맞게 균형을 맞추는 과정이다.
