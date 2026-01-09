---
layout: post
title: "Cloud 필수 용어 정리 - 1 (Kor.ver)"
date: 2025-11-19
categories:
  - "Cloud" 
tags: [클라우드, 기초, Korean] 
---
# 🧱 1️⃣ 가상화 및 컴퓨팅 (Virtualization & Compute)

### 1 Virtual Machine (가상 머신)
- **meaning**: 실제 컴퓨터 안에서 또 다른 가상의 컴퓨터를 만들어 사용하는 기술.  
- **simple explanation**: 한 대의 컴퓨터 안에 여러 개의 컴퓨터를 띄워 쓰는 것.  
- **example**: AWS EC2, VMware, VirtualBox.  
- **sample image**:
  ```
  ┌──────────────┐
  │ Host OS      │
  │  ┌──────────┐│
  │  │ VM1      ││
  │  │ (Ubuntu) ││
  │  ├──────────┤│
  │  │ VM2      ││
  │  │ (CentOS) ││
  │  └──────────┘│
  └──────────────┘
  ```

---

### 2️ Host OS / Guest OS
- **meaning**: Host는 실제 컴퓨터의 운영체제, Guest는 그 위에서 돌아가는 가상의 운영체제.  
- **simple explanation**: Host는 주인, Guest는 손님 컴퓨터.  
- **example**: Host OS가 Windows일 때 Guest OS로 Ubuntu를 설치 가능.  
- **sample image**:
  ```
  [Host: Windows]
      ↓ VirtualBox
  [Guest: Ubuntu]
  ```

---

### 3️ Bare Metal (베어메탈)
- **meaning**: 가상화 없이 직접 물리 서버에 OS를 설치해 사용하는 방식.  
- **simple explanation**: 아무 것도 깔리지 않은 생컴퓨터에 직접 OS 설치하는 것.  
- **example**: Naver Cloud의 Bare Metal Server.  
- **sample image**:
  ```
  [물리 서버] → [운영체제 설치] → [애플리케이션 실행]
  ```

---

### 4️ Virtual Private Server (VPS)
- **meaning**: 한 물리 서버를 가상으로 나누어 여러 사용자가 각자의 서버처럼 사용하는 형태.  
- **simple explanation**: 한 건물(물리 서버)을 여러 세입자가 방(가상서버)으로 나눠 쓰는 것.  
- **example**: AWS Lightsail, Vultr VPS.  
- **sample image**:
  ```
  [물리 서버]
    ├─ VPS 1 (User A)
    ├─ VPS 2 (User B)
    └─ VPS 3 (User C)
  ```

---

### 5️ On-Premise (온프레미스)
- **meaning**: 클라우드가 아닌, 직접 회사 내에서 서버를 운영하는 방식.  
- **simple explanation**: 내 사무실 안에 서버실을 직접 꾸려 관리하는 것.  
- **example**: 기업 내 데이터센터.  
- **sample image**:
  ```
  🏢 회사 서버실 → 🧑‍💻 직접 관리 & 유지보수
  ```

---

### 6️ Hypervisor (하이퍼바이저)
- **meaning**: 가상 머신을 만들고 관리하는 소프트웨어.  
- **simple explanation**: 컴퓨터 안에서 여러 가상 컴퓨터를 조정하는 관리자.  
- **example**: VMware ESXi, KVM, Hyper-V.  
- **sample image**:
  ```
  [하드웨어]
    ↓
  [Hypervisor]
    ↓
  ├─ VM1
  ├─ VM2
  └─ VM3
  ```

---

### 7️ Instance (인스턴스)
- **meaning**: 클라우드에서 생성한 가상의 컴퓨터 한 대.  
- **simple explanation**: AWS에서 생성한 나만의 서버 한 대.  
- **example**: EC2 Instance, NCP Server Instance.  
- **sample image**:
  ```
  AWS → Launch Instance → 내 서버 생성
  ```

