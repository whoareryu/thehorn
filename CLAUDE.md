# CLAUDE.md

Behavioral guidelines to reduce common LLM coding mistakes. Merge with project-specific instructions as needed.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---

**These guidelines are working if:** fewer unnecessary changes in diffs, fewer rewrites due to overcomplication, and clarifying questions come before implementation rather than after mistakes.

## [Shared] Part II — GoF Design Patterns

### 5. GoF Patterns (Gang of Four)

**`if/else` = the caller knows the branching → caller must change when behavior changes.**
**GoF pattern = the object knows its own branching → OCP achieved naturally.**

Telling AI "use Strategy here" compresses 10 lines of `if/elif/else` intent into one word.
Prefer `@abstractmethod` and polymorphism over any conditional that dispatches on type or state.

### Conditional → Pattern Mapping

| Bad code (conditional) | GoF Pattern | Category |
|---|---|---|
| `if type == "A": ... elif type == "B":` | **Strategy** | Behavioral |
| `if state == "PENDING": ... elif state == "PAID":` | **State** | Behavioral |
| `if format == "JSON": ... elif format == "XML":` | **Factory / Abstract Factory** | Creational |
| `if a: do_a(); if b: do_b();` | **Chain of Responsibility** | Behavioral |
| `if event == "click": ... elif event == "hover":` | **Observer / Command** | Behavioral |
| `for item in list: item.do()` | **Iterator + Visitor** | Behavioral |
| `obj = ClassA() if x else ClassB()` | **Factory Method** | Creational |
| `if cache: return cache; else: fetch()` | **Proxy** | Structural |
| `obj.a(); obj.b(); obj.c();` fixed order | **Template Method** | Behavioral |
| `if A and B and C: do()` complex condition | **Specification** | Behavioral |
| `result = step1(step2(step3(x)))` nested calls | **Decorator** | Structural |
| `global_var = None; if not global_var: init()` | **Singleton** | Creational |
| `try: ... except TypeA: ... except TypeB:` | **Command + Handler** | Behavioral |
| `if legacy_api: adapt(); else: use_new()` | **Adapter** | Structural |
| `obj1.notify(obj2); obj1.notify(obj3);` manual propagation | **Observer** | Behavioral |
| `if flag: do_extra()` feature toggle | **Decorator** | Structural |
| `if subsystem_a: ...; if subsystem_b: ...` | **Facade** | Structural |
| `copy = deepcopy(obj)` manual copy | **Prototype** | Creational |
| `for`-loop directly traversing a tree | **Composite + Iterator** | Structural + Behavioral |
| `if obj_type == "remote": ... elif "local":` | **Bridge** | Structural |

### GoF 23 Pattern Reference

```
Creational (5)
├── Singleton       ← global variable + if None check
├── Factory Method  ← if/else object creation
├── Abstract Factory← platform-specific if/else
├── Builder         ← telescoping constructor (too many __init__ args)
└── Prototype       ← manual deepcopy

Structural (7)
├── Adapter         ← if legacy / new API
├── Bridge          ← if remote / local
├── Composite       ← tree traversed directly with for
├── Decorator       ← nested function calls, flag-toggled features
├── Facade          ← complex subsystem if-chain
├── Flyweight       ← repeated object creation for identical data
└── Proxy           ← if cache / if auth / if lazy-load

Behavioral (11)
├── Chain of Responsibility ← if a: do_a; if b: do_b
├── Command         ← direct method call with no undo/queue
├── Iterator        ← direct for-loop over internals
├── Mediator        ← objects holding direct references to each other
├── Memento         ← state saved manually in dict/list
├── Observer        ← manual notify calls listed in sequence
├── State           ← if state == "X": elif state == "Y":
├── Strategy        ← if type == "A": elif type == "B":
├── Template Method ← fixed-order procedural calls
├── Visitor         ← for + if isinstance() dispatch
└── Interpreter     ← string parsing with if/elif chains
```

