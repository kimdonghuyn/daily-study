# Daily Study Bot — 포트폴리오 기록

## 프로젝트 개요

백엔드 취업 준비를 위해 직접 설계하고 구현한 자동 학습 시스템.
매일 AI가 질문을 생성하고, 사용자 답변에 실시간 피드백을 주며, 모범 답안을 자동 발송한다.

**GitHub**: https://github.com/kimdonghuyn/daily-study-bot

---

## 문제 정의

> "매일 꾸준히 학습하고 싶은데, 혼자 하면 무엇을 공부해야 할지 막막하고 지속하기 어렵다."

- 매일 학습 주제를 스스로 정하는 데 드는 마찰 제거
- 내 답변이 맞는지 확인할 수단 부재
- 학습 기록이 쌓이지 않아 성장이 보이지 않음

---

## 해결 방법

```
08:00 KST   Claude AI가 오늘의 질문 생성 → Slack 발송
            (개념 설명 / 문제 상황 / 면접 질문 3가지 유형 중 랜덤)

사용자 답변 → Slack에 메시지 입력
            → 즉시 AI 피드백 (잘한 점 / 보완할 점 / 핵심 포인트)

13:00 KST   모범 답안 + 개념 정리 자동 발송
```

---

## 아키텍처

```
┌─────────────────────────────────────────────────────┐
│                  GitHub Actions                      │
│  cron: 0 23 * * * (08:00 KST)  →  morning.js       │
│  cron: 0 4  * * * (13:00 KST)  →  afternoon.js     │
└──────────────┬──────────────────────────────────────┘
               │ Claude API 호출 (질문/답안 생성)
               ▼
┌─────────────────────────────────────────────────────┐
│              Upstash Redis                           │
│  오늘의 질문 저장 / 사용자 답변 저장 (2일 TTL)       │
└──────────────┬──────────────────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────────────────┐
│                 Slack                                │
│  질문 발송 → 사용자 답변 → 피드백 응답               │
└──────────────┬──────────────────────────────────────┘
               │ 메시지 이벤트
               ▼
┌─────────────────────────────────────────────────────┐
│          Vercel Serverless (api/slack.js)            │
│  Slack Events API 수신                               │
│  → Claude API 피드백 생성                            │
│  → Slack 스레드에 응답                               │
└─────────────────────────────────────────────────────┘
```

---

## 기술적 의사결정

### 왜 GitHub Actions를 스케줄러로 선택했나?
- 별도 서버 없이 크론 스케줄링 가능
- 무료, 안정적, 로그 추적 용이
- `workflow_dispatch`로 수동 테스트 가능

### 왜 Vercel을 Slack Bot 호스팅으로 선택했나?
- Slack Events API는 항상 켜진 엔드포인트 필요
- GitHub Actions는 일회성 실행 → 이벤트 수신 불가
- Vercel Serverless + `waitUntil`로 3초 타임아웃 문제 해결

### 왜 Upstash Redis를 선택했나?
- GitHub Actions와 Vercel이 서로 다른 런타임 → 공유 상태 필요
- Serverless 환경에 최적화된 HTTP 기반 Redis
- 무료 티어로 일일 메시지 수준은 충분

### Slack 3초 타임아웃 해결
```js
// 즉시 200 응답 후 백그라운드에서 Claude API 호출
res.status(200).end();
waitUntil(handleMessage(event)); // Vercel waitUntil
```

---

## 기술 스택

| 분류 | 기술 |
|------|------|
| Runtime | Node.js 20 (ES Modules) |
| AI | Claude API (claude-opus-4-6) |
| 스케줄러 | GitHub Actions (cron) |
| 봇 호스팅 | Vercel Serverless Functions |
| 저장소 | Upstash Redis |
| 메시징 | Slack Web API + Events API |
| 보안 | HMAC-SHA256 Slack 서명 검증 |

---

## 구현 날짜

2026-05-06
