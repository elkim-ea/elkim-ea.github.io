---
layout: post
title: " Portfolio-ncp "
date: 2025-12-03
categories:
  - "Portfolio" 
---
# 🚀 Naver Cloud(NCP) 기반 DevOps CI/CD 구축기  
### _서비스 운영을 위한 인프라 설계부터 자동 배포까지_

Matcha 프로젝트는 React + Spring Boot 기반의 풀스택 서비스입니다.  
이 프로젝트를 실제 배포 가능한 형태로 만들기 위해,  
저는 **Naver Cloud Platform(NCP)** 위에 직접 DevOps 환경을 설계하고 구축했습니다.

이 글에서는 단순히 “어떻게 했다”가 아니라,  
**왜 이렇게 설계했는지**, 그리고 **구현하면서 어떤 점을 고려했는지**를 중심으로 설명합니다.

---

# 🔍 1. 전체 아키텍처 설계 의도

초기 목표는 단순했습니다.

> **"코드를 푸시하면, 자동으로 빌드하고, 자동으로 서버에 배포되는 환경을 만들자."**

하지만 실제 운영 환경을 고려하니 더 많은 요소가 필요했습니다:

- 외부 노출 최소화  
- 배포 서버는 Private Subnet에서만 운영  
- Jenkins는 GitHub Webhook 수신을 위해 Public Subnet 필요  
- Backend만 LoadBalancer로 외부 공개  
- Frontend는 Internal Only(Deploy Server 포트 80)  

이 기준을 바탕으로 다음과 같은 아키텍처를 설계했습니다.

---

## ✔ CI/CD 전체 동작 흐름

| 번호 | 동작 |
|------|-------------------------------------------------------------|
| 1 | GitHub에 코드 Push |
| 2 | Webhook으로 Jenkins 자동 트리거 |
| 3 | Jenkins가 소스 Pull |
| 4 | FE/BE Build |
| 5 | Docker Image Build |
| 6 | Image Export (.tar) |
| 7 | Deploy Server로 전송 |
| 8 | docker load 후 컨테이너 실행 |
| 9 | Backend가 LoadBalancer Target Group에 연결 |
| 10 | 사용자 → LB → Backend API 호출 |

---

# 🏗 전체 인프라 구조  

<img src="./docs/architecture.png" width="800">

---

# 🧱 2. 네트워크 설계 (VPC / Subnet / Routing / NAT)

## ✔ 2-1) VPC 구성

| 항목 | 값 |
|------|----------------|
| VPC CIDR | 10.0.0.0/16 |
| 목적 | Jenkins · Deploy · NAT · LB 네트워크 분리 |

---

## ✔ 2-2) Subnet 구성

| Subnet | CIDR | Zone | 역할 |
|--------|-----------|------|---------------------------|
| cicd-subnet | 10.0.1.0/24 | KR-1 | Jenkins Server |
| private-subnet | 10.0.2.0/24 | KR-1 | Deploy Server |
| nat-subnet | 10.0.3.0/24 | KR-1 | NAT Gateway |
| public-subnet-1 | 10.0.4.0/24 | KR-2 | LoadBalancer Zone A |
| public-subnet-2 | 10.0.5.0/24 | KR-1 | LoadBalancer Zone B |

<img src="./docs/subnet-list.png" width="700">

---

## ✔ 2-3) Routing Table 구성

| 목적지 | Target | 설명 |
|--------|-------------|---------------------------|
| 0.0.0.0/0 | NAT Gateway | Private 서버의 외부 통신 |
| 10.0.0.0/16 | LOCAL | 내부 통신 |

<img src="./docs/nat-gateway.png" width="700">

---

# 🔐 3. 보안 그룹(ACG) 설계

## ✔ Jenkins ACG

| 포트 | 출처 | 이유 |
|------|---------|----------------|
| 22 | 0.0.0.0/0 | SSH 접근 |
| 8080 | 0.0.0.0/0 | Jenkins Web Console |

---

## ✔ Deploy Server ACG

| 포트 | 출처 | 설명 |
|------|----------------|------------------------------|
| 22 | Jenkins Server | 자동 배포 |
| 80 | LB Subnet | Frontend 내부 서비스 |
| 8080 | LB Subnet | Backend API |
| 3306 | Private Only | DB 내부 통신 |

