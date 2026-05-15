# InformationSecurityNote

## 보안 솔루션 구조 
```
Internet → F/W → Internal 
```

1. Firewall (침입 차단 시스템) ⇒ Firewalld // iptables
2. IDS (침입 탐지 시스템) ⇒ Snort 
3. IPS (침입 방지 시스템) 
    
    → 침입 탐지 후 차단 
    
4. UTM (통합 위협 관리 시스템) 
    
    → 모든 기능을 장비 하나에 담음 
    
    ex) Firewall, IDS, IPS, VPN, Virus Wall, WAF … 
    

## 관련 법률/정책
    
    정보통신 이용 촉진 및 정보보호 등에 관한 법률 
    
    ⇒ 정보통신망법 
    
    ⇒ 시행령 
    
    개인정보보호법
    
    ⇒ 시행령 
    
    정보통신 기반 보호법
    
    전자서명법
    
    클라우드법
    
    위치정보법
    

## 암호학 기본 개념 

평문(Plaintext)

= Clear Text

암호문(Ciphertext) ← 키 

암호화(Encryption) 

복호화(Decryption) 

암호 해독(cryptanalysis) 

키(Key)

암호시스템(Cryptosystem) 

<aside>
💡

## 암호 알고리즘 분류 

### **양방향 암호 알고리즘** 

P/T → Key → C/T (암호화(Encryption))

C/T → Key → P/T (복호화(Decryption))

→ 대칭키 / 공개키

---

### **단방향 암호 알고리즘** 

⇒ Hash ( 키x 암호화 → 복호화 불가능 ) 

1. 암호학적 해시함수 
    
    MD5(128bit), SHA-1(160bit), SHA-224, 256, 384, 512 bit 
    
    → 해시함수의 충돌성을 방지하기 위해서 (같은 값이 나올 확률 존재)
    
2. 비암호학적 해시함수 
    
    CRC, Checksum, FCS 
    
</aside>

<aside>

💡
## 대칭키 암호 알고리즘 

**대칭키 암호 알고리즘 (암호화 키 == 복호화 키)** 

P/T → Key → C/T

C/T → key → P/T 

→ 속도가 빠름 

1. 블록 암호 알고리즘 (32bit, 64bit, 128bit로 묶어서 함호화) 
    
    DES, AES, IDEA, DSA (외국) / SEED, ARIA, LEA, HIGHT (국내) 
    
2. 스트림 암호 알고리즘 (한 bit, 한 byte씩 암호화) 
    
    RC4
    

---

## **공개키(비대칭키) 암호 알고리즘 (암호화 키 ≠ 복호화 키)** 

→ 공개키를 사용하여 암호화 

→ 속도가 느림 

1. 소인수분해 기반 
    
    **RSA**, RABIN 
    
2. 이산대수 기반 
    
    **ECC**, Elgamal, **DSA**, **Diffie-Hellman**(키교환프로토콜)
    
</aside>

## 하이브리드 암호 시스템 

대칭키 암호 알고리즘 + 공개키 암호 알고리즘 

→ 하이브리드 암호 시스템 

P/T (x 대칭키 암호 알고리즘) → x (공개키 암호 알고리즘) → C/T (x 대칭키 암호 알고리즘)

## 인증서와 전자서명 

CA(공인인증기관) 

공인인증기관의 개인키로 암호화(전자서명)한 것 

→ 공인 인증서 / 공동 인증서 (”이 공개키는 이 사람의 것이다”를 증명하는 전자문서) 

⇒ CA가 자신의 개인키로 서명한 전자문서