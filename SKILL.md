---
name: ux-audit
description: 서비스의 사용자 경험을 절차대로 점검해 검증 가능한 Improvement Backlog로 만드는 스킬. 서비스 이해 → 사용자 정의 → Task 정의 → 실제 사용 → 휴리스틱·접근성·엣지케이스 → Issue → 심각도와 확신도 분리 판정 → 개선 가설 → 백로그 → 재검증 순서로 진행한다. 관찰한 사실과 추론을 분리하고, 확인하지 못한 것은 Assumption으로 표시하며, Audit 중에는 코드를 고치지 않는다. 신규·기존·리뉴얼 어느 단계에서나 반복 사용한다. 트리거 — "UX 점검", "UX 감사", "UX 오딧", "사용성 점검해줘", "이 서비스 써보고 문제 찾아줘", "사용자 입장에서 봐줘", "개선할 거 뽑아줘", "접근성 점검해줘", "/ux-audit". 코드 수정·기능 구현·디자인 시안 제작은 범위 밖(백로그 승인 후 별도 작업).
---

# UX Audit

## 0. 이 스킬의 목적

불편한 점을 나열하는 것이 목적이 아니다. `검증 가능한 Improvement Backlog`를 만드는 것이 목적이다.

따라서 모든 항목은 다음 사슬을 갖춰야 한다.

Observation → Problem → Hypothesis → Recommendation → Verification

사슬이 끊긴 항목은 Backlog에 올리지 않는다.

---

## 1. 착수 게이트

작업을 시작하기 전에 다음 4가지를 확정한다. 답을 모르는 채로 진행하지 않는다.

| 항목 | 확인할 것 |
|---|---|
| 대상 | 서비스명, 점검 범위(전체 / 특정 플로우 / 특정 화면) |
| 접근 수단 | 실제 URL·계정으로 사용 가능한지, 코드만 읽을 수 있는지, 캡처만 있는지 |
| 관점 | 어떤 사용자 유형을 기준으로 볼 것인지 |
| 산출물 | 파일 경로와 형식(MD 기본, 분량이 많거나 색이 필요하면 HTML) |

접근 수단은 결과물의 신뢰도를 결정하므로 특히 중요하다. 실제로 만져본 것과 코드로 추정한 것은
Confidence 등급이 달라지며, 이 차이를 보고서에 명시한다.

브라우저로 접근 가능한 서비스라면 실제 조작을 우선한다. Chrome 도구 또는 Playwright로 화면을
열고 Task를 직접 수행하며, 각 단계의 화면을 캡처해 근거로 남긴다.

---

## 2. 표기 규칙

모든 서술은 셋 중 하나로 표시한다. 이 구분이 이 스킬의 핵심이다.

`Fact` — 실제로 확인한 것. 화면 캡처·코드 위치·조작 결과 등 근거를 함께 적는다.
`Assumption` — 확인하지 못해 전제로 둔 것.
`Hypothesis` — UX 원칙이나 페르소나에서 추론한 것으로, 사용자 검증이 필요한 것.

확인하지 못한 내용은 `Unknown`으로 남긴다. 빈칸을 추측으로 채우지 않는다.

수행하지 않은 테스트를 수행한 것처럼 기록하지 않는다. 이 규칙에 예외는 없다.

---

## 3. 절차

### 3.1 Service Understanding

서비스의 목적, 해결하려는 사용자 문제, 주요 기능, 주요 화면, Navigation 구조, 회원과 비회원의
구분, 사용자 권한 구조, 서비스가 기대하는 핵심 사용자 행동을 정리한다.

확실하지 않은 내용은 `Unknown` 또는 `Assumption`으로 표시한다.

### 3.2 User Type Identification

주요 사용자 유형을 식별한다. 연령·성별과 같은 인구통계로 나누지 않고, 사용 목적, 사용 빈도,
서비스 숙련도, 도메인 지식, 행동 패턴, 필요한 기능, 사용 상황의 차이로 구분한다.

### 3.3 Persona Creation

