---
layout: post
title: "Cloud 필수 용어 정리 - 2 (Kor.ver)"
date: 2025-11-19
categories:
  - "Cloud" 
---
# 🐳 6️⃣ 컨테이너 및 오케스트레이션 (Containerization & Orchestration)

### 51 Container (컨테이너)
- **meaning**: 애플리케이션과 실행 환경을 함께 묶은 독립 실행 단위.  
- **simple explanation**: 어디서든 똑같이 실행되도록 만든 작고 가벼운 패키지.  
- **example**: Nginx Container, Python App Container.  
- **sample image**:
  ```
  [App Code + Library + OS] → Container로 포장 → 실행
  ```

---

### 52 Docker (도커)
- **meaning**: 컨테이너를 만들고 실행할 수 있게 해주는 플랫폼.  
- **simple explanation**: 컨테이너를 쉽게 만들고 배포할 수 있는 도구.  
- **example**: Docker Engine, Docker Desktop.  
- **sample image**:
  ```
  🐳 Docker → Build → Ship → Run
  ```

---

### 53 Kubernetes (쿠버네티스)
- **meaning**: 여러 컨테이너를 자동으로 배포·관리·확장하는 오케스트레이션 도구.  
- **simple explanation**: 수백 개의 컨테이너를 자동으로 관리해주는 시스템.  
- **example**: GKE, EKS, NKS.  
- **sample image**:
  ```
  [Cluster]
   ├─ Node 1 (Pods)
   ├─ Node 2 (Pods)
   └─ Node 3 (Pods)
  ```

---

### 54 Pod (파드)
- **meaning**: 하나 이상의 컨테이너가 함께 실행되는 가장 작은 쿠버네티스 단위.  
- **simple explanation**: 같은 공간에서 함께 일하는 컨테이너들의 그룹.  
- **example**: Nginx + Sidecar Container.  
- **sample image**:
  ```
  [Pod]
   ├─ Container #1 (App)
   └─ Container #2 (Logger)
  ```

---

### 55 Node (노드)
- **meaning**: 쿠버네티스 클러스터를 구성하는 실제 서버(또는 가상 머신).  
- **simple explanation**: 컨테이너가 실제로 실행되는 컴퓨터 한 대.  
- **example**: Worker Node, Master Node.  
- **sample image**:
  ```
  [Node]
   ├─ Pod 1
   ├─ Pod 2
   └─ Pod 3
  ```

---

### 56 Cluster (클러스터)
- **meaning**: 여러 Node를 하나로 묶어 관리하는 쿠버네티스의 전체 시스템.  
- **simple explanation**: 여러 서버가 함께 일하는 하나의 큰 팀.  
- **example**: Kubernetes Cluster, Docker Swarm Cluster.  
- **sample image**:
  ```
  Cluster = Node1 + Node2 + Node3
  (컨테이너 자동 배포 및 관리)
  ```

---

### 57 Deployment (디플로이먼트)
- **meaning**: 애플리케이션을 자동으로 배포하고 버전을 관리하는 쿠버네티스 리소스.  
- **simple explanation**: 컨테이너를 배포하고 업데이트를 자동화하는 설정 파일.  
- **example**: Nginx Deployment, API Deployment.  
- **sample image**:
  ```
  Deployment → Pod 생성 → Replica 관리
  ```

---

### 58 StatefulSet (스테이트풀셋)
- **meaning**: 상태를 가지는 애플리케이션(DB 등)을 위한 쿠버네티스 배포 리소스.  
- **simple explanation**: 데이터가 유지되어야 하는 앱을 안전하게 관리하는 방법.  
- **example**: MySQL StatefulSet, Kafka StatefulSet.  
- **sample image**:
  ```
  StatefulSet
   ├─ Pod 0 (DB1)
   ├─ Pod 1 (DB2)
   └─ Pod 2 (DB3)
  ```

---

