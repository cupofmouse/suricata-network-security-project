# 시스템 구성

Attacker

- Kali Linux

↓

IDS

- Ubuntu Server
- Suricata

↓

Log Analysis

- Python

↓

Automatic Response

- iptables

↓

(7주차)

Elastic Stack



Host PC
│
├── VirtualBox
│
├── Ubuntu (IDS Server)
│   ├── NAT : DHCP
│   └── Internal : 192.168.100.10
│
└── Kali (Attacker)
    ├── NAT : DHCP
    └── Internal : 192.168.100.20


## Week 2

                 Internet
                     │
                 NAT Adapter
                     │
      ┌──────────────────────────┐
      │      Ubuntu Desktop      │
      │        IDS Server        │
      │--------------------------│
      │ Suricata                 │
      │ local.rules              │
      │ ET Open Rules            │
      │ fast.log                 │
      │ eve.json                 │
      └───────────┬──────────────┘
                  │
      Internal Network
      192.168.100.0/24
                  │
      ┌───────────┴──────────────┐
      │      Kali Linux          │
      │      Attacker            │
      │--------------------------│
      │ nmap                     │
      │ ping                     │
      │ ssh                      │
      └──────────────────────────┘

HOME_NET
192.168.100.10/32

EXTERNAL_NET
!HOME_NET