<img src="./docs/jenkins-acg.png" width="700">  
<img src="./docs/deploy-acg.png" width="700">

---

# 🏛 4. 서버 구성

| 서버명 | Private IP | Public IP | 역할 |
|--------|-------------|-----------|---------------------------|
| Jenkins Server | 10.0.1.6 | 211.188.54.xxx | Build · Dockerize |
| Deploy Server | 10.0.2.6 | ❌ 없음 | docker-compose 운영 서버 |

---

# 🧰 5. Jenkins 기반 CI/CD Pipeline

## ✔ 전체 빌드 · 배포 흐름

1. GitHub → Jenkins Checkout  
2. Backend Gradle Build  
3. Frontend Build  
4. Docker Build  
5. Docker Save (.tar)  
6. Deploy Server로 SCP 전송  
7. docker load → docker-compose up  

---

## ✔ Jenkinsfile (설계 의도 포함)

```groovy
pipeline {
  agent any

  stages {

    // 1. GitHub 코드 가져오기
    stage('Checkout') {
      steps { checkout scm }
    }

    // 2. Backend 빌드
    stage('Build Backend') {
      steps { sh './gradlew clean build -x test' }
    }

    // 3. Frontend 빌드
    stage('Build Frontend') {
      steps { sh 'cd frontend && npm install && npm run build' }
    }

    // 4. Docker 이미지 생성
    stage('Docker Build') {
      steps { sh 'docker build -t matcha-backend ./backend' }
    }

    // 5. Deploy Server로 전송 & 실행
    stage('Deploy') {
      steps {
        sh 'scp backend.tar root@10.0.2.6:/opt/matcha'
        sh 'ssh root@10.0.2.6 "docker load < backend.tar && docker-compose up -d"'
      }
    }
  }
}
<img src="./docs/jenkins-dashboard.png" width="700"> <img src="./docs/jenkins-trend.png" width="700">

6. Deploy Server (docker-compose 운영 구조)
version: "3.8"

services:
  backend:
    image: matcha-backend:latest
    ports:
      - "8080:8080"

  frontend:
    image: matcha-frontend:latest
    ports:
      - "80:80"

  db:
    image: mariadb:10.6
    environment:
      MYSQL_ROOT_PASSWORD: 1234

<img src="./docs/docker-compose-run.png" width="700">

🌐 7. LoadBalancer 설정
✔ Backend만 외부 노출한 이유

Frontend는 정적 웹이기 때문에 내부 제공(Internal Only)으로 충분했고,
API 통신만 외부에 필요했기 때문에 Backend(8080) 만 Target Group에 연결했습니다.

항목	값
LB Subnets	public-subnet-1, public-subnet-2
Target Group	backend:8080
Health Check	/actuator/health
<img src="./docs/lb1.png" width="700"> <img src="./docs/lb2.png" width="700"> <img src="./docs/lb3.png" width="700"> <img src="./docs/lb4.png" width="700">
🎉 8. 서비스 동작 화면
<img src="./docs/web1.png" width="700"> <img src="./docs/web2.png" width="700"> <img src="./docs/web3.png" width="700">
📁 9. 프로젝트 구조
PORTFOLIO
 ├── Deploy
 │   ├── AWS
 │   ├── GCP
 │   └── NCP   ← 본 문서 설명
 ├── Matcha      ← ESG FullStack App
 ├── Jenkinsfile
 └── README.md

⭐ 10. 이 프로젝트에서 강조하고 싶은 핵심 포인트

✔ 실무 수준의 DevOps 인프라를 직접 설계
✔ Jenkins Public + Deploy Private 구조로 보안 강화
✔ NAT Gateway 기반 Private Subnet 외부 통신 구성
✔ Backend만 공개하는 최소 권한 인프라 설계
✔ Docker 기반 CI/CD 자동화 파이프라인 구축
✔ GitHub → Jenkins → Deploy → LB 전체 자동화 성공

🎯 마무리

이 프로젝트를 통해 단순 배포를 넘어서,
실제 운영 환경에 가까운 DevOps 인프라를 스스로 설계하고 구축한 경험을 얻었습니다.

특히 네트워크 설계, Private Subnet 운용, NAT 구성, Jenkins 파이프라인, LB 설계 등
기업 환경에서도 요구되는 핵심 DevOps 역량을 직접 실습하며 강화할 수 있었습니다.

---
