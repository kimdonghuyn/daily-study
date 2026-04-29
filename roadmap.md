# 🗺️ 백엔드 엔지니어 취업 로드맵

**목표**: 오늘의집 / 무신사 / 컬리 / 올리브영 / 배달의민족
**기간**: 6개월 (2026.04 ~ 2026.10)
**베이스**: Java / Spring Boot

---

## 전체 흐름

```
Phase 1       Phase 2       Phase 3       Phase 4       Phase 5       Phase 6
(Month 1)     (Month 2)     (Month 3)     (Month 4)     (Month 5)     (Month 6)
   │             │             │             │             │             │
Java/Spring   DB 심화       아키텍처       인프라 &      고급 패턴 &   면접 &
기초 정립     & API 설계    & Kafka        AWS           보안 & AI    포트폴리오
```

---

## Phase 1 — Java / Spring Boot 기초 정립 (Month 1)
> 모든 목표 회사의 공통 기반. 여기가 흔들리면 면접에서 무너짐.

### 핵심 주제
| 주제 | 퀘스트 예시 | 완료 |
|------|------------|------|
| JVM 동작 원리 | GC 종류와 동작 방식 정리 | ⬜ |
| OOP 4대 원칙 | 실제 코드 예시로 설명 | ⬜ |
| SOLID 원칙 | 각 원칙 위반 사례 + 개선 | ⬜ |
| Spring IoC / DI | Bean 생명주기, 스코프 정리 | ⬜ |
| Spring AOP | 프록시 동작 원리, @Transactional 연결 | ⬜ |
| @Transactional | 전파 수준 6가지, 롤백 조건 | ⬜ |
| Spring MVC 흐름 | DispatcherServlet → Controller 흐름 | ⬜ |
| 예외 처리 전략 | @ExceptionHandler, @ControllerAdvice | ⬜ |

### 목표 XP: 120 XP

---

## Phase 2 — DB 심화 & API 설계 (Month 2)
> 5개 회사 모두 MySQL + Redis 사용. DB는 반드시 깊게.

### 핵심 주제
| 주제 | 퀘스트 예시 | 완료 |
|------|------------|------|
| 인덱스 (B-Tree) | 어떻게 동작하는지, 복합 인덱스 순서 | ⬜ |
| ACID & 트랜잭션 | 예시로 설명, 실패 시나리오 | ⬜ |
| 격리 수준 4가지 | 각 수준별 문제 (Dirty Read 등) | ⬜ |
| N+1 문제 | JPA에서 발생 원인 + 해결 (fetch join) | ⬜ |
| 샤딩 & 파티셔닝 | 차이점, 언제 쓰나 | ⬜ |
| DB 복제 (Replication) | Master-Slave 구조, 장단점 | ⬜ |
| Redis 자료구조 | 5가지 + 실제 사용 사례 | ⬜ |
| 캐싱 전략 3가지 | Look-aside, Write-through, Write-back | ⬜ |
| 캐시 무효화 | 문제점 + 해결 전략 | ⬜ |
| REST API 설계 | 버저닝, 멱등성, 상태코드 | ⬜ |
| gRPC + Protobuf | 기본 개념, REST와 차이 | ⬜ |

### 목표 XP: 150 XP

---

## Phase 3 — 아키텍처 & Kafka (Month 3)
> MSA + Kafka는 5개 회사 공통. 배달의민족, 오늘의집 필수.

### 핵심 주제
| 주제 | 퀘스트 예시 | 완료 |
|------|------------|------|
| MSA vs 모놀리식 | 트레이드오프, 전환 기준 | ⬜ |
| API Gateway 패턴 | 역할, 장단점 | ⬜ |
| 서비스 디스커버리 | Eureka, Consul 개념 | ⬜ |
| Kafka 기본 개념 | Topic, Partition, Consumer Group | ⬜ |
| Kafka vs RabbitMQ | 차이점, 선택 기준 | ⬜ |
| 이벤트 기반 아키텍처 | 장단점, 사용 패턴 | ⬜ |
| Backpressure | 개념 + 대응 전략 | ⬜ |
| CAP 정리 | 실제 사례와 연결 | ⬜ |
| 확장성 설계 | 수평/수직 확장, 로드밸런서 | ⬜ |
| 시스템 설계 실전 | 배민 같은 서비스 설계 스케치 | ⬜ |

### 목표 XP: 150 XP

