# 퀘스트 풀

매일 아침 여기서 퀘스트를 골라서 진행해요.
완료하면 daily-log에 체크하고 XP를 profile.md에 기록하세요.

---

## 🏗️ 시스템 설계

| 퀘스트 | 타입 | XP | 스킬 |
|--------|------|----|------|
| 확장성(Scalability) vs 가용성(Availability) 트레이드오프 정리 | ✍️ | 10 | MSA |
| CAP 정리란? 실제 사례로 설명하기 | ✍️ | 10 | MSA |
| 수평 확장 vs 수직 확장 차이와 언제 쓰는지 | ✍️ | 10 | MSA |
| 로드 밸런서 동작 방식 정리 (L4 vs L7) | ✍️ | 10 | MSA |
| 배달의민족 / 쿠팡 같은 서비스 시스템 설계 스케치 | 💻 | 20 | MSA |

## 🗄️ 데이터베이스

| 퀘스트 | 타입 | XP | 스킬 |
|--------|------|----|------|
| 인덱스 동작 원리 (B-Tree) 개념 정리 | ✍️ | 10 | DB |
| 트랜잭션 ACID란? 예시와 함께 설명 | ✍️ | 10 | DB |
| 격리 수준 4가지 (READ UNCOMMITTED ~ SERIALIZABLE) 정리 | ✍️ | 10 | DB |
| N+1 문제란? JPA에서 어떻게 해결하나 | 💡 | 15 | DB |
| 샤딩 vs 파티셔닝 차이 정리 | ✍️ | 10 | DB |
| DB 복제(Replication) 동작 방식과 장단점 | ✍️ | 10 | DB |
| 실제 쿼리 튜닝 경험 면접 답변 준비 | 💡 | 15 | DB |

## 🌐 API 설계

| 퀘스트 | 타입 | XP | 스킬 |
|--------|------|----|------|
| REST vs gRPC 차이점과 선택 기준 정리 | ✍️ | 10 | MSA |
| REST API 버저닝 전략 (URL vs Header vs Media Type) | ✍️ | 10 | MSA |
| 멱등성(Idempotency)이란? 어떤 메서드가 멱등한가? | 💡 | 15 | MSA |
| GraphQL 기본 개념과 REST와의 차이 | 📖 | 5 | MSA |
| gRPC + Protobuf 간단 실습 | 💻 | 20 | MSA |

## 📨 비동기 / Kafka

| 퀘스트 | 타입 | XP | 스킬 |
|--------|------|----|------|
| Kafka 기본 개념 (Topic, Partition, Consumer Group) 정리 | ✍️ | 10 | Kafka |
| 메시지 큐 vs 이벤트 스트리밍 차이 정리 | ✍️ | 10 | Kafka |
| 이벤트 기반 아키텍처 장단점 정리 | ✍️ | 10 | Kafka |
| Backpressure란? 어떻게 다루나 | 💡 | 15 | Kafka |
| Kafka 로컬 실습 (Producer/Consumer 만들기) | 💻 | 20 | Kafka |
| 배달의민족 기술 블로그 Kafka 관련 글 읽기 | 📖 | 5 | Kafka |

## 🔴 캐싱

| 퀘스트 | 타입 | XP | 스킬 |
|--------|------|----|------|
| Redis 자료구조 5가지 + 사용 예시 정리 | ✍️ | 10 | DB |
| 캐시 전략 3가지 (Look-aside, Write-through, Write-back) | ✍️ | 10 | DB |
| 캐시 무효화(Cache Invalidation) 문제와 해결 전략 | 💡 | 15 | DB |
| CDN이란? 어떤 상황에서 쓰나 | ✍️ | 10 | AWS |
| Redis 분산 락(Redisson) 개념 정리 | ✍️ | 10 | DB |

## ⚡ 동시성 / 일관성