---

### 8️ vCPU (Virtual CPU)
- **meaning**: 물리 CPU를 여러 개의 가상 CPU로 나눈 것.  
- **simple explanation**: 한 개의 CPU를 여러 명이 나눠 쓰는 구조.  
- **example**: t2.micro 인스턴스 = 1 vCPU.  
- **sample image**:
  ```
  [물리 CPU]
    ├─ vCPU #1
    ├─ vCPU #2
    └─ vCPU #3
  ```

---

### 9️ Snapshot (스냅샷)
- **meaning**: 현재 서버 상태를 그대로 복사해 저장해두는 기능.  
- **simple explanation**: 지금 이 순간의 서버 사진을 찍어두는 것.  
- **example**: AWS EC2 Snapshot, DB Snapshot.  
- **sample image**:
  ```
  [현재 서버 상태] → 📸 Snapshot 저장 → [복원 시 사용]
  ```

---

### 10 Image (이미지)
- **meaning**: 서버의 OS와 설정을 모두 포함한 복제 템플릿.  
- **simple explanation**: 새 서버를 찍어내는 '틀' 역할.  
- **example**: Amazon Machine Image (AMI).  
- **sample image**:
  ```
  [Base Image: Ubuntu + Nginx]
    ↓ 복제
  ├─ Instance #1
  ├─ Instance #2
  └─ Instance #3
  
---


# ☁️ 2️⃣ 클라우드 서비스 모델 및 개념 (Cloud Service Models & Core Concepts)

### 11 Infrastructure as a Service (IaaS)
- **meaning**: 서버, 네트워크, 스토리지 같은 인프라를 클라우드로 제공하는 서비스.  
- **simple explanation**: 컴퓨터 하드웨어를 인터넷으로 빌려 쓰는 것.  
- **example**: AWS EC2, Google Compute Engine, Naver Cloud Server.  
- **sample image**:
  ```
  사용자 → [IaaS 제공업체] → 서버, 네트워크, 스토리지 대여
  ```

---

### 12 Platform as a Service (PaaS)
- **meaning**: 애플리케이션을 개발할 수 있는 환경(운영체제, 런타임, DB 등)을 제공하는 서비스.  
- **simple explanation**: 서버 설정은 신경 안 쓰고, 코드만 올려서 실행하는 환경.  
- **example**: AWS Elastic Beanstalk, Google App Engine, Heroku.  
- **sample image**:
  ```
  개발자 → [PaaS 플랫폼] → 코드 업로드 → 자동 실행
  ```

---

### 13 Software as a Service (SaaS)
- **meaning**: 완성된 소프트웨어를 인터넷을 통해 바로 사용하는 서비스.  
- **simple explanation**: 설치 없이 웹으로 사용하는 프로그램.  
- **example**: Gmail, Slack, Google Docs.  
- **sample image**:
  ```
  사용자 → 인터넷 접속 → [SaaS 애플리케이션 사용]
  ```

---

### 14 Public Cloud (퍼블릭 클라우드)
- **meaning**: 여러 사용자가 함께 사용하는 클라우드 환경.  
- **simple explanation**: 공용 아파트처럼, 같은 건물(서버)을 여러 회사가 나눠 쓰는 구조.  
- **example**: AWS, Azure, Google Cloud Platform.  
- **sample image**:
  ```
  [서버 빌딩]
    ├─ Company A
    ├─ Company B
    └─ Company C
  ```

---

### 15 Private Cloud (프라이빗 클라우드)
- **meaning**: 한 조직만을 위해 구축된 전용 클라우드 환경.  
- **simple explanation**: 사무실 건물 전체를 한 회사가 독점 사용하는 느낌.  
- **example**: VMware Private Cloud, OpenStack.  
- **sample image**:
  ```
  [Private Cloud] → Company A 전용 사용
  ```

---

### 16 Hybrid Cloud (하이브리드 클라우드)
- **meaning**: Public Cloud와 Private Cloud를 함께 사용하는 구조.  
- **simple explanation**: 일부는 클라우드, 일부는 사내 서버로 관리.  
- **example**: AWS Outposts, Azure Arc.  
- **sample image**:
  ```
  [Private Cloud] ↔ [Public Cloud]
  (데이터와 서비스 연결)
  ```

---

### 17 Region (리전)
- **meaning**: 클라우드 서비스가 실제로 위치한 지리적 데이터센터 구역.  
- **simple explanation**: 서울, 도쿄, 런던 같은 서버 위치 지역.  
- **example**: AWS ap-northeast-2 (서울 리전).  
- **sample image**:
  ```
  🌏 세계 지도
  ├─ 서울 Region
  ├─ 도쿄 Region
  └─ 프랑크푸르트 Region
  ```

---

### 18 Cloud Service Provider (CSP)
- **meaning**: 클라우드 서비스를 제공하는 회사.  
- **simple explanation**: 클라우드 “주인” 회사들.  
- **example**: AWS, Azure, Google Cloud, Naver Cloud.  
- **sample image**:
  ```
  ☁️ AWS | ☁️ GCP | ☁️ Azure | ☁️ NCP
  ```

---

### 19 Marketplace (마켓플레이스)
- **meaning**: 클라우드 내에서 소프트웨어나 솔루션을 구매하거나 배포할 수 있는 공간.  
- **simple explanation**: 앱스토어처럼, 필요한 서버 앱을 클릭 한 번으로 설치하는 곳.  
- **example**: AWS Marketplace, Azure Marketplace.  
- **sample image**:
  ```
  [Marketplace]
   ├─ WordPress 설치
   ├─ MySQL 설치
   └─ Jenkins 설치
  ```

---

### 20 Availability Zone (AZ)
- **meaning**: 한 리전 안에서도 나뉜 독립된 데이터센터 구역.  
- **simple explanation**: 한 지역(Region) 안의 여러 건물(센터).  
- **example**: ap-northeast-2a, ap-northeast-2b.  
- **sample image**:
  ```
  [서울 Region]
    ├─ AZ a
    ├─ AZ b
    └─ AZ c