### 59 DaemonSet (데몬셋)
- **meaning**: 모든 노드에 동일한 Pod를 하나씩 배포하는 쿠버네티스 리소스.  
- **simple explanation**: 모든 서버에 꼭 필요한 공통 컨테이너를 배포할 때 사용.  
- **example**: 로그 수집 에이전트, 모니터링 에이전트.  
- **sample image**:
  ```
  Node1 → Log Agent
  Node2 → Log Agent
  Node3 → Log Agent
  ```

---

### 60 Service (서비스)
- **meaning**: 쿠버네티스에서 Pod에 안정적인 네트워크 주소(IP)를 제공하는 리소스.  
- **simple explanation**: Pod들이 죽거나 교체돼도 항상 같은 주소로 접근할 수 있게 해주는 창구.  
- **example**: ClusterIP, NodePort, LoadBalancer Service.  
- **sample image**:
  ```
  [User]
    ↓
  [Service] → Pod1 / Pod2 / Pod3
  
---

# ⚙️ 7️⃣ 배포 자동화 및 CI/CD 파이프라인 (Automation & CI/CD Pipeline)

### 61 Helm (헬름)
- **meaning**: 쿠버네티스에서 애플리케이션 배포를 간소화하는 패키지 관리자.  
- **simple explanation**: 쿠버네티스의 앱 설치를 클릭 한 번처럼 쉽게 만들어주는 도구.  
- **example**: Helm Chart로 Nginx 설치, MySQL 배포.  
- **sample image**:
  ```
  helm install my-nginx nginx-chart/
  ```

---

### 62 Auto Scaling (오토 스케일링)
- **meaning**: 트래픽 증가나 감소에 따라 서버 인스턴스를 자동으로 늘리거나 줄이는 기능.  
- **simple explanation**: 사용자가 많으면 서버를 늘리고, 적으면 줄이는 자동 조절 장치.  
- **example**: AWS Auto Scaling Group.  
- **sample image**:
  ```
  낮: 2대 → 트래픽 증가 → 밤: 5대로 자동 확장
  ```

---

### 63 Health Check (헬스 체크)
- **meaning**: 서버나 애플리케이션이 정상 동작 중인지 주기적으로 확인하는 기능.  
- **simple explanation**: 살아있는지 주기적으로 확인하는 ‘심박 측정’.  
- **example**: ALB Health Check, Kubernetes Liveness Probe.  
- **sample image**:
  ```
  Server A ✅  Server B ❌ → 자동 교체
  ```

---

### 64 CI/CD (Continuous Integration / Continuous Deployment)
- **meaning**: 코드 변경을 자동으로 빌드·테스트·배포하는 프로세스.  
- **simple explanation**: 개발자가 코드를 올리면 자동으로 배포까지 되는 시스템.  
- **example**: GitHub Actions, Jenkins Pipeline.  
- **sample image**:
  ```
  Code Push → Build → Test → Deploy
  ```

---

### 65 Pipeline (파이프라인)
- **meaning**: 소스 코드가 배포되기까지 자동으로 거치는 단계의 흐름.  
- **simple explanation**: ‘코드 → 테스트 → 배포’의 자동 연결 통로.  
- **example**: Jenkins Pipeline, GitLab CI Pipeline.  
- **sample image**:
  ```
  Step 1: Build → Step 2: Test → Step 3: Deploy
  ```

---

### 66 Jenkins (젠킨스)
- **meaning**: 오픈소스 기반의 CI/CD 자동화 서버.  
- **simple explanation**: 코드를 빌드하고 배포하는 자동화 로봇.  
- **example**: Jenkinsfile로 빌드 스크립트 정의.  
- **sample image**:
  ```
  Git Commit → Jenkins → Docker Build → Deploy
  ```

---

### 67 GitHub Actions
- **meaning**: GitHub 내에서 직접 워크플로우를 자동화할 수 있는 CI/CD 서비스.  
- **simple explanation**: 코드 푸시만으로 자동 빌드/배포가 되는 GitHub 내장 기능.  
- **example**: .github/workflows/deploy.yml.  
- **sample image**:
  ```
  on: push → jobs: build → deploy
  ```

---

### 68 GitLab CI
- **meaning**: GitLab에서 제공하는 내장형 CI/CD 시스템.  
- **simple explanation**: GitLab 안에서 파이프라인을 자동으로 실행해주는 기능.  
- **example**: .gitlab-ci.yml 설정.  
- **sample image**:
  ```
  stages: [build, test, deploy]
  ```

---

### 69 Ansible (앤서블)
- **meaning**: 서버 설정, 배포, 구성 관리를 자동화하는 도구.  
- **simple explanation**: 여러 서버를 한 번에 자동 설정하는 ‘원격 리모컨’.  
- **example**: ansible-playbook install.yml.  
- **sample image**:
  ```
  Control Node → SSH → Managed Servers
  ```

---

### 70 Chef (셰프)
- **meaning**: 인프라 구성을 코드로 관리하는 구성 관리 도구.  
- **simple explanation**: 서버 환경 설정을 요리 레시피처럼 코드로 관리.  
- **example**: Chef Cookbook, Recipe.  
- **sample image**:
  ```
  Recipe → Install Nginx → Configure → Restart Service
  ```

---

# ⚙️ 8️⃣ 자동화 확장 및 배포 전략 (Advanced Automation & Deployment Strategies)

---

### 71 Puppet (퍼펫)
- **meaning**: 인프라 환경을 코드로 관리하고 서버 설정을 자동화하는 도구.  
- **simple explanation**: 여러 서버의 설정을 동시에 자동으로 바꾸는 시스템.  
- **example**: Puppet Master 서버에서 수백 대의 서버를 일괄 설정.  
- **sample image**:
  ```
  Puppet Master → Agent Servers (자동 설정 배포)
  ```

---

### 72 Bash Script (배시 스크립트)
- **meaning**: 리눅스에서 명령어를 자동으로 실행하도록 작성한 스크립트 파일.  
- **simple explanation**: 반복 작업을 자동으로 처리하는 리눅스용 자동화 스크립트.  
- **example**: build.sh, deploy.sh.  
- **sample image**:
  ```
  #!/bin/bash
  echo "Server Starting..."
  ```

---

### 73 Shell Script (셸 스크립트)
- **meaning**: 운영체제의 명령줄에서 실행할 수 있는 자동화 스크립트 언어.  
- **simple explanation**: 여러 명령어를 한 번에 실행하는 “자동 명령서”.  
- **example**: Linux Shell, Zsh Script.  
- **sample image**:
  ```
  #!/bin/sh
  echo "Deploying App..."
  ```

---

### 74 Infrastructure as Code (IaC)
- **meaning**: 서버와 네트워크 설정을 코드로 정의하고 관리하는 개념.  
- **simple explanation**: 인프라 환경을 코드로 만들어서 자동 배포하는 방식.  
- **example**: Terraform, CloudFormation, Ansible.  
- **sample image**:
  ```
  main.tf → terraform apply → 자동 인프라 구축
  ```

---

### 75 Load Testing (부하 테스트)
- **meaning**: 시스템이 많은 사용자를 동시에 처리할 수 있는지 테스트하는 방법.  
- **simple explanation**: 얼마나 많은 요청을 견딜 수 있는지 미리 실험.  
- **example**: Apache JMeter, k6, Locust.  
- **sample image**:
  ```
  1000명 동시 접속 → 서버 응답 시간 측정
  ```

---

### 76 Blue-Green Deployment (블루-그린 배포)
- **meaning**: 두 개의 동일한 환경(Blue/Green)을 두고 하나는 서비스, 하나는 배포용으로 사용하는 무중단 배포 방식.  
- **simple explanation**: 새 버전을 미리 올려두고, 완성되면 바로 교체하는 배포 전략.  
- **example**: AWS Elastic Beanstalk Blue-Green Deployment.  
- **sample image**:
  ```
  [Blue: 현재 서비스] ←→ [Green: 새 버전 준비]
  스위치 시 트래픽 전환
  ```

---

### 77 Canary Deployment (카나리 배포)
- **meaning**: 새 버전을 일부 사용자에게만 먼저 배포해 테스트하는 방식.  
- **simple explanation**: 새 버전을 조금씩 시범 운영 후 안정 시 전체 배포.  
- **example**: Kubernetes Canary Release.  
- **sample image**:
  ```
  Users: 10% → New Version
          90% → Old Version
  ```

---

### 78 Rolling Update (롤링 업데이트)
- **meaning**: 기존 서버를 하나씩 새 버전으로 교체하며 서비스 중단 없이 배포하는 방식.  
- **simple explanation**: 하나씩 바꾸면서 천천히 전체 업데이트하는 배포.  
- **example**: Kubernetes Rolling Update, Docker Swarm Update.  
- **sample image**:
  ```
  Pod1 ✅ → 업데이트 → Pod2 → Pod3 순차 교체
  ```

---

### 79 Metrics (메트릭)
- **meaning**: 시스템 성능을 측정하기 위한 수치 데이터(CPU, 메모리 등).  
- **simple explanation**: 서버가 얼마나 일하는지 보여주는 숫자 지표.  
- **example**: Prometheus, CloudWatch Metrics.  
- **sample image**:
  ```
  CPU: 80% | Memory: 65% | Disk: 40%
  ```

---

### 80 Logs (로그)
- **meaning**: 시스템이나 애플리케이션의 동작 기록.  
- **simple explanation**: 서버가 무슨 일을 했는지 일기처럼 기록한 데이터.  
- **example**: Nginx Access Log, Application Error Log.  
- **sample image**:
  ```
  [2025-11-19 21:00] INFO - User login success
  