---

## Phase 4 — 인프라 & AWS (Month 4)
> 클라우드 없이 현대 백엔드 없다. AWS 핵심만 집중.

### 핵심 주제
| 주제 | 퀘스트 예시 | 완료 |
|------|------------|------|
| Docker 기초 | 이미지, 컨테이너, Dockerfile | ⬜ |
| Docker Compose | 멀티 컨테이너 구성 | ⬜ |
| Kubernetes 기초 | Pod, Deployment, Service, Ingress | ⬜ |
| AWS EC2 / S3 / RDS | 핵심 서비스 개념 | ⬜ |
| AWS SNS / SQS | 차이점 + 배달의민족 사례 연결 | ⬜ |
| AWS Lambda | 서버리스 개념 + 올리브영 랭킹 사례 | ⬜ |
| CI/CD 개념 | GitHub Actions, Jenkins 흐름 | ⬜ |
| 모니터링 기초 | Prometheus + Grafana 개념 | ⬜ |
| 로깅 전략 | 구조화 로그, ELK Stack | ⬜ |
| 분산 추적 | OpenTelemetry, Jaeger 개념 | ⬜ |

### 목표 XP: 140 XP

---

## Phase 5 — 고급 패턴 & 보안 & AI (Month 5)
> 시니어 수준의 깊이. 면접 차별화 포인트.

### 핵심 주제
| 주제 | 퀘스트 예시 | 완료 |
|------|------------|------|
| 동시성 & Race Condition | 실제 코드 예시, Lock 전략 | ⬜ |
| Optimistic vs Pessimistic Lock | DB Lock vs 애플리케이션 Lock | ⬜ |
| 분산 락 (Redisson) | Redis 기반 분산 락 구현 | ⬜ |
| Circuit Breaker | Resilience4j 개념 + 사례 | ⬜ |
| Retry & Exponential Backoff | 구현 방법과 주의점 | ⬜ |
| Rate Limiting | 토큰 버킷, 슬라이딩 윈도우 | ⬜ |
| OAuth2 & JWT | 인증 흐름, 취약점 | ⬜ |
| OWASP Top 10 | 주요 취약점 + 방어 방법 | ⬜ |
| 성능 튜닝 | 병목 분석, 쿼리 최적화 | ⬜ |
| AI 통합 (RAG) | LLM API 연동, 벡터 DB 개념 | ⬜ |

### 목표 XP: 160 XP

---

## Phase 6 — 면접 준비 & 포트폴리오 (Month 6)
> 학습한 것을 면접에서 말할 수 있도록.

### 핵심 주제
| 주제 | 퀘스트 예시 | 완료 |
|------|------------|------|
| 회사별 채용 공고 분석 | 5개 회사 JD 분석 + 갭 파악 | ⬜ |
| 예상 면접 질문 100선 | 주제별 답변 정리 | ⬜ |
| 포트폴리오 프로젝트 | 배운 기술 적용한 미니 프로젝트 | ⬜ |
| 기술 블로그 정리 | 학습 내용 외부 공개용 정리 | ⬜ |
| 모의 면접 | 주제별 Q&A 실전 연습 | ⬜ |

### 목표 XP: 200 XP

---

## 월별 목표 XP 요약

| 월차 | Phase | 목표 XP | 누적 XP | 예상 레벨 |
|------|-------|---------|---------|---------|
| 1개월 | Phase 1 | 120 | 120 | Lv.2 |
| 2개월 | Phase 2 | 150 | 270 | Lv.3 |
| 3개월 | Phase 3 | 150 | 420 | Lv.4 |
| 4개월 | Phase 4 | 140 | 560 | Lv.5 |
| 5개월 | Phase 5 | 160 | 720 | Lv.6 |
| 6개월 | Phase 6 | 200 | 920 | Lv.7 |

---

## 매일 루틴

```
아침 (30~60분)
  └── 오늘의 퀘스트 2~3개 선택
  └── 개념 학습 + 노트 정리

저녁 (15분)
  └── daily-log 작성
  └── XP 업데이트
  └── git push
```

---

## 우선순위 기술 (5개 회사 공통)

```
★★★ 필수     Java/Spring Boot, MySQL, Redis, REST API
★★☆ 중요     Kafka, MSA, AWS, JPA/QueryDSL
★☆☆ 우대     gRPC, Kubernetes, 분산 락, AI 통합
```
