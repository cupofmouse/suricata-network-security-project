# Alert가 발생하지 않았던 원인

## 증상

- fast.log 비어 있음
- eve.json 정상 기록

## 원인

HOME_NET 설정으로 인해 Kali가 내부망으로 인식됨.

## 해결

HOME_NET

192.168.100.10/32

local.rules 추가

사용자 정의 Rule 테스트 성공