---

# 📈 9️⃣ 모니터링 · 로그 · 관찰성 (Monitoring, Logging & Observability)

---

### 81 Tracing (트레이싱)
- **meaning**: 분산 시스템에서 요청이 어떻게 흐르는지 추적하는 기술.  
- **simple explanation**: 사용자의 요청이 여러 서버를 거칠 때 전체 경로를 따라가는 지도.  
- **example**: Jaeger, Zipkin, AWS X-Ray.  
- **sample image**:
  ```
  User → Service A → Service B → DB
  (요청 경로 추적)
  ```

---

### 82 Prometheus (프로메테우스)
- **meaning**: 서버나 애플리케이션의 성능 데이터를 수집하고 저장하는 모니터링 도구.  
- **simple explanation**: 서버 상태를 숫자로 기록하고 분석하는 시스템.  
- **example**: Prometheus + Grafana 대시보드 구축.  
- **sample image**:
  ```
  [Server Metrics] → Prometheus DB → Grafana
  ```

---

### 83 Grafana (그라파나)
- **meaning**: Prometheus 등에서 수집한 데이터를 시각화하는 도구.  
- **simple explanation**: 서버 상태를 그래프로 보여주는 대시보드.  
- **example**: Grafana Dashboard, Alert 설정.  
- **sample image**:
  ```
  📊 CPU 사용률 그래프
  📈 네트워크 트래픽 차트
  ```

