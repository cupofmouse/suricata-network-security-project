# Week 1

## 목표

- 프로젝트 구조 생성
- GitHub 저장소 생성
- Ubuntu Server 준비
- Kali Linux 확인

---

## 진행 내용
프로젝트 디렉토리 생성

Git 저장소 초기화

GitHub Repository 생성

# Week 1 완료

### 실습 환경 구축
- VirtualBox 네트워크 구성
  - Adapter 1: NAT
  - Adapter 2: Internal Network (SecurityLab)

### Ubuntu (IDS Server)
- Netplan을 이용한 고정 IP 설정
- 192.168.100.10/24

### Kali (Attacker)
- NetworkManager를 이용한 고정 IP 설정
- 192.168.100.20/24

### 검증
- Ubuntu ↔ Kali Ping 성공
- Kali → Ubuntu SSH 접속 성공


### Suricata 설치
- Suricata 7 설치
- Emerging Threats Open Rule 적용
- 서비스 정상 실행 확인
- AF_PACKET 기반 인터페이스(enp0s8) 모니터링

### 문제 해결
Suricata는 정상 실행되었지만 Alert가 발생하지 않는 문제가 있었다.

원인을 분석한 결과 HOME_NET이
192.168.0.0/16으로 설정되어 Kali도 내부망으로 인식되고 있었다.

ET Rule은 대부분
EXTERNAL_NET → HOME_NET
형태이므로 Rule이 매칭되지 않았다.

HOME_NET을
192.168.100.10/32
로 수정하여 Kali를 EXTERNAL_NET으로 인식하도록 변경하였다.

또한 local.rules를 추가하여 사용자 정의 Rule을 분리하였다.

### 테스트
- Ping 테스트
- Nmap 테스트
- 사용자 정의 Nmap Rule 정상 탐지
- fast.log Alert 생성 확인

## 느낀 점

단순히 설치보다 Rule과 네트워크 정책(HOME_NET, EXTERNAL_NET)이 IDS 탐지에 매우 중요한 요소임을 이해하였다.