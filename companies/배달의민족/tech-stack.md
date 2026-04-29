# 배달의민족 (우아한형제들) — 기술 스택

## 언어 / 프레임워크
- **언어**: Java (8 이상)
- **백엔드**: Spring Framework, Spring Boot
- **ORM**: JPA, QueryDSL

## 데이터베이스
- MySQL, Aurora, MariaDB
- Redis, DynamoDB (다중 캐시 아키텍처)
- Kafka, AWS SNS/SQS (메시징)
- InfluxDB (시계열)

## 인프라 / 클라우드
- AWS 기반
- Kafka, SNS/SQS (메시징)
- Prometheus, Grafana, InfluxDB (모니터링)
- Airflow, Athena (추천/통계)
- Spark (데이터 처리)
- Reactor (비동기)

## 아키텍처
- 완전한 MSA (서비스 간 독립)
- 이벤트 기반 아키텍처
- 다중 저장소 패턴 (Redis + DynamoDB 캐시)
- 대규모 트래픽 처리 특화 (배차, 주문)

## 채용 주요 요구사항
- Java 객체지향 설계 3년 이상
- Spring Framework/Boot 실무
- JPA, QueryDSL ORM 경험
- MySQL/Aurora 운영 경험
- MSA 이해
- AWS SNS/SQS 우대
- Kafka 메시징 시스템 우대

## 기술 블로그
- https://techblog.woowahan.com/