| 퀘스트 | 타입 | XP | 스킬 |
|--------|------|----|------|
| Race Condition이란? 실제 코드 예시로 설명 | 💡 | 15 | Java |
| Optimistic Lock vs Pessimistic Lock 차이 | ✍️ | 10 | DB |
| 데드락 발생 조건 + 예방 방법 | ✍️ | 10 | DB |
| Java synchronized vs ReentrantLock 차이 | 💡 | 15 | Java |
| Spring @Transactional 동작 원리 (프록시) | 💡 | 15 | Spring |

## 🛡️ 신뢰성 패턴

| 퀘스트 | 타입 | XP | 스킬 |
|--------|------|----|------|
| Circuit Breaker 패턴이란? (Resilience4j) | ✍️ | 10 | MSA |
| Retry 전략과 Exponential Backoff 정리 | ✍️ | 10 | MSA |
| Rate Limiting 구현 방법 (토큰 버킷, 슬라이딩 윈도우) | 💡 | 15 | MSA |
| 오늘의집 / 배민 기술블로그 장애 대응 사례 읽기 | 📖 | 5 | MSA |

## 👁️ 관찰 가능성 (Observability)

| 퀘스트 | 타입 | XP | 스킬 |
|--------|------|----|------|
| 로깅 vs 메트릭 vs 트레이싱 차이 정리 | ✍️ | 10 | AWS |
| OpenTelemetry란? 어떻게 동작하나 | 📖 | 5 | AWS |
| Prometheus + Grafana 모니터링 개념 정리 | ✍️ | 10 | AWS |
| 분산 추적(Distributed Tracing)이 왜 필요한가? | 💡 | 15 | MSA |

## ☁️ AWS / 인프라

| 퀘스트 | 타입 | XP | 스킬 |
|--------|------|----|------|
| AWS SNS vs SQS 차이 + 사용 사례 | ✍️ | 10 | AWS |
| AWS Lambda (서버리스) 개념과 장단점 | ✍️ | 10 | AWS |
| Docker 기본 개념 (이미지, 컨테이너, 레이어) | ✍️ | 10 | AWS |
| Kubernetes 기본 개념 (Pod, Deployment, Service) | ✍️ | 10 | AWS |
| GitOps란? ArgoCD 개념 정리 | 📖 | 5 | AWS |

## 🔐 보안

| 퀘스트 | 타입 | XP | 스킬 |
|--------|------|----|------|
| OAuth2 동작 흐름 (Authorization Code Grant) 정리 | ✍️ | 10 | Spring |
| JWT 구조와 서명 방식 정리 | 💡 | 15 | Spring |
| OWASP Top 10 훑어보기 | 📖 | 5 | CS |
| SQL Injection 방어 방법 | 💡 | 15 | DB |

## 🤖 AI 통합 (2026 트렌드)

| 퀘스트 | 타입 | XP | 스킬 |
|--------|------|----|------|
| LLM API 연동 개념 정리 (OpenAI / Claude) | 📖 | 5 | CS |
| 벡터 데이터베이스란? (Pinecone, pgvector) | ✍️ | 10 | DB |
| RAG(검색 증강 생성) 아키텍처 개념 정리 | ✍️ | 10 | CS |
| 백엔드에서 AI 기능 붙이는 설계 패턴 | 💡 | 15 | MSA |

## 🎯 회사 공략 퀘스트

| 퀘스트 | 타입 | XP |
|--------|------|----|
| 오늘의집 채용 공고 분석 + 부족한 기술 파악 | 🔍 | 10 |
| 무신사 채용 공고 분석 + 부족한 기술 파악 | 🔍 | 10 |
| 컬리 채용 공고 분석 + 부족한 기술 파악 | 🔍 | 10 |
| 올리브영 채용 공고 분석 + 부족한 기술 파악 | 🔍 | 10 |
| 배달의민족 채용 공고 분석 + 부족한 기술 파악 | 🔍 | 10 |
| 우아한형제들 기술블로그 글 1개 읽고 요약 | 📖 | 5 |
| 올리브영 기술블로그 글 1개 읽고 요약 | 📖 | 5 |
| 컬리 기술블로그 글 1개 읽고 요약 | 📖 | 5 |
