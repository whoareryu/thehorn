# 기획서 조항 ↔ 사이트 대조표

- 기준: `jekyll/_specs/plan.md` 기획서 확정본 v5.2 · `eval-spec.md` Evaluation PART 1 v2.2 · `visual.md` Visual Guide v1.1
- 갱신: 2026-09-11 (사이트 골격 + 목업 17 + 12장)
- 상태: ● 설명 + 목업 / ○ 설명만 / ✗ 없음
- 검사 칸의 `check:N` 은 `scripts/check_site.py` 의 N 번째 검사다(1 게임명 · 2 뿔피리 개수 · 3 MOCK 배지 · 4 NOT RUN · 5 relative_url · 6 링크 해소 · 7 v4 경고).

## 기획서 v5.2

| 조항 | 사이트 위치 | 데이터 | 검사 | 상태 |
|---|---|---|---|---|
| §0 출발 질문 · 연구 질문 | `/#why` | — | — | ○ |
| §1.1 유저는 조종하지 않는다 | `/#hands` | — | — | ○ |
| §1.2 자유도는 AI, 법칙은 Rule Engine | `/#hands` · 인스펙터 OUTCOME | — | — | ● |
| §1.3 CLASS ≠ BUILD | `/#birth` | `classes.yml` | — | ● |
| §1.4 · §9 무기 공격력 동일 | `/#birth` 무기표 | `classes.yml` | — | ○ |
| §1.5 · §35 같은 방법을 벌한다 | `/#boss` · `mock/fingerprint` | `missions.yml` stage | — | ● |
| §2 생성 순서 ①~⑧ | `mock/creation` | `mock_roster.yml` F | check:3 | ● |
| §3 Physical · §4 Age | `/#birth` | — | — | ○ |
| §5 MBTI 8축 | `/#birth` · 평가 ④ | `mbti.yml` | — | ● |
| §6 Gender 영향 0 | `/#birth` · 현황 guards | `status.yml` | — | ○ |
| §7 · 통합시나리오 §0 작가 · 배우 · 감독 | `/#hands` | — | — | ○ |
| §8 클래스 5종 · 무기 풀 | `/#birth` | `classes.yml` | — | ● |
| §11 · §12 20 Mission · 출전 인원 | `mock/campaign` · `/#campaign` | `missions.yml` | — | ● |
| §13 Troll Guard M1 · M2 | `mock/mission` · `mock/party` · `/#campaign` | `missions.yml` guard | — | ● |
| §14 초반 사망 완충 | `/#campaign` | — | — | ○ |
| §15 Taken 즉시 결정 | `mock/taken` | — | — | ● |
| §16 구조비 배율 · 시작 Gold | `/#after` 표 · `mock/hq` | — | — | ● |
| §17 · §18 보상 · MVP · Growth 지급 | `mock/result` · `/#after` 표 | — | — | ● |
| §19~§23 Camp 5턴 · 순응/거부 · 효과 | `mock/camp` · `mock/camp-result` · `/#camp` | `missions.yml` camp · `mock_roster.yml` rest | check:3 | ● |
| §24~§30 +5년 · Life Event · Rookie/Veteran | `mock/years` · `/#years` | — | — | ● |
| §31 Fatigue 로테이션 | `mock/party` 캡션 | — | — | ● |
| §32 · §33 단장 · 단원 역할 | `/#hands` · `/#battle` | — | — | ○ |
| §34 뿔피리 — Resource 아님 · Bard 지연 | `mock/battle` · `mock/hq` · `/#battle` | — | check:2 | ● |
| §36 Boss 학습 구현(코드 → LLM) | `/#boss` | — | — | ○ |
| §38 Growth History | `mock/detail` HISTORY | — | — | ● |
| §39 · §51 인스펙터 | `mock/inspector` | — | — | ● |
| §40 트레이스 이벤트 | `mock/inspector` 원본 트레이스 | — | — | ○ |
| §41 E1~E4 | `/#eval` · `/#status` | `eval.yml` · `status.yml` | check:4 · check:7 | ● |
| §42 대회 스코프 A/B/C | `/#scope` | — | — | ○ |
| §43 아키텍처 원칙 | `/#scope` | — | — | ○ |
| §44 제거되는 설계 | `/#status` 격차표 (v4 로만 언급) | `status.yml` gap | check:7 | ○ |
| §46 외부 설명 문구 · 상용 게임명 금지 | 푸터 · 전역 | — | check:1 | ● |
| §47 Screen Flow | `/screens/` 순서 | `screens.yml` | check:6 | ● |
| §48 · §49 Base 10 · Combat Variant 30 | `mock/detail` · `/#birth` (합계는 `classes.yml` 에서 계산) | `classes.yml` variants | — | ● |
| §50 전투 화면 2-depth | `mock/battle` | — | — | ● |
| §52 P0 Asset 130~150 | `/#scope` 표 | — | — | ○ |
| §53 Evaluation Dashboard | `mock/evaluation` · `/#eval` | `eval.yml` | check:4 | ● |
| §54 UI 와 AI 의 경계 | `/#battle` | — | — | ○ |

## Evaluation PART 1 v2.2

| 조항 | 사이트 위치 | 데이터 | 검사 | 상태 |
|---|---|---|---|---|
| §2 E4 고정 · 변경 | `/#eval` 리드 | — | — | ○ |
| §3 RQ1~RQ6 | `/#eval` | `eval.yml` | — | ○ |
| §4 Evaluation State | 대시보드 헤더 STATE | `eval.yml` state | — | ● |
| §5 Anchor 는 정답이 아니다 · §30 비열등성 | `/#eval` | — | — | ○ |
| §7 Funnel | `/#eval` | `eval.yml` funnel | — | ○ |
| §28 · §29 Gate (초기안) | `/#eval` 표 | `eval.yml` | — | ○ |
| §33 Failure Taxonomy | `/#eval` | `eval.yml` failures | — | ○ |
| §39 결과 문장 형식 | `/#eval` | `eval.yml` claims | — | ○ |
| §42 · §43.8 NOT RUN · Mock 표시 | `mock/evaluation` | `eval.yml` | check:4 · check:3 | ● |
| §43.7 Failure Drill-down | 대시보드 ⑥ | `eval.yml` drill | — | ● |
| §46 인스펙터 출력 순서 | `mock/inspector` | — | — | ● |

## Visual Guide v1.1

| 조항 | 사이트 위치 | 검사 | 상태 |
|---|---|---|---|
| §1.2 Art Direction · 금지 목록 | `assets/css/site.css` 팔레트 | — | ● |
| §15 P0 Screen 16 | `/screens/` | check:6 | ● |
| §16 HQ Resource 셋 | `mock/hq` | check:2 | ● |
| §17 Roster 최소 정보 | `mock/roster` | — | ● |
| §22 Floating Decision Tag | `mock/battle` | — | ● |
| §26 RETREAT SIGNAL | `mock/battle` | — | ● |
| §29.3 색에만 의존하지 않는다 | NOT RUN 빗금 + 글자, ✓/! | — | ● |
| §35 외부 발표 표현 | 푸터 | check:1 | ● |
| §36 성공 기준 3초 · 30초 · 3분 | 표지 · `/screens/` · `/#eval` | — | ○ |

## 아직 없는 것 (✗)

없음. ○ 는 목업 없이 글로만 설명한 조항이다 — 사이트의 목적(핵심 화면을 보여준다)상 목업이 필요한 것은 §46~§53 이고 전부 ● 다.