**Rules:**
- Replace any `if/elif` that dispatches on **type or state** with Strategy or State.
- Replace any object creation `if/else` with Factory Method or Abstract Factory.
- Replace any `for + if isinstance()` with Visitor.
- Use `@abstractmethod` to enforce contracts. Never check `isinstance` in business logic.
- When AI is asked to implement branching logic, default to the pattern — not the conditional.

---

## 이 프로젝트의 규칙

이 저장소는 **「자유중대 (Free Company)」의 프로젝트 사이트**(Jekyll)다. 코드네임 `thehorn` — 전장에서 유저가 직접 개입할 수 있는 유일한 수단인 뿔피리에서 따왔다.
게임 본체(`~/Documents/RPG`)와 저장소를 나눈다. 여기에는 백엔드도 프론트 앱도 없다 — **기획 v5.2 를 읽히고, 핵심 P0 화면을 목업으로 보여주는 사이트**다.

「자유중대」는 AI 캐릭터가 주어진 신체·성격·초기 방향 안에서 스스로 성장하고 판단하는 과정을 게임이라는 재현 가능한 환경에서 평가하는 **Agent Testbed** 다(Wanted AI Championship 2026 출품).
유저는 캐릭터를 조종하지 않는다. 출발점과 환경을 만들 뿐이다. 그리고 우리는 **그 자율성을 유지하는 가장 작은 모델**을 찾는다.

Part I·II 는 범용 지침이다. 충돌하면 **이 절과 기획서가 이긴다**.

### 문서 위치

| 무엇 | 어디 |
|---|---|
| 기획 원문 6편 (최종 권위) | `jekyll/_specs/` — 원문 본문은 바이트 단위로 손대지 않는다. 앞에 붙은 front matter 만 사이트용이다 |
| 사이트 설계 | `docs/superpowers/specs/` |
| 구현 계획 | `docs/superpowers/plans/` |
| 기획서 조항 ↔ 사이트 절·목업 ↔ 검사 대응표 | `docs/spec-trace.md` |
| 페르소나 QA 발견 | `docs/qa/` |
| 개발 일지 | `jekyll/_logs/` — 커밋 훅이 쓰고, `/log/` 가 렌더링한다 |

원문의 권위 순서: **기획서 확정본 v5.2 > Evaluation PART 1 > Visual Guide v1.1 > 통합시나리오 v3.2 > 쉬운설명·ELI5**. 사이트 문장이 원문과 다르면 사이트가 틀린 것이다.

### 저장소 파일 구조

```
thehorn/
├── CLAUDE.md                이 파일
├── README.md
├── .claude/
│   ├── settings.json        커밋 → 개발 일지 훅
│   ├── agents/              페르소나 QA 5인 (qa-judge·qa-voter·qa-canon·qa-teammate·qa-frontend)
│   └── skills/              qa-personas · spec-trace
├── scripts/
│   ├── check_site.py        사이트판 경계 테스트 — 기획서의 약속을 빌드 산출물에서 검사한다
│   └── commit_to_devlog.py  커밋 하나 → 개발 일지 한 편
├── docs/                    설계 · 계획 · spec-trace · qa
├── .github/workflows/       ci.yml(빌드+검사) · pages.yml(배포 — 원격이 생기면)
└── jekyll/                  사이트 소스. 테마 없음
    ├── _config.yml
    ├── _layouts/            base(밤 표지 + 장부) · doc(문서 본문)
    ├── _includes/           icons(SVG 문장) · mock/(P0 화면 목업 부품)
    ├── _data/               미션·클래스·MBTI·평가·구현현황 — 사이트 수치의 단일 출처
    ├── _specs/              기획 원문 6편 (컬렉션)
    ├── _logs/               개발 일지 (컬렉션, 개별 페이지 없음)
    ├── assets/css/site.css
    └── index.html · screens.html · docs.html · log.html · 404.html
```

### 사이트가 굳힌 규칙

이 여섯은 의견이 아니라 `scripts/check_site.py` 다. 바꾸려면 기획서를 먼저 바꾼다.

