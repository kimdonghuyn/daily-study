# Daily Study Bot — 포트폴리오

**GitHub**: https://github.com/kimdonghuyn/daily-study-bot

백엔드 취업 준비를 위해 직접 설계·구현한 AI 기반 자동 학습 시스템.

---

## 문제 정의

> "매일 꾸준히 학습하고 싶은데, 혼자 하면 무엇을 공부해야 할지 막막하고 지속하기 어렵다."

- 매일 학습 주제를 스스로 정하는 마찰 제거
- 내 답변이 맞는지 확인할 수단 부재
- 학습 기록이 쌓이지 않아 성장이 보이지 않음

---

## 시스템 흐름

```
08:00 KST   Claude AI → 오늘의 질문 생성 → Slack 발송 → Redis 저장
            (개념 설명 / 문제 상황 / 면접 질문 3가지 유형 중 랜덤)

낮          사용자 답변 → Slack 채널 입력
            → Vercel Edge Function 수신
            → Claude AI 피드백 생성 → Redis 저장
            → Slack 스레드에 즉시 응답

13:00 KST   Claude AI → 모범 답안 생성 → Slack 발송
            → daily-study-bot/logs/YYYY-MM-DD.md GitHub 커밋
            → daily-study 레포: XP 적립 · 뱃지 체크 · README 업데이트
```

---

## 기술 스택

| 분류 | 기술 |
|------|------|
| AI | Claude API (`claude-haiku-4-5`) |
| Hosting | Vercel Edge Functions |
| Scheduler | GitHub Actions (cron) |
| Storage | Upstash Redis |
| Messaging | Slack Web API + Events API |
| 보안 | HMAC-SHA256 Slack 서명 검증 (Web Crypto API) |

---

## 기술적 의사결정 및 트러블슈팅

### 1. Slack 서명 검증 실패 — 2단계 디버깅 끝에 Edge Runtime 전환

**1차**: `getRawBody()`로 raw body 읽으려 했으나 Vercel Node.js Runtime은 body를 자동 파싱해 스트림을 소진 → 함수 무한 대기

**2차**: `JSON.stringify(req.body)`로 재직렬화했으나 Vercel 로그로 expected/received 서명을 직접 비교한 결과 여전히 불일치

```
[slack] expected: v0=08c71b0d494c3...
[slack] received: v0=d25e6d3712135...
```

**해결**: Edge Runtime 전환. `request.text()`로 파싱 전 raw body 직접 획득 → Web Crypto API(`crypto.subtle`)로 HMAC 계산

```js
// Node.js Runtime (실패) — 스트림 소진 후 재직렬화 불일치
const rawBody = JSON.stringify(req.body);

// Edge Runtime (성공) — 파싱 전 raw body 직접 획득
const rawBody = await request.text();
```

---

### 2. `@upstash/redis` 자동 역직렬화로 JSON 이중 파싱 오류

**문제**: 오후 워크플로우에서 `SyntaxError: "[object Object]" is not valid JSON`

**원인**: `@upstash/redis`는 JSON을 자동 역직렬화함 → 이미 객체인 값에 `JSON.parse()` 재호출

**해결**: 타입 가드로 이중 파싱 방지
```js
const data = await redis.get(key);
return typeof data === 'string' ? JSON.parse(data) : data;
```

---

### 3. Slack Block Kit 3,000자 초과로 메시지 잘림

**해결**: 줄바꿈 기준 2,900자 단위로 분할해 다중 블록으로 전송하는 `splitTextBlocks()` 헬퍼 구현

---

### 4. Slack 앱 권한 변경 후 이벤트 미수신

**원인**: OAuth 스코프 변경 후 앱 재설치를 하지 않아 변경된 권한이 미적용

**학습**: URL Verified ✓ 상태와 이벤트 실제 전달은 별개. 스코프 변경 시 반드시 재설치 필요

---

### 5. AI 엔진 교체 이력 (비용 vs 품질 검증)

| 단계 | 엔진 | 이유 |
|------|------|------|
| 초기 | Claude API | 높은 응답 품질 |
| 1차 교체 | Gemini API | 무료 티어 탐색 |
| 2차 교체 | Groq (llama-3.3-70b) | 완전 무료 |
| 최종 | Claude API | 학습 피드백 정확도 우선 |

`lib/claude.js` 단일 파일 캡슐화 → 엔진 교체 시 다른 파일 무변경

---

## 학습 이력 관리 연동

매일 학습이 완료되면 [`daily-study`](https://github.com/kimdonghuyn/daily-study) 레포가 자동 업데이트된다.

- `profile.json` — XP·스트릭·스킬·뱃지 통계 원본
- `profile.md` — 상세 프로필 자동 재생성
- `README.md` — 진행도 바·스킬 레벨·뱃지·최근 기록 시각화
- `daily-log/YYYY-MM-DD.md` — 질문·답변·피드백·모범답안 학습 일지

**XP 시스템**: 질문 유형별 10~15 XP + 연속 학습 스트릭 보너스(3일 +10, 7일 +30, 30일 +100) + 토픽별 스킬 XP 분배 + 달성 조건 충족 시 뱃지 자동 해금

---

## 구현 기간

2026-05-06 ~ 2026-05-07 (2일, 개인 프로젝트)