# 🌐 3️⃣ 네트워크 및 보안 (Networking & Security)

---

### 21 VPC (Virtual Private Cloud)
- **meaning**: 사용자가 정의한 가상의 독립 네트워크 환경.  
- **simple explanation**: 클라우드 안에 나만의 네트워크 공간을 만드는 것.  
- **example**: AWS VPC, Naver Cloud VPC.  
- **sample image**:
  ```
  ☁️ Cloud
   └─ VPC (내 전용 네트워크)
       ├─ Subnet A
       └─ Subnet B
  ```

---

### 22 Subnet (서브넷)
- **meaning**: VPC를 더 작게 나누어 구성한 네트워크 구역.  
- **simple explanation**: 한 아파트 단지를 여러 동으로 나누는 개념.  
- **example**: Public Subnet, Private Subnet.  
- **sample image**:
  ```
  [VPC]
   ├─ Public Subnet (인터넷 접근 가능)
   └─ Private Subnet (내부 전용)
  ```

---

### 23 Route Table (라우팅 테이블)
- **meaning**: 네트워크 트래픽이 어디로 가야 할지를 정의하는 표.  
- **simple explanation**: 길 안내 지도 같은 역할.  
- **example**: VPC Route Table 설정에서 인터넷 게이트웨이로 트래픽 전송.  
- **sample image**:
  ```
  목적지: 0.0.0.0/0 → Internet Gateway
  목적지: 10.0.1.0/24 → Local Subnet
  ```

---