---

### 84 ELK Stack (Elasticsearch, Logstash, Kibana)
- **meaning**: 로그를 수집(Logstash), 저장(Elasticsearch), 시각화(Kibana)하는 통합 로그 관리 시스템.  
- **simple explanation**: 서버 로그를 모아 검색하고 분석할 수 있게 하는 도구 세트.  
- **example**: ELK Stack으로 웹 서버 로그 분석.  
- **sample image**:
  ```
  App Logs → Logstash → Elasticsearch → Kibana (Dashboard)
  ```

---

### 85 Alerting (알림)
- **meaning**: 시스템 이상이나 오류 발생 시 관리자에게 경고를 보내는 기능.  
- **simple explanation**: 문제가 생기면 즉시 알려주는 자동 경보 시스템.  
- **example**: Prometheus Alertmanager, Grafana Alert.  
- **sample image**:
  ```
  CPU 90% 초과 → Slack 알림 전송
  ```

---

### 86 Observability (관찰성)
- **meaning**: 시스템 내부 상태를 외부에서 관찰하고 이해할 수 있는 능력.  
- **simple explanation**: 시스템이 왜 느려졌는지를 알아낼 수 있게 하는 ‘가시성’.  
- **example**: Logs + Metrics + Tracing = Observability.  
- **sample image**:
  ```
  Logs + Metrics + Traces → System Insight
  ```