목적과 행동 패턴이 서로 다른 Persona를 만들며, 각각에 Persona ID, 사용자 유형, 현재 상황,
사용 목적, 숙련도, 주요 Needs, 주요 Task를 담는다.

실제 사용자 조사 결과가 없다면 `Hypothetical Persona`임을 명시한다. AI가 만든 Persona를 실제
사용자 데이터처럼 취급하지 않는다.

### 3.4 Task & Success Criteria

각 Persona가 수행해야 할 핵심 Task를 정의하며, Task ID, Persona, Starting Point, Goal,
Expected Flow, Success Criteria를 포함한다.

Success Criteria는 관찰 가능한 문장으로 쓴다. "쉽게 찾을 수 있다"가 아니라 "별도의 안내 없이
게시물을 찾고 댓글 등록까지 완료한다"와 같이 성공 여부를 판정할 수 있어야 한다.

### 3.5 Task-based Exploration

가능한 경우 실제로 Task를 수행하며, 각 단계마다 현재 화면, 수행하려는 행동, 발견 가능한 UI
요소, 선택한 행동, 실제 결과, 예상과의 차이, 진행을 방해한 요소를 기록한다.

확인할 수 없는 동작은 기록하지 않고 Task 상태를 `수행 불가`로 남긴다.

### 3.6 Simulated Think-Aloud Analysis

사용자가 고민할 가능성이 있는 지점을 분석한다. 다음 행동을 찾기 어려운 자리, 버튼의 의미가
불분명한 자리, 용어의 뜻을 추론해야 하는 자리, 현재 상태를 알기 어려운 자리, 행동 결과가 예상과
다른 자리가 해당한다.

이는 실제 사용자 Think-Aloud Test가 아니라 `Simulated Think-Aloud Analysis`이며, 실제 반응이
필요한 항목은 User Testing 대상으로 따로 표시한다.

### 3.7 Cognitive Walkthrough

주요 Task의 각 단계를 네 가지 질문으로 평가한다.

1. 사용자가 현재 무엇을 해야 하는지 알 수 있는가
2. 필요한 행동 또는 UI 요소를 발견할 수 있는가
3. 그 UI 요소가 자신의 목적과 연결된다는 것을 이해할 수 있는가
4. 행동 후 시스템의 반응을 이해할 수 있는가

문제가 발견되면 해당 Task 단계와 함께 기록한다.

### 3.8 Heuristic Evaluation

10개 항목으로 평가하며, 각 항목에 근거를 반드시 붙인다. 점수만 적지 않는다.

1. 시스템 상태의 가시성
2. 현실 세계 및 사용자 언어와의 일치
3. 사용자 통제권과 자유
4. 일관성과 표준
5. 오류 예방
6. 기억보다 인식
7. 사용의 유연성과 효율성
8. 단순하고 명확한 정보 표현
9. 오류 인식·진단·복구 지원
10. 도움말 및 안내

### 3.9 Accessibility Review

색상 대비, 텍스트 가독성, 글자 크기, 클릭·터치 영역, 키보드 탐색, Focus 상태, Form Label,
이미지 대체 텍스트, 오류 메시지 전달 방식, 색상만으로 상태를 구분하는지 여부를 점검한다.

자동으로 확인할 수 없는 항목은 `수동 검증 필요`로 표시한다.

### 3.10 Edge Case Review

빈 입력, 잘못된 입력, 매우 긴 입력, 데이터 없음, 중복 요청, 반복 클릭, 네트워크 오류, 이미지
로딩 실패, 로그인 만료, 권한 없는 접근, 존재하지 않는 URL, 삭제된 데이터 접근, 뒤로가기와
새로고침, 화면 크기 변화를 점검한다.

실제로 테스트하지 못한 항목은 `Potential Edge Case`로 구분한다.

### 3.11 Issue Identification

앞 단계의 발견을 Issue로 변환하며, 관찰과 해석을 반드시 분리한다.

- Issue ID
- Persona
- Task
- Screen / Feature
- Observation (본 것만)
- Expected Behavior
- Actual Behavior
- Problem Hypothesis (해석)
- Evidence
- Severity
- Confidence
- Recommendation
- Verification Method

