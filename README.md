# ux-audit

서비스의 사용자 경험을 절차대로 점검해 `검증 가능한 Improvement Backlog`로 변환하는 Claude Code 스킬

불편한 점의 나열이 아니라, 모든 항목이 다음 사슬을 갖추도록 강제하는 것이 목적

```
Observation → Problem → Hypothesis → Recommendation → Verification
```

- 사슬이 끊긴 항목은 Backlog 제외

## 설치

Claude Code에서 아래 두 줄 실행 (권장)

```
/plugin marketplace add snhomeground-cell/ux-audit-skill
/plugin install ux-audit@ux-audit-skill
```

수동 설치를 원할 경우 저장소를 스킬 폴더로 복제

```bash
git clone https://github.com/snhomeground-cell/ux-audit-skill.git ~/.claude/skills/ux-audit
```

`SKILL.md` 한 파일만 내려받아 아래 위치에 배치해도 동작

| 운영체제 | 경로 |
|---|---|
| macOS / Linux | `~/.claude/skills/ux-audit/SKILL.md` |
| Windows | `%USERPROFILE%\.claude\skills\ux-audit\SKILL.md` |

- 특정 프로젝트 전용으로 쓸 경우 해당 프로젝트의 `.claude/skills/ux-audit/`에 배치

## 사용

Claude Code에서 `/ux-audit` 호출, 또는 아래 표현으로 실행

- "UX 점검해줘"
- "이 서비스 써보고 문제 찾아줘"
- "사용자 입장에서 봐줘"
- "접근성 점검해줘"
- "개선할 거 뽑아줘"

착수 게이트로 대상·접근 수단·관점·산출물 경로 4가지를 먼저 확정한 뒤 진행

## 절차

1. Service Understanding — 서비스 목적·기능·화면·권한 구조 파악
2. User Type Identification — 인구통계가 아닌 사용 목적과 행동 패턴으로 구분
3. Persona Creation — 사용자 조사 결과가 없으면 Hypothetical Persona로 명시
4. Task & Success Criteria — 성공 여부를 판정 가능한 문장으로 작성
5. Task-based Exploration — 가능한 경우 실제 조작, 화면을 근거로 기록
6. Simulated Think-Aloud Analysis — 실제 사용자 테스트와 구분해 표기
7. Cognitive Walkthrough — 단계별 4개 질문으로 평가
8. Heuristic Evaluation — 10개 항목, 점수가 아닌 근거 기재
9. Accessibility Review — 자동 확인 불가 항목은 수동 검증 필요로 표시
10. Edge Case Review — 미테스트 항목은 Potential Edge Case로 구분
11. Issue Identification — 관찰과 해석의 분리
12. Severity / Confidence — 두 축을 별도 평가
13. Recommendation — 정답이 아닌 검증 대상 가설로 제시
14. Improvement Backlog — P0 · P1 · P2 · P3 · Later
15. Re-validation Plan — 개선 후 동일 기준으로 재검증

## 산출물 구성

Executive Summary, Service Overview, Personas, Tasks, Key Findings, Detailed Issues,
Heuristic Evaluation, Accessibility Findings, Edge Cases, Improvement Backlog,
Validation Required, Re-validation Plan 순서

- Detailed Issues는 심각도순이 아니라 사용자가 실제로 겪는 Task 흐름 순으로 배열
- 심각도는 Key Findings와 Backlog에서 취급

## 설계 원칙

- 관찰한 사실(`Fact`)·전제(`Assumption`)·추론(`Hypothesis`)을 표기로 구분
- 확인하지 못한 항목은 `Unknown`으로 유지, 빈칸을 추측으로 채우지 않음
- 수행하지 않은 테스트를 수행한 것으로 기록하지 않음
- AI가 생성한 Persona를 실제 사용자 조사 결과로 취급하지 않음
- Severity와 Confidence는 별개의 축. Severity 높음 + Confidence 낮음이면 사용자 검증이 선행
- Audit 종료 전 서비스 코드 미수정
- 사용성 문제와 개인적 디자인 취향의 구분

## 라이선스

MIT