---

### 87 Monitoring Dashboard
- **meaning**: 실시간으로 서버나 애플리케이션 상태를 보여주는 시각화 화면.  
- **simple explanation**: 현재 시스템이 정상인지 한눈에 보는 계기판.  
- **example**: Grafana Dashboard, CloudWatch Dashboard.  
- **sample image**:
  ```
  🖥️ Dashboard → CPU 40%, Memory 60%, Disk 70%
  ```

---

### 88 Incident Management (사고 관리)
- **meaning**: 시스템 장애나 오류가 발생했을 때 문제를 탐지하고 해결하는 프로세스.  
- **simple explanation**: 장애 발생 시 즉시 대응하고 원인 파악하는 절차.  
- **example**: PagerDuty, Opsgenie.  
- **sample image**:
  ```
  Alert 발생 → 담당자 알림 → 원인 조사 → 해결 완료
  ```

---

### 89 Root Cause Analysis (RCA, 근본 원인 분석)
- **meaning**: 장애나 문제의 표면적인 원인이 아닌 근본적인 원인을 찾는 분석 과정.  
- **simple explanation**: 왜 문제가 생겼는지를 ‘진짜 이유’까지 파고드는 분석.  
- **example**: RCA Report after System Outage.  
- **sample image**:
  ```
  Issue: DB 오류 → 원인: 디스크 포화 → 해결: 스토리지 확장
  ```

---