### 3.12 Severity

`Critical` — 핵심 Task 수행이 불가능하거나 보안·데이터 손실 등 중대한 문제가 발생한다.
`High` — 핵심 Task 수행에 큰 방해가 발생한다.
`Medium` — Task는 수행 가능하나 명확한 불편이나 혼란이 발생한다.
`Low` — 영향이 작거나 주로 완성도·일관성에 관련된다.

### 3.13 Confidence

`High` — 실제 서비스에서 명확하게 관찰되었다.
`Medium` — 관찰 근거는 있으나 사용자 검증이 필요하다.
`Low` — Persona 또는 UX 원칙에 근거한 추정이다.

Severity와 Confidence는 별개의 축이다. Severity High에 Confidence Low라면 중요할 가능성은
있으나 사용자 검증이 먼저다.

### 3.14 Recommendation

특정 UI 구현을 정답처럼 단정하지 않는다. 하나의 문제에 해결 방법이 여럿일 수 있음을 전제로,
개선안은 검증해야 할 가설로 제시하고 검증 방법을 함께 적는다.

### 3.15 Improvement Backlog

Issue를 실행 가능한 작업으로 변환하며, Backlog ID, Related Issue, Objective, Recommended
Change, Priority, Expected Impact, Implementation Scope, Verification Method, Target Release를
담는다.

Priority는 `P0`(즉시) · `P1`(높음) · `P2`(권장) · `P3`(낮음) · `Later`(현재 범위 외)로 나눈다.

Target Release는 특정 버전을 강제하지 않는다. Current Sprint, Next Release, Hotfix, Later,
TBD 중에서 고르거나 프로젝트가 쓰는 이름을 그대로 쓴다.

### 3.16 Re-validation Plan

개선 후 동일한 Task와 기준으로 다시 검증할 수 있도록 비교 항목을 정한다. Task 성공 여부, 완료
시간, 오류 횟수, 도움 필요 여부, 혼란 지점, Heuristic 결과, Accessibility Issue, 기존 Issue
해결 여부가 대상이다.

개선했다는 사실만으로 문제가 해결된 것으로 간주하지 않는다.

---

## 4. 최종 산출물 구성

다음 순서로 작성한다.

1. Executive Summary — 전체 UX 상태와 가장 중요한 발견
2. Service Overview
3. Personas
4. Tasks
5. Key Findings
6. Detailed Issues
7. Heuristic Evaluation
8. Accessibility Findings
9. Edge Cases
10. Improvement Backlog
11. Validation Required — 사용자 테스트가 필요한 가설
12. Re-validation Plan

Detailed Issues는 심각도순으로 늘어놓지 않고 사용자가 실제로 겪는 순서, 즉 Task 흐름 순으로
배열한다. 심각도는 Key Findings와 Backlog에서 다룬다.

---

## 5. 불변 규칙

1. 관찰된 사실과 추론을 명확히 구분한다.
2. 실제 사용자 행동이나 감정을 임의로 단정하지 않는다.
3. AI가 만든 Persona를 실제 사용자 조사 결과로 취급하지 않는다.
4. 확인할 수 없는 사항은 Assumption 또는 Hypothesis로 표시한다.
5. 실제로 수행하지 않은 테스트를 수행했다고 기록하지 않는다.
6. 사용성 문제와 개인적인 디자인 취향을 구분한다.
7. 문제를 발견해도 즉시 코드를 수정하지 않는다.
8. 먼저 기록하고 우선순위를 정한다.
9. Severity와 Confidence를 별도로 평가한다.
10. 기존 기능이 정상 작동한다면 코드나 디자인 취향만을 이유로 변경하지 않는다.
11. 개선안은 정답이 아니라 검증해야 할 가설이다.
12. 특정 버전에 종속되지 않는다.
13. 최종 목적은 문제 목록이 아니라 검증 가능한 Improvement Backlog다.
14. 사용자 검증이 필요한 문제는 별도로 표시한다.
15. Audit이 끝나기 전에는 서비스 코드를 수정하지 않는다.