### 24 NAT Gateway
- **meaning**: Private Subnet의 인스턴스가 외부로 나갈 수 있도록 중계하는 장치.  
- **simple explanation**: 내부 전용 서버가 인터넷으로 나갈 때 대신 나가주는 출입문.  
- **example**: AWS NAT Gateway.  
- **sample image**:
  ```
  [Private Subnet] → NAT Gateway → Internet
  ```

---

### 25 Internet Gateway
- **meaning**: VPC와 외부 인터넷을 연결해주는 장치.  
- **simple explanation**: 외부 세상으로 나가는 문.  
- **example**: AWS Internet Gateway.  
- **sample image**:
  ```
  [VPC 내부] ↔ [Internet Gateway] ↔ 🌍 Internet
  ```

---

### 26 Security Group
- **meaning**: 인스턴스 단위로 적용되는 방화벽 규칙.  
- **simple explanation**: 서버의 문을 열고 닫는 역할.  
- **example**: 22번(SSH)만 허용, 80번(HTTP)만 열기.  
- **sample image**:
  ```
  [EC2 Instance]
   ├─ Inbound: 22, 80 허용
   └─ Outbound: 모든 트래픽 허용
  ```

---

### 27 NACL (Network ACL)
- **meaning**: Subnet 단위의 네트워크 접근 제어 목록.  
- **simple explanation**: 아파트 단지 정문 보안관 같은 역할.  
- **example**: 특정 IP 차단 또는 허용 설정.  
- **sample image**:
  ```
  [Subnet]
   ├─ Allow: 80, 443
   └─ Deny: 22
  ```

---

### 28 DNS (Domain Name System)
- **meaning**: 도메인 이름을 IP 주소로 바꿔주는 시스템.  
- **simple explanation**: www.google.com → 142.250.190.14 로 변환.  
- **example**: Route 53, Cloud DNS.  
- **sample image**:
  ```
  User → www.site.com → DNS → 192.168.1.10
  ```

---

### 29 Load Balancer (로드 밸런서)
- **meaning**: 여러 서버로 트래픽을 분산시켜주는 장치.  
- **simple explanation**: 손님을 여러 카운터로 나눠주는 점원.  
- **example**: AWS ALB, Nginx Load Balancer.  
- **sample image**:
  ```
  [사용자 요청]
     ↓
  [Load Balancer]
   ├─ Server A
   └─ Server B
  ```

---