### 90 Logging Agent (로깅 에이전트)
- **meaning**: 서버의 로그를 수집해서 중앙 시스템으로 전송하는 프로그램.  
- **simple explanation**: 서버 일지를 자동으로 모아주는 ‘배달부’.  
- **example**: Fluentd, Filebeat.  
- **sample image**:
  ```
  Server Logs → Fluentd → Elasticsearch
  
---

# 🧠 🔟 아키텍처 & 고가용성 (Architecture & High Availability)

---

### 91 Contents Delivery Network (CDN)
- **meaning**: 전 세계에 분산된 서버를 통해 사용자와 가까운 위치에서 콘텐츠를 제공하는 네트워크.  
- **simple explanation**: 서울 이용자에게는 서울 근처 서버에서 바로 파일을 주는 ‘가까운 창고’.  
- **example**: CloudFront, Akamai, Cloudflare CDN.  
- **sample image**:
  ```
  Origin Server → 🌍 글로벌 CDN 엣지 → 사용자 (지연시간 감소)
  ```

---

### 92 High Availability (HA)
- **meaning**: 장애가 발생해도 서비스가 지속되도록 설계하는 개념.  
- **simple explanation**: 한 대가 고장 나도 다른 대가 바로 이어받는 구조.  
- **example**: 이중화(Active-Active, Active-Standby), 다중 인스턴스 배치.  
- **sample image**:
  ```
  LB → Server A (Active)
        Server B (Active)
  ```

---

### 93 Failover (장애 조치)
- **meaning**: 장애가 발생했을 때 자동으로 대기 중인 자원으로 전환되는 과정.  
- **simple explanation**: 메인 서버가 죽으면 예비 서버가 자동으로 ‘바로 교체’.  
- **example**: DB Primary 장애 시 Standby로 자동 전환.  
- **sample image**:
  ```
  Primary ❌ → (자동 전환) → Standby ✅
  ```

---

### 94 Disaster Recovery (DR)
- **meaning**: 대규모 재해 상황에서 서비스를 복구하기 위한 계획과 체계.  
- **simple explanation**: 지진/정전 같은 큰 사고가 나도 다른 지역에서 빨리 복구.  
- **example**: 다른 리전에 백업/스냅샷 유지, DR 사이트 운영.  
- **sample image**:
  ```
  Region A 장애 → Region B DR 사이트로 복구
  ```

---

### 95 Multi-AZ
- **meaning**: 한 리전 안의 여러 가용 영역(AZ)에 자원을 분산 배치하는 구성.  
- **simple explanation**: 같은 도시의 다른 건물에 서버를 나눠두기.  
- **example**: RDS Multi-AZ 배포.  
- **sample image**:
  ```
  [Region]
   ├─ AZ-a: App/DB
   └─ AZ-b: App/DB (대기/복제)
  ```

---

### 96 Scalability (확장성)
- **meaning**: 시스템이 트래픽 증가에 따라 성능/용량을 확장할 수 있는 능력.  
- **simple explanation**: 손님이 많아지면 서버 대수를 늘려도 잘 버티는 성질.  
- **example**: 수평 확장(Horizontal), 수직 확장(Vertical).  
- **sample image**:
  ```
  Horizontal: 서버 수 ↑
  Vertical: 서버 사양 ↑
  ```

---

### 97 Elasticity (탄력성)
- **meaning**: 부하 변화에 맞춰 자원을 자동으로 늘렸다 줄이는 능력.  
- **simple explanation**: 점심 피크만 잠깐 서버 늘리고, 끝나면 다시 줄이기.  
- **example**: Auto Scaling 정책 기반 증감.  
- **sample image**:
  ```
  트래픽 ↑ → 서버 자동 증가
  트래픽 ↓ → 서버 자동 감소
  ```

---

### 98 Caching (캐싱)
- **meaning**: 자주 요청되는 데이터를 빠르게 응답하기 위해 임시 저장하는 기술.  
- **simple explanation**: 자주 보는 자료를 책상 위에 올려두는 것.  
- **example**: Redis, Memcached, CDN 캐시.  
- **sample image**:
  ```
  User → Cache Hit → 빠른 응답
        Cache Miss → DB 조회
  ```

---

### 99 API Gateway
- **meaning**: 여러 마이크로서비스의 엔드포인트를 하나로 묶어 인증/라우팅/모니터링을 제공하는 진입점.  
- **simple explanation**: ‘입구는 하나, 안에서는 각 서비스로 길 안내’.  
- **example**: AWS API Gateway, Kong, NGINX Gateway.  
- **sample image**:
  ```
  Client → API Gateway → Auth/RateLimit → Service A/B/C
  ```

---

### 100 Service Mesh
- **meaning**: 마이크로서비스 간 통신을 보안·관찰·제어하는 인프라 레이어.  
- **simple explanation**: 서비스들 사이의 대화를 대신 관리해주는 ‘통신 관리자’.  
- **example**: Istio, Linkerd.  
- **sample image**:
  ```
  Service A ↔ (Sidecar Proxy) ↔ Service B
  TLS, Retry, Circuit Breaker, Telemetry
  
---

# 🌍 1️⃣1️⃣ 서버리스 · 엣지 컴퓨팅 · 메시지큐 · 버전 관리 (Serverless, Edge Computing, MQ & Version Control)

---

### 101 Serverless (서버리스)
- **meaning**: 서버를 직접 관리하지 않고, 클라우드가 자동으로 실행 환경을 제공하는 컴퓨팅 방식.  
- **simple explanation**: 서버 걱정 없이 코드를 올리면 자동으로 실행되는 구조.  
- **example**: AWS Lambda, Google Cloud Functions, NCP Function.  
- **sample image**:
  ```
  Code Upload → 자동 실행 (트리거 기반)
  Server 관리 X
  ```

---

