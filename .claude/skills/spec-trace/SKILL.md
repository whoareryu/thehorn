---
name: spec-trace
description: 기획 원문 v5.2 조항 ↔ 사이트 절·목업 ↔ 검사(check_site.py) 대응표(docs/spec-trace.md)를 갱신하고 누락을 찾는 절차. "기획서 대조", "조항 추적", 마일스톤 종료 시 사용.
---

# 기획서 조항 추적

기획 원문(`jekyll/_specs/plan.md` 기획서 확정본 v5.2 를 중심으로, 평가는 `eval-spec.md`, 비주얼은 `visual.md`)의 각 조항이 사이트 어디에서 설명되고 무엇이 그것을 지키는지를 `docs/spec-trace.md` 한 표로 유지한다.

## 절차
1. 표의 각 행: `조항 | 사이트 위치(절 id · 목업 부품) | 데이터(_data) | 검사 | 상태(● 설명+목업 / ○ 설명만 / ✗ 없음)`.
2. 새 마일스톤이 끝나면 변경된 파일을 grep 해 대응 행을 갱신한다.
3. 기획서 §46~§53 (Visual/UI 제품 방향·Screen Flow·Evaluation Dashboard) 의 `✗` 가 다음 작업이다 — 사이트의 목적이 그 화면을 보여주는 것이기 때문이다.
4. 사이트 문장이 원문 수치를 옮길 때는 `_data` 를 거쳤는지 확인한다. 리터럴로 적힌 수치는 `_data` 로 옮긴다.
5. 새로 굳힐 규칙(원문의 "하지 않는다")이 생기면 `scripts/check_site.py` 에 검사를 추가하고 표의 검사 칸에 적는다.