| 규칙 | 근거 | 강제 방식 |
|---|---|---|
| **특정 상용 게임명을 쓰지 않는다** | Visual Guide §35, 기획서 §46 | 빌드 산출물(원문 페이지 제외)에 금지어가 없다 |
| **실험하지 않은 값은 채우지 않는다** | Eval PART 1 §42·§43.8, Visual Guide §29.8 | 평가 대시보드 목업의 결과 셀은 `NOT RUN` 뿐이다. `_data/eval.yml` 에 숫자 결과 필드가 없다 |
| **목업 인물은 예시임을 밝힌다** | Visual Guide §29.8 (`MOCK` 배지) | `mock-frame` 마다 `MOCK` 배지가 있다 |
| **뿔피리는 Resource 가 아니다** | 기획서 §34, Visual Guide §16·§26 | `Horn remaining` · `Horn ×` 표기가 없다 |
| **모든 내부 링크는 `relative_url` 을 거친다** | 배포 baseurl(`/thehorn`) | 산출물에 `href="/…"` 원시 경로가 없고, 내부 링크가 전부 `_site` 안에서 풀린다 |
| **구현 현황은 v4 기준임을 밝힌다** | 오해 방지 — 코드는 v4(에르덴), 사이트는 v5.2 | 현황 절에 `v4` 기준 경고 문구가 있다 |

### 수치 단일 출처

미션별 출전 인원·Camp 시점·클래스 무기 풀·MBTI 8축·평가 게이트·구현 현황 수치는 **`jekyll/_data/*.yml`** 에 있다.
HTML 에 리터럴로 다시 쓰지 않고 Liquid 로 읽는다. 원문 수치를 바꿀 일이 생기면 원문 → `_data` 순서로 고친다.
구현 현황 수치(테스트 수·커밋 수)는 **RPG 저장소에서 실제로 돌려 본 값**만 쓴다 — 측정일을 `_data/status.yml` 에 함께 적는다.

### 비주얼 규약

Visual Guide §1.2 를 사이트에도 적용한다 — Medieval Low Fantasy, 1360년대 자유중대, 철·가죽·천·목재·양피지, 흐린 자연광·횃불.
**금지: 네온 · 과도한 마법광 · 과장 갑옷 · 과금형 UI.**

- 표지·네비·목업 프레임은 **밤**(가죽·쇠·횃불 호박색), 본문은 **장부**(양피지·먹·밀랍 붉은색).
- 이미지 에셋은 쓰지 않는다. 클래스 문장·리벳·인장은 인라인 SVG(`_includes/icons.html`). 초상 자리에 가짜 그림을 넣지 않는다.
- 색에만 의존하지 않는다 — 히트맵·상태는 글자(PASS/FAIL/NOT RUN, ✓/!)를 병행한다(Visual Guide §29.3).
- 390px 폭에서 본문은 가로로 넘치지 않는다. 표·목업은 자기 컨테이너 안에서만 스크롤한다.

### 코드 규약

- 주석은 "무엇"이 아니라 **"왜"**. 기획서 조항 번호를 인용한다 (`(기획서 §34, Visual Guide §26)`).
- 커밋 메시지는 **한국어 평서형**(`~했다`). 제목 한 줄 + 본문에 이유.
- 도메인 용어는 고정한다 — **유저**(서기 겸 계약 관리자) · **단장**(Orchestrator) · **단원**(Character AI) · **작가**(Scenario Director) · **Rule Engine** · **인스펙터** · **트레이스**.
  원문이 영문 용어(Build·Camp·Taken·Fingerprint)를 쓰는 곳은 원문을 따른다. 용어가 흔들리면 읽는 사람이 흔들린다.

### 검증 명령

```bash
cd jekyll && bundle exec jekyll build && cd .. && python3 scripts/check_site.py
```

완료를 말하기 전에 실제로 돌리고 출력을 본다(§4). 화면은 `bundle exec jekyll serve` 로 띄워 눈으로 본다.

### 페르소나 QA

마일스톤이 끝날 때마다 `.claude/agents/qa-*.md` 다섯 페르소나로 리뷰를 돌린다 (`/qa-personas`).
발견은 `docs/qa/` 에 남기고, 고치고, 재검한다. **발견을 무시하고 넘어가지 않는다.**