### 102 Edge Computing (엣지 컴퓨팅)
- **meaning**: 데이터를 중앙 서버 대신 사용자와 가까운 ‘엣지(Edge)’ 장치에서 처리하는 기술.  
- **simple explanation**: 데이터를 멀리 보내지 않고 근처에서 빠르게 처리하는 구조.  
- **example**: Cloudflare Workers, AWS Greengrass.  
- **sample image**:
  ```
  IoT Device ↔ Edge Node ↔ Cloud
  (근처에서 빠르게 연산)
  ```

---

### 103 Message Queue (메시지 큐)
- **meaning**: 서비스 간 데이터를 안전하게 전달하기 위한 비동기 메시징 시스템.  
- **simple explanation**: 한 서비스가 보낸 메시지를 큐에 담아 다른 서비스가 나중에 꺼내보는 구조.  
- **example**: RabbitMQ, AWS SQS, Kafka.  
- **sample image**:
  ```
  Producer → [Message Queue] → Consumer
  ```

---

### 104 Version Control (버전 관리)
- **meaning**: 코드나 문서의 변경 이력을 기록하고 이전 버전으로 되돌릴 수 있게 하는 시스템.  
- **simple explanation**: 과거로 돌아가거나 협업을 쉽게 해주는 ‘시간 여행 도구’.  
- **example**: Git, GitHub, GitLab.  
- **sample image**:
  ```
  v1.0 → v1.1 → v2.0 (히스토리 관리)
  ```

---

### 105 Load Testing (부하 테스트)
- **meaning**: 많은 트래픽을 발생시켜 시스템의 한계를 테스트하는 과정.  
- **simple explanation**: 서버가 몇 명까지 버틸 수 있는지 실험하는 것.  
- **example**: JMeter, k6, Locust.  
- **sample image**:
  ```
  1000명 동시 접속 시 응답속도 측정
  ```

---

### 106 API Gateway
- **meaning**: 여러 서비스의 API를 한 곳에서 통합 관리하고 인증, 라우팅, 모니터링을 담당하는 진입점.  
- **simple explanation**: 모든 요청이 먼저 통과하는 ‘API 입구 관리자’.  
- **example**: AWS API Gateway, Kong Gateway.  
- **sample image**:
  ```
  Client → API Gateway → Auth / Route → Services
  ```

---

### 107 Monitoring (모니터링)
- **meaning**: 시스템의 상태를 지속적으로 감시하여 문제를 조기에 발견하는 행위.  
- **simple explanation**: 서버의 건강 상태를 실시간으로 지켜보는 역할.  
- **example**: CloudWatch, Prometheus.  
- **sample image**:
  ```
  📊 CPU 80% → Alert → 관리자 확인
  ```

---

### 108 Observability Tools (관찰성 도구)
- **meaning**: 로그, 메트릭, 트레이스를 통합 분석하여 시스템의 내부 상태를 파악하는 도구.  
- **simple explanation**: 문제의 원인을 ‘보이게’ 만들어주는 도구 모음.  
- **example**: Grafana, Datadog, New Relic.  
- **sample image**:
  ```
  Logs + Metrics + Traces → 시각화 분석
  ```

---

### 109 Secrets Manager
- **meaning**: 비밀번호나 API 키 등 민감한 정보를 안전하게 보관하는 서비스.  
- **simple explanation**: 중요한 비밀정보를 코드 대신 안전한 금고에 저장.  
- **example**: AWS Secrets Manager, HashiCorp Vault.  
- **sample image**:
  ```
  App → [Secrets Manager] → Key 반환
  ```

---

### 110 Bastion Host (점프 서버)
- **meaning**: 외부에서 내부 서버로 안전하게 접속하기 위한 보안 중계 서버.  
- **simple explanation**: 내부망에 직접 들어가기 전 반드시 거쳐야 하는 보안 게이트.  
- **example**: AWS Bastion Host, NCP Jump Server.  
- **sample image**:
  ```
  🧑‍💻 User → Bastion Host → Private Server
  

---