### 30 Firewall (방화벽)
- **meaning**: 네트워크 접근을 차단하거나 허용하는 보안 장치.  
- **simple explanation**: 외부의 공격으로부터 서버를 지키는 보호벽.  
- **example**: AWS Network Firewall, Cisco Firewall.  
- **sample image**:
  ```
  🌍 Internet → [Firewall] → 🖥️ Internal Network
  
---

# 🔐 4️⃣ 보안 확장 및 스토리지 시작 (Security Extension & Storage Intro)

### 31 VPN (Virtual Private Network)
- **meaning**: 외부에서 안전하게 내부 네트워크에 접속할 수 있게 해주는 암호화된 통신 기술.  
- **simple explanation**: 집에서도 회사 내부 서버에 보안 터널을 통해 접속하는 것.  
- **example**: OpenVPN, Cisco AnyConnect, AWS Client VPN.  
- **sample image**:
  ```
  🏠 Home → 🔒 VPN Tunnel → 🏢 Company Network
  ```

---

### 32 Identity and Access Management (IAM)
- **meaning**: 클라우드 리소스에 대한 사용자 및 권한을 관리하는 서비스.  
- **simple explanation**: 누가 무엇을 할 수 있는지를 통제하는 관리자 시스템.  
- **example**: AWS IAM, Naver Cloud IAM.  
- **sample image**:
  ```
  👤 User → [IAM Policy] → 접근 허용/거부 결정
  ```

---

### 33 MFA (Multi-Factor Authentication)
- **meaning**: 비밀번호 외에 추가 인증 수단을 요구하는 보안 절차.  
- **simple explanation**: 로그인 시 비밀번호 + 휴대폰 인증 코드 같이 2단계 확인.  
- **example**: Google Authenticator, AWS MFA.  
- **sample image**:
  ```
  로그인 → 🔑 비밀번호 + 📱 OTP 코드
  ```

---

### 34 Role (역할)
- **meaning**: 특정 권한의 집합으로, 사용자가 어떤 작업을 수행할 수 있는지를 정의.  
- **simple explanation**: 관리자, 개발자, 읽기 전용 같은 역할 구분.  
- **example**: AWS IAM Role (EC2에 S3 접근 허용).  
- **sample image**:
  ```
  Role: EC2ReadAccess → EC2가 S3에 접근 가능
  ```

---

### 35 Policy (정책)
- **meaning**: 리소스에 대한 접근 허용/거부 규칙을 JSON 형태로 정의.  
- **simple explanation**: “누가 어떤 리소스에 무엇을 할 수 있는가”를 적어놓은 문서.  
- **example**: S3 ReadOnly Policy.  
- **sample image**:
  ```
  {
    "Effect": "Allow",
    "Action": "s3:GetObject",
    "Resource": "arn:aws:s3:::bucket/*"
  }
  ```

---

### 36 Permission (권한)
- **meaning**: 특정 사용자 또는 역할이 리소스에 수행할 수 있는 작업의 범위.  
- **simple explanation**: “읽기만 가능” 또는 “삭제 가능” 같은 세부 권한.  
- **example**: EC2:StartInstances, S3:DeleteObject.  
- **sample image**:
  ```
  User → Permission → Resource (Read / Write / Delete)
  ```

---

### 37 Key Pair (키 페어)
- **meaning**: 비대칭 암호화를 사용해 서버에 안전하게 접속하기 위한 공개키와 비밀키 쌍.  
- **simple explanation**: 내 컴퓨터의 열쇠(Private Key)와 서버의 자물쇠(Public Key).  
- **example**: AWS EC2 SSH Key (.pem 파일).  
- **sample image**:
  ```
  🔑 Private Key (내 PC)
  🔒 Public Key (서버)
  연결 시 인증
  ```

---

### 38 Secrets Manager
- **meaning**: 비밀번호, API 키 같은 민감한 정보를 안전하게 저장하고 관리하는 서비스.  
- **simple explanation**: 중요한 비밀번호를 코드에 직접 적지 않고 안전한 금고에 보관하는 것.  
- **example**: AWS Secrets Manager, HashiCorp Vault.  
- **sample image**:
  ```
  [App] → [Secrets Manager] → API Key 반환
  ```

---

### 39 KMS (Key Management Service)
- **meaning**: 데이터를 암호화/복호화할 때 사용하는 키를 안전하게 생성하고 관리하는 서비스.  
- **simple explanation**: 암호화에 쓰이는 열쇠를 안전하게 보관하고 사용하는 시스템.  
- **example**: AWS KMS, Google Cloud KMS.  
- **sample image**:
  ```
  🔐 Data → [KMS Key Encrypt] → 🔒 Ciphertext
  ```

---

### 40 Encryption (암호화)
- **meaning**: 데이터를 읽을 수 없도록 암호문으로 바꾸는 기술.  
- **simple explanation**: 데이터를 잠가서 권한 있는 사람만 열어볼 수 있게 하는 것.  
- **example**: AES-256, RSA 암호화.  
- **sample image**:
  ```
  Plain Text → 🔐 Encryption → Cipher Text
  
---

# 💾 5️⃣ 스토리지 및 데이터 관리 (Storage & Data Management)

---

### 41 Block Storage
- **meaning**: 데이터를 일정한 크기의 블록 단위로 저장하는 방식의 스토리지.  
- **simple explanation**: 하드디스크처럼 데이터를 조각(블록)으로 저장하는 구조.  
- **example**: AWS EBS, Naver Cloud Block Storage.  
- **sample image**:
  ```
  [Block 1][Block 2][Block 3] → 조합 = 전체 파일
  ```

