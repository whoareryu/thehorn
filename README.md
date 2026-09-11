# thehorn — 「자유중대 (Free Company)」 프로젝트 사이트

**캐릭터를 조종하지 않는다. 출발점과 환경을 만들 뿐이다.**
AI 캐릭터가 스스로 성장하고 판단하는 과정을 게임으로 기록하고, 그 자율성을 유지하는 **가장 작은 모델**을 찾는 Agent Testbed — 그 기획을 읽히고 핵심 화면을 보여주는 Jekyll 사이트다.

> Wanted AI Championship 2026 출품작 · 게임 본체는 [whoareryu/RPG-agnet](https://github.com/whoareryu/RPG-agnet)

코드네임 `thehorn` 은 뿔피리에서 따왔다 — 전장에서 유저가 누를 수 있는 유일한 버튼이다.

## 무엇이 있나

| 경로 | 내용 |
|---|---|
| `/` | 장부 — 표지 + 12장. 왜 존재하는가부터 검증 · 구현 현황까지 |
| `/screens/` | 한 판 따라가기 — P0 핵심 화면 16개 목업 (Screen Flow 순서) |
| `/docs/` | 문서 서가 — 기획 원문 6편 (본문 무수정) |
| `/log/` | 개발 로그 — 커밋 훅이 쌓는다 |

목업의 인물 · 수치는 전부 **MOCK** 이고, 평가 대시보드의 결과 칸은 실험 전이라 **NOT RUN** 이다.

## 돌려보기

```bash
cd jekyll
bundle install          # 처음 한 번
bundle exec jekyll serve   # http://localhost:4000
```

## 검증

```bash
cd jekyll && bundle exec jekyll build && cd .. && python3 scripts/check_site.py
cd jekyll && bundle exec jekyll build --baseurl /thehorn && cd .. && python3 scripts/check_site.py --baseurl /thehorn
```

`check_site.py` 가 원문의 "하지 않는다"를 산출물에서 검사한다 — 상용 게임명 금지, 뿔피리 개수 표기 금지, 목업마다 MOCK 배지, 평가 결과는 NOT RUN, 모든 내부 링크는 `relative_url`, 구현 현황은 v4 기준 명시.

## 하네스

작업 규칙은 [`CLAUDE.md`](CLAUDE.md). 페르소나 QA 5인(`.claude/agents/`) · 스킬(`qa-personas` · `spec-trace`) · 커밋 → 개발 로그 훅(`.claude/settings.json`). QA 기록은 [`docs/qa/`](docs/qa/), 조항 대응표는 [`docs/spec-trace.md`](docs/spec-trace.md).
