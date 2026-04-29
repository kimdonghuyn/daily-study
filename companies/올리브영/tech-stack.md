# 올리브영 (CJ올리브영) — 기술 스택

## 언어 / 프레임워크
- **언어**: Java, Kotlin
- **백엔드**: Spring Framework, Spring Boot, SpringBatch
- **빅데이터**: BigQuery

## 데이터베이스
- Aurora Serverless (MySQL 호환)
- BigQuery (데이터 웨어하우스, Greenplum에서 전환)
- Redis (캐싱)
- S3 Parquet (분석용)

## 인프라 / 클라우드
- **멀티 클라우드**: AWS + GCP
- AWS: EventBridge, Glue, Athena, S3, Lambda
- Kafka, Redis, Grafana (모니터링)
- SRE 팀 운영

## 아키텍처
- 서버리스 + MSA 혼합
- 이벤트 기반: EventBridge 주기 처리
- 랭킹 시스템: 서버리스 기반 (EventBridge → Glue → Athena → S3), 월 $50 미만 운영

## 채용 주요 요구사항
- Java/Spring 3년 이상
- SpringBatch 배치 처리 경험
- 동기/비동기 처리 연동
- 분산환경 대규모 데이터 처리
- AWS/GCP 경험
- 성능 최적화 경험

## 기술 블로그
- https://oliveyoung.tech/