---

### 42 Object Storage
- **meaning**: 데이터를 객체 단위(파일 + 메타데이터)로 저장하는 스토리지.  
- **simple explanation**: 파일을 한 덩어리(객체)로 저장하고, URL로 접근하는 구조.  
- **example**: AWS S3, Naver Cloud Object Storage.  
- **sample image**:
  ```
  Object = { Data + Metadata + Unique ID }
  URL로 접근 → https://bucket/object
  ```

---

### 43 File Storage
- **meaning**: 여러 서버가 동시에 접근할 수 있는 네트워크 기반 파일 시스템.  
- **simple explanation**: 여러 컴퓨터가 함께 쓰는 공유 폴더.  
- **example**: AWS EFS, NFS(Network File System).  
- **sample image**:
  ```
  Server A ↔ [File Storage] ↔ Server B
  ```

---

### 44 Backup
- **meaning**: 데이터를 손실에 대비해 복사해 두는 것.  
- **simple explanation**: 혹시 모를 사고를 대비해 복사본을 보관하는 것.  
- **example**: DB 백업, Snapshot 백업.  
- **sample image**:
  ```
  📂 Original Data → 📦 Backup Copy
  ```

---

### 45 Archive
- **meaning**: 자주 사용하지 않는 데이터를 장기 보관용으로 저장하는 방식.  
- **simple explanation**: 오래된 데이터를 값싼 창고에 저장하는 것.  
- **example**: AWS Glacier, NCP Archive Storage.  
- **sample image**:
  ```
  🔹 Hot Data → S3
  🔹 Cold Data → Glacier (Archive)
  ```

---

### 46 Lifecycle Policy
- **meaning**: 저장된 데이터를 일정 기간 후 자동으로 이동하거나 삭제하는 규칙.  
- **simple explanation**: 일정 시간이 지나면 자동 정리해주는 청소 규칙.  
- **example**: S3 Lifecycle Rule (30일 후 Glacier 이동).  
- **sample image**:
  ```
  Day 0 → Upload
  Day 30 → Move to Archive
  Day 365 → Delete
  ```

---

### 47 Read Replica
- **meaning**: 데이터베이스 읽기 부하를 분산하기 위한 복제본.  
- **simple explanation**: 원본 DB를 복제해 읽기 전용으로 사용하는 서버.  
- **example**: AWS RDS Read Replica.  
- **sample image**:
  ```
  [Primary DB] → [Read Replica #1]
                 → [Read Replica #2]
  ```

---

### 48 Database Cluster
- **meaning**: 여러 DB 서버를 하나의 시스템처럼 묶어 운영하는 구조.  
- **simple explanation**: 여러 DB가 하나처럼 작동하는 팀플레이 구조.  
- **example**: MySQL Cluster, PostgreSQL Cluster.  
- **sample image**:
  ```
  [DB Node 1] ↔ [DB Node 2] ↔ [DB Node 3]
  ```

---

### 49 Caching
- **meaning**: 자주 사용하는 데이터를 임시로 저장해 빠르게 불러오는 기술.  
- **simple explanation**: 자주 찾는 책을 책장 앞에 두는 것처럼, 빠른 접근용 복사본 저장.  
- **example**: Redis, Memcached, CloudFront Cache.  
- **sample image**:
  ```
  [User Request] → Cache → DB
  ```

---

### 50 Data Replication
- **meaning**: 데이터를 여러 위치에 복사해 고가용성을 확보하는 기술.  
- **simple explanation**: 데이터를 여러 지역에 복제해 장애 시에도 접근 가능하게 하는 것.  
- **example**: Multi-AZ RDS, GCP Cloud SQL Replication.  
- **sample image**:
  ```
  Region A ↔ Region B ↔ Region C
  (동기화된 복제 데이터)
  
---
