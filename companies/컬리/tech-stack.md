# 컬리 (마켓컬리 / Kurly) — 기술 스택

## 언어 / 프레임워크
- **레거시**: PHP, Laravel
- **신규**: Java, Spring Boot
- **전환 중**: Spring Cloud Netflix 기반 MSA로 이관

## 데이터베이스
- MySQL, MariaDB, AWS Aurora
- Redis (캐싱)

## 인프라 / 클라우드
- AWS 기반 (2019년 전환 완료)
- Jenkins, Ansible, Docker
- SonarQube, Clair (코드 품질 / 보안)
- Prometheus, Grafana (모니터링)
- ELK Stack, Lambda, Terraform, Consul

## 아키텍처
- 모놀리식(PHP) → MSA 점진적 전환
- Spring Cloud Netflix 기반
- 멀티 레이어: 회원/상품/주문(PHP) + 앱API(Laravel) + 검색(Java/Spring)

## 채용 주요 요구사항
- Spring/Spring Boot 3년 이상
- MySQL/MariaDB 깊이 있는 이해
- 성능 최적화, 트러블슈팅 경험
- PG / 간편결제 시스템 이해
- 핀테크 시스템 경험 우대

## 기술 블로그
- https://helloworld.kurly.com/
