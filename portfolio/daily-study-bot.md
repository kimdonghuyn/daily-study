# Daily Study Bot — 포트폴리오

> 마지막 업데이트: 2026-05-09 | 누적 학습일: 1일 | 현재 레벨: Lv.1 (5 XP)

백엔드 개발자 취업 준비를 위한 **자동 학습 Slack 봇**.
매일 AI가 기술 질문 3문제를 생성·발송하고, 답변의 정확도를 0~100점으로 채점해 XP를 부여합니다.

---

## 문제 정의

> "매일 학습 계획을 세워도 작심삼일. 실행을 자동화하지 않으면 꾸준함을 유지할 수 없다."

- 백엔드 개념은 방대해 혼자 범위를 정하기 어려움
- 배운 내용을 다음 날 복습하지 않으면 빠르게 휘발됨
- 면접 대비를 위한 구조화된 질문·피드백 루프가 없음

---

## 시스템 흐름

```
[저녁] Slack: "!학습 오늘 Spring AOP 공부했어"
  └─ Claude API: 토픽 자동 매핑 → 내일 아침 토픽 Redis 저장

[08:00 KST] GitHub Actions
  └─ profile.json에서 현재 레벨 조회
  └─ Redis에서 사용자 지정 토픽 확인 (없으면 랜덤)
  └─ Claude API: 개념/문제/면접 3문제 병렬 생성 (800 tokens each)
  └─ Slack: 토픽 요약 + 질문 3개 개별 메시지 발송

[낮] Slack: 사용자 답변 입력
  └─ Vercel Edge Function: Slack 서명 검증 (Web Crypto API)
  └─ Claude API: 0~100점 채점 + 피드백 생성 (JSON 구조화 응답)
  └─ Slack: 스레드에 피드백 + 점수 표시
  └─ Redis: 점수·피드백 저장

[13:00 KST] GitHub Actions
  └─ Claude API: 모범 답안 3개 병렬 생성
  └─ Slack: 모범 답안 3개 개별 메시지 발송
  └─ XP 계산: baseXP(40) × (score / 100), 최소 5XP
  └─ GitHub: daily-study-bot/logs/ 커밋
  └─ GitHub: daily-study/ profile.json·README·daily-log·portfolio 자동 업데이트
```

---

## 핵심 기술 결정

### 1. Vercel Edge Runtime 선택 — Slack 서명 검증

Slack 웹훅 서명 검증은 파싱 전 **raw body**가 필요. Vercel Node.js Runtime에서는 body가 이미 소진된 상태로 전달돼 raw body 재현 불가. Edge Runtime의 `request.text()`로 해결. Node.js `crypto` 대신 Web Crypto API(`crypto.subtle`) 사용.

### 2. AI 응답 구조화 — JSON 채점

피드백과 점수를 하나의 API 호출로 동시에 얻기 위해 AI에게 순수 JSON으로만 응답하도록 프롬프트 설계. 파싱 실패 시 regex로 JSON 블록 추출, 최종 실패 시 기본값(50점) fallback.

```js
const jsonMatch = raw.match(/\{[\s\S]*\}/);
const parsed = JSON.parse(jsonMatch[0]);
return { score: Number(parsed.score), feedback: String(parsed.feedback) };
```

### 3. 3문제 병렬 생성 — Promise.all

개념/문제/면접 3문제를 순차 생성하면 ~6초. `Promise.all`로 병렬화해 ~2초로 단축. 각 질문은 독립적이라 병렬화 부작용 없음.

### 4. Slack 메시지 분리 발송 — 블록 한도 회피

3문제를 하나의 Slack 메시지에 담으면 블록 페이로드 한도를 초과해 내용이 잘림. 토픽 요약 헤더 1개 + 질문별 개별 메시지 3개로 분리해 해결.

### 5. 레벨 기반 난이도 자동 조절

morning.js가 `daily-study/profile.json`에서 현재 XP를 읽어 레벨 계산 후 프롬프트에 난이도 가이드 삽입. 코드 변경 없이 학습자의 성장에 맞게 질문 수준이 자동으로 올라감.

### 6. 타겟 회사 맥락 시나리오

문제 상황 질문에 오늘의집·무신사·컬리·올리브영·배달의민족 5개사의 서비스 특성을 프롬프트에 명시. AI가 토픽과 가장 잘 어울리는 회사를 선택해 현실감 있는 장애 시나리오 생성.

### 7. 크로스 레포 연동 — PAT 분리

`daily-study-bot` 레포는 `GITHUB_TOKEN`(자동 발급), `daily-study` 레포는 별도 PAT(`STUDY_GITHUB_TOKEN`) 사용. 두 레포의 write 권한을 최소 범위로 분리.

---

## 트러블슈팅 요약

| # | 문제 | 원인 | 해결 |
|---|------|------|------|
| 1 | Slack 서명 검증 401 | Vercel Node.js Runtime에서 body 스트림 소진 | Edge Runtime + `request.text()` 전환 |
| 2 | Redis JSON 이중 파싱 오류 | `@upstash/redis` 자동 역직렬화 | `typeof data === 'string'` 타입 가드 |
| 3 | Slack 메시지 3000자 잘림 | Block Kit section 3000자 제한 | `splitTextBlocks()` 2900자 분할 헬퍼 |
| 4 | 3문제 메시지 페이로드 잘림 | 단일 메시지 블록 총량 한도 초과 | 질문별 개별 메시지 분리 발송 |
| 5 | UTC/KST 날짜 불일치 | `new Date().toISOString()`이 UTC 기준 | KST 오프셋 +9h 적용 통일 |
| 6 | 이벤트 미수신 | OAuth 스코프 변경 후 앱 재설치 누락 | Slack 앱 Reinstall to Workspace |
| 7 | AI 엔진 품질 이슈 | 무료 엔진(Gemini, Groq) 피드백 정확도 부족 | Claude Haiku 4.5로 회귀 |

---

## 기술 스택

| 분류 | 기술 | 선택 이유 |
|------|------|----------|
| Runtime | Node.js 20 (ES Modules) | GitHub Actions 기본 환경 |
| AI | Claude API (claude-haiku-4-5) | 피드백 정확도 + 비용 균형 |
| Hosting | Vercel Edge Functions | raw body 접근 + 저지연 |
| Scheduler | GitHub Actions cron | 별도 서버 불필요 |
| Storage | Upstash Redis (REST) | Edge Runtime에서 HTTP로 접근 가능 |
| Messaging | Slack Web API + Events API | |

---

## 학습 현황 (자동 갱신)

| 항목 | 값 |
|------|-----|
| 누적 학습일 | 1일 |
| 현재 레벨 | Lv.1 |
| 총 XP | 5 |
| 연속 학습 | 1일 |
| 완료 퀘스트 | 1개 |
| 획득 뱃지 | 🔥 첫 불꽃 |

> 이 문서는 [daily-study-bot](https://github.com/kimdonghuyn/daily-study-bot)이 매일 13:00 KST에 자동으로 업데이트합니다.
