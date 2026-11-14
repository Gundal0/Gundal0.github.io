---
{"dg-publish":true,"permalink":"/ai-technique/skills/claude-skills/","title":"Claude Skills 완전 정복 — 개념부터 고급까지","tags":["claude/skills","ai/agent","tutorial"],"dg-note-properties":{"title":"Claude Skills 완전 정복 — 개념부터 고급까지","aliases":["Claude Skills 강좌","Agent Skills 튜토리얼"],"tags":["claude/skills","ai/agent","tutorial"],"level":"초급 → 중급 → 고급","audience":"개발자","created":"2026-10-18","status":"complete"}}
---


# Claude Skills 완전 정복 — 개념부터 고급까지

> [!abstract] 이 강좌로 얻는 것
> - Skill이 **무엇이고, 왜 존재하며, 내부에서 어떻게 로딩되는지** 정확히 이해한다.
> - Claude Code / claude.ai / Claude API / Agent SDK 에서 **직접 Skill을 만들고, 배포하고, 운영**한다.
> - 스크립트·검증 루프·서브에이전트·훅·플러그인·평가(Eval)까지 **고급 패턴**을 실전 예제로 익힌다.
> - 마지막 캡스톤 프로젝트를 끝내면 팀에서 "Skill은 저 사람한테 물어봐"라는 말을 듣는 수준이 된다.

> [!info] 기준 시점
> 이 문서는 **2026년 10월** 공식 문서 기준입니다. Skills는 빠르게 진화하는 기능이므로, 필드 이름이나 SDK 메서드가 다르면 [[AI technique/skills/Claude-Skills-완전정복-강좌#부록 C. 참고 자료\|공식 문서]]를 먼저 확인하세요.

---

## 목차

- [[AI technique/skills/Claude-Skills-완전정복-강좌#Part 0. 학습 로드맵\|#Part 0. 학습 로드맵]]
- **초급**
  - [[AI technique/skills/Claude-Skills-완전정복-강좌#Part 1. 개념 — Skill이란 무엇인가\|#Part 1. 개념 — Skill이란 무엇인가]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌#Part 2. 첫 번째 Skill 만들기 (Hello, Skill)\|#Part 2. 첫 번째 Skill 만들기 (Hello, Skill)]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌#Part 3. SKILL.md 해부학\|#Part 3. SKILL.md 해부학]]
- **중급**
  - [[AI technique/skills/Claude-Skills-완전정복-강좌#Part 4. 파일 번들링 — references, scripts, assets\|#Part 4. 파일 번들링 — references, scripts, assets]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌#Part 5. Claude Code 전용 기능 — 인자, 동적 컨텍스트, 권한, 호출 제어\|#Part 5. Claude Code 전용 기능 — 인자, 동적 컨텍스트, 권한, 호출 제어]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌#Part 6. 실전 예제 3종\|#Part 6. 실전 예제 3종]]
- **고급**
  - [[AI technique/skills/Claude-Skills-완전정복-강좌#Part 7. 고급 패턴 — 워크플로·검증 루프·자유도 설계\|#Part 7. 고급 패턴 — 워크플로·검증 루프·자유도 설계]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌#Part 8. 서브에이전트, 훅, 경로 기반 활성화\|#Part 8. 서브에이전트, 훅, 경로 기반 활성화]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌#Part 9. Claude API & Agent SDK에서 Skills 쓰기\|#Part 9. Claude API & Agent SDK에서 Skills 쓰기]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌#Part 10. 배포 — 팀 공유와 플러그인\|#Part 10. 배포 — 팀 공유와 플러그인]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌#Part 11. 평가 주도 개발 (Eval-Driven Skill Development)\|#Part 11. 평가 주도 개발 (Eval-Driven Skill Development)]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌#Part 12. 보안, 성능, 운영\|#Part 12. 보안, 성능, 운영]]
- **마무리**
  - [[AI technique/skills/Claude-Skills-완전정복-강좌#Part 13. 캡스톤 프로젝트 — 카메라 로그 분석 Skill\|#Part 13. 캡스톤 프로젝트 — 카메라 로그 분석 Skill]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌#Part 14. 트러블슈팅\|#Part 14. 트러블슈팅]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌#부록 A. 연습문제와 해답\|#부록 A. 연습문제와 해답]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌#부록 B. 치트시트\|#부록 B. 치트시트]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌#부록 C. 참고 자료\|#부록 C. 참고 자료]]

---

## Part 0. 학습 로드맵

```mermaid
flowchart LR
    A[개념 이해<br/>Part 1] --> B[첫 Skill<br/>Part 2]
    B --> C[SKILL.md 해부<br/>Part 3]
    C --> D[파일 번들링<br/>Part 4]
    D --> E[Claude Code 기능<br/>Part 5]
    E --> F[실전 예제<br/>Part 6]
    F --> G[고급 패턴<br/>Part 7~8]
    G --> H[API / SDK<br/>Part 9]
    H --> I[배포 / Eval / 보안<br/>Part 10~12]
    I --> J((캡스톤<br/>Part 13))
```

| 단계 | 목표 | 예상 소요 |
|---|---|---|
| 초급 (Part 1~3) | 개념 이해 + 첫 Skill 동작 확인 | 1~2시간 |
| 중급 (Part 4~6) | 스크립트/참조 파일이 있는 실무형 Skill 작성 | 3~4시간 |
| 고급 (Part 7~12) | 검증 루프, 서브에이전트, API 배포, Eval, 보안 | 4~6시간 |
| 캡스톤 (Part 13) | 처음부터 끝까지 하나의 프로덕션급 Skill 완성 | 2~3시간 |

> [!tip] 실습 환경 준비
> - **Claude Code** 설치 (`npm install -g @anthropic-ai/claude-code` 또는 공식 설치 스크립트) — 이 강좌의 주 실습 환경
> - Python 3.10+ (스크립트 예제용)
> - (선택) Anthropic API 키 — Part 9 실습용
> - (선택) claude.ai Pro/Max/Team/Enterprise 계정 — Code execution 기능 활성화 필요

---

# 🟢 초급

## Part 1. 개념 — Skill이란 무엇인가

### 1.1 한 문장 정의

> [!quote] 정의
> **Skill = Claude가 필요할 때 스스로 꺼내 쓰는 "업무 매뉴얼 폴더"**
> `SKILL.md`(지침) + 선택적 부가 파일(스크립트, 참조 문서, 템플릿)로 구성된 **디렉터리**이며, Claude는 작업과 관련 있을 때만 이를 로드합니다.

개발자 비유로 말하면:

| 개발 개념 | Skill에서의 대응 |
|---|---|
| 라이브러리의 `README` + `docs/` | `SKILL.md` + `references/` |
| CLI 유틸리티 (`bin/`) | `scripts/` |
| 패키지 메타데이터 (`package.json`의 name/description) | YAML frontmatter |
| Lazy loading / 동적 import | Progressive Disclosure (점진적 공개) |
| 플러그인 시스템 | Skills를 묶어 배포하는 Plugin |

### 1.2 왜 필요한가 — 프롬프트의 한계

매번 이런 프롬프트를 붙여 넣은 경험이 있을 겁니다.

```text
우리 팀 커밋 컨벤션은 Conventional Commits이고, scope는 모듈명,
본문은 72자 줄바꿈, 이슈 번호는 footer에 "Refs: VMS-123" 형식으로…
```

이 방식의 문제점:

1. **반복** — 대화마다 복붙
2. **컨텍스트 낭비** — 관련 없는 대화에서도 항상 토큰을 차지 (CLAUDE.md에 다 넣는 경우)
3. **결정론 부족** — 정확해야 하는 로직(파싱, 검증)도 LLM이 매번 "추론"
4. **공유 어려움** — 팀원마다 다른 버전의 프롬프트

Skill은 이 네 가지를 동시에 해결합니다: **한 번 작성 → 필요할 때만 로드 → 결정론적 작업은 스크립트로 → 폴더째 공유**.

### 1.3 핵심 원리: Progressive Disclosure (점진적 공개)

Skill의 가장 중요한 설계 개념입니다. ==이것 하나만 확실히 이해하면 Skill 설계의 80%가 해결됩니다.==

```mermaid
flowchart TB
    subgraph L1["Level 1 — 메타데이터 (항상 로드, Skill당 ~100 토큰)"]
        M["name + description"]
    end
    subgraph L2["Level 2 — 지침 (트리거될 때 로드, 권장 5k 토큰 이하)"]
        B["SKILL.md 본문"]
    end
    subgraph L3["Level 3+ — 리소스 (필요할 때만)"]
        R["references/*.md<br/>(읽을 때 로드)"]
        S["scripts/*.py<br/>(실행 결과만 컨텍스트에 들어옴)"]
        A["assets/*<br/>(템플릿, 이미지 등)"]
    end
    U[사용자 요청] --> M
    M -- "관련 있다고 판단" --> B
    B -- "필요 시 Read" --> R
    B -- "필요 시 Bash 실행" --> S
    B -- "필요 시 복사/사용" --> A
```

| 레벨 | 언제 로드? | 토큰 비용 | 내용 |
|---|---|---|---|
| **1. 메타데이터** | 항상 (시작 시) | Skill당 약 100 토큰 | `name`, `description` |
| **2. 지침** | Skill이 트리거될 때 | 5k 토큰 이하 권장 | `SKILL.md` 본문 |
| **3+. 리소스** | 필요할 때 | 접근 전까지 0 | 참조 파일(읽을 때), 스크립트(**출력만** 들어옴) |

> [!important] 핵심 통찰
> - Skill을 **100개 설치해도** 평소 비용은 메타데이터 약 10k 토큰 수준입니다.
> - 스크립트는 **소스 코드가 컨텍스트에 들어가지 않고 실행 결과만** 들어옵니다. 1,000줄짜리 파서도 결과 10줄이면 10줄 비용.
> - 따라서 `description`은 "**언제 이 Skill을 꺼낼지**" 판단하는 유일한 근거입니다. ([[AI technique/skills/Claude-Skills-완전정복-강좌#3.3 description 작성법 — 가장 중요한 한 줄\|Part 3.3]]에서 자세히)

### 1.4 Skill은 어떻게 실행되는가 (내부 동작)

Skill은 마법이 아니라 **파일시스템 + 도구 호출**입니다.

```mermaid
sequenceDiagram
    participant U as 사용자
    participant C as Claude
    participant FS as 파일시스템 / Bash
    Note over C: 시스템 프롬프트에 모든 Skill의<br/>name + description 목록이 있음
    U->>C: "이 PDF에서 표 추출해줘"
    C->>C: description 매칭 → pdf skill 관련
    C->>FS: Read skills/pdf/SKILL.md
    FS-->>C: 지침 본문
    C->>FS: bash: python scripts/extract_tables.py input.pdf
    FS-->>C: 결과(JSON) — 스크립트 소스는 안 들어옴
    C->>U: 정리된 표
```

즉 Skill이 동작하려면 **파일 읽기 + 코드 실행 환경**이 필요합니다. 그래서 Claude API에서는 Code Execution 도구가 필수이고, claude.ai에서는 Code execution 설정이 켜져 있어야 합니다.

### 1.5 비슷한 기능과의 비교 (매우 중요)

초보자가 가장 헷갈리는 부분입니다.

| 기능 | 무엇인가 | 로딩 시점 | 언제 쓰나 |
|---|---|---|---|
| **프롬프트** | 대화 중 직접 입력 | 그때만 | 일회성 지시 |
| **CLAUDE.md** (Claude Code) | 프로젝트 메모리 | **항상** 로드 | 모든 작업에 적용되는 규칙 (빌드 명령, 코딩 스타일) |
| **Skill** | 지침+코드 폴더 | **관련 있을 때만** | 특정 작업 절차·도메인 지식·도구 |
| **Slash command** (`.claude/commands/`) | 프롬프트 템플릿 | 사용자가 `/명령` 입력 시 | 단순 반복 프롬프트 (현재는 Skill로 통합 추세) |
| **MCP 서버** | 외부 시스템 연결 프로토콜 | 도구로 상시 노출 | DB, Slack, Jira 등 **외부 데이터/액션** 접근 |
| **Subagent** | 독립 컨텍스트의 하위 에이전트 | 위임 시 | 컨텍스트 분리가 필요한 큰 작업 |
| **Plugin** | Skill+명령+훅+MCP+에이전트 묶음 | 설치 시 | 팀/조직 배포 |

> [!tip] 기억법
> - **MCP = 손과 발** (외부 세계에 접근하는 능력)
> - **Skill = 노하우** (그 능력을 *어떻게* 잘 쓰는지에 대한 절차 지식)
> - **CLAUDE.md = 상식** (항상 알아야 하는 것)
> - **Subagent = 동료** (따로 일 시키기)
>
> 예: Jira MCP는 "이슈를 만들 수 있게" 해주고, `triaging-bugs` Skill은 "우리 팀 방식으로 버그를 분류하고 이슈를 만드는 법"을 알려줍니다.

### 1.6 Skill은 어디서 동작하는가

| 환경 | 기본 제공 Skill | 커스텀 Skill | 설치/등록 방법 | 공유 범위 |
|---|---|---|---|---|
| **claude.ai / Desktop** | ✅ (pptx, xlsx, docx, pdf) | ✅ | Settings > Features(Capabilities)에서 zip 업로드 | 개인 |
| **Claude Code** | ❌ (문서 Skill 미포함) | ✅ | `~/.claude/skills/`, `.claude/skills/` 폴더 | 개인 / 프로젝트(git) / 플러그인 |
| **Claude API** | ✅ | ✅ | `/v1/skills` 엔드포인트로 업로드, `container.skills`로 사용 | 워크스페이스 전체 |
| **Agent SDK** | — | ✅ | 파일시스템 Skill (`.claude/skills/`) 로드 | 프로젝트 |

> [!warning] 동기화되지 않습니다
> claude.ai, API, Claude Code의 커스텀 Skill은 **서로 동기화되지 않습니다**. 각 환경에 따로 설치/업로드해야 합니다. (그래서 git 저장소 하나를 "원본"으로 두고 각 환경에 배포하는 방식을 [[AI technique/skills/Claude-Skills-완전정복-강좌#Part 10. 배포 — 팀 공유와 플러그인\|Part 10]]에서 다룹니다.)

> [!note] 오픈 표준
> Agent Skills 포맷(`SKILL.md` + frontmatter)은 오픈 표준으로 공개되어 있어, Claude 외 다른 에이전트 도구들도 같은 폴더 구조를 읽을 수 있습니다. 즉 **한 번 잘 만든 Skill은 이식성이 높습니다.**

### 1.7 Part 1 요약

- [x] Skill = `SKILL.md`가 들어 있는 폴더
- [x] 평소엔 이름+설명만, 필요할 때 본문, 더 필요할 때 부가 파일 (Progressive Disclosure)
- [x] 스크립트는 출력만 컨텍스트에 들어온다
- [x] MCP는 능력, Skill은 노하우
- [x] 환경 간 동기화는 안 된다

---

## Part 2. 첫 번째 Skill 만들기 (Hello, Skill)

### 2.1 Claude Code에서 만들기 (권장)

**Step 1 — 폴더 만들기**

```bash
# 개인 Skill (모든 프로젝트에서 사용)
mkdir -p ~/.claude/skills/explaining-code

# 또는 프로젝트 Skill (이 저장소에서만, git으로 팀 공유)
mkdir -p .claude/skills/explaining-code
```

**Step 2 — `SKILL.md` 작성**

```markdown
---
name: explaining-code
description: Explains code with an ASCII diagram and a real-world analogy. Use when the user asks how code works, asks to explain a file or function, or says "이 코드 설명해줘".
---

# Explaining Code

코드를 설명할 때 항상 다음 순서를 따른다.

1. **한 줄 요약**: 이 코드가 하는 일을 한 문장으로.
2. **비유**: 일상생활의 비유 하나.
3. **ASCII 다이어그램**: 데이터/제어 흐름을 그린다.
4. **단계별 설명**: 핵심 로직을 순서대로.
5. **주의할 점**: 흔한 실수나 엣지 케이스 1~2개.

설명은 한국어로, 코드 식별자는 원문 그대로 둔다.
```

**Step 3 — 동작 확인**

```bash
cd 아무_프로젝트
claude
```

```text
> 사용 가능한 skill 목록 보여줘
> src/main.py 가 어떻게 동작하는지 설명해줘
```

Claude가 `explaining-code` Skill을 로드하는 것이 보이고, 답변이 비유 → 다이어그램 → 단계별 설명 형식으로 나오면 성공입니다.

**Step 4 — 직접 호출해 보기**

```text
> /explaining-code src/main.py
```

Claude Code에서 Skill은 자동 호출뿐 아니라 `/skill-name`으로 **직접 호출**도 됩니다.

> [!success] 축하합니다
> 첫 Skill을 만들었습니다. 정리하면 Skill의 최소 요건은 단 두 가지입니다.
> 1. 폴더 안의 `SKILL.md`
> 2. frontmatter의 `name`, `description`

### 2.2 claude.ai(웹/데스크톱)에서 사용하기

1. **Settings → Capabilities(또는 Features)** 에서 **Code execution** 활성화
2. 위의 `explaining-code` 폴더를 **폴더째 zip으로 압축** (zip 안에 `explaining-code/SKILL.md` 구조)
3. Skills 섹션에서 **Upload skill** → zip 선택
4. 새 대화에서 "이 코드 설명해줘" + 코드 붙여넣기

```bash
cd ~/.claude/skills
zip -r explaining-code.zip explaining-code/
```

> [!tip] claude.ai에서 Skill 만들기의 지름길
> claude.ai에는 **skill-creator** 라는 기본 Skill이 있습니다. "회의록을 우리 팀 템플릿으로 정리하는 Skill을 만들어줘"라고 대화하면 인터뷰 → 초안 → 테스트까지 도와줍니다. 처음엔 이걸로 초안을 만들고, 이 강좌의 원칙으로 다듬는 것을 추천합니다.

### 2.3 디렉터리 구조 한눈에 보기

```text
explaining-code/
└── SKILL.md            ← 필수 (이것만 있어도 Skill)

# 실무형 Skill은 보통 이렇게 성장합니다
processing-invoices/
├── SKILL.md            ← 개요 + 워크플로 (500줄 이하)
├── references/
│   ├── schema.md       ← 필요할 때만 읽는 상세 문서
│   └── edge-cases.md
├── scripts/
│   ├── parse.py        ← 실행만 하고 소스는 컨텍스트에 안 들어옴
│   └── validate.py
└── assets/
    └── template.xlsx   ← 출력에 쓰는 템플릿/리소스
```

> [!note] 폴더 이름 관례
> `references/`, `scripts/`, `assets/`는 **관례**이지 강제 사항이 아닙니다. 중요한 것은 `SKILL.md`에서 **상대 경로로 정확히 가리키는 것**입니다.

---

## Part 3. SKILL.md 해부학

### 3.1 전체 구조

````markdown
---                                  ← 반드시 파일의 첫 줄
name: reviewing-pull-requests        ← 메타데이터 (Level 1)
description: Reviews pull requests for ...
---

# Reviewing Pull Requests            ← 본문 (Level 2)

## Quick start
...

## Workflow
...

## References
- 보안 체크리스트: [references/security.md](references/security.md)   ← Level 3
````

### 3.2 공통 frontmatter 규칙 (모든 환경)

| 필드 | 필수 | 규칙 |
|---|---|---|
| `name` | API/claude.ai: 필수<br/>Claude Code: 선택(기본값=폴더명) | 최대 **64자**, **소문자·숫자·하이픈만**, XML 태그 금지, 예약어 **"anthropic", "claude" 포함 금지** |
| `description` | 필수(권장) | 비어 있으면 안 됨, 최대 **1024자**, XML 태그 금지, **무엇을 하는지 + 언제 쓰는지** 둘 다 |

```yaml
# ✅ 좋은 예
name: processing-pdfs
name: analyzing-spreadsheets
name: writing-release-notes

# ❌ 나쁜 예
name: PDF_Helper        # 대문자, 언더스코어
name: claude-helper     # 예약어 포함
name: utils             # 너무 모호
```

> [!tip] 이름 짓기 관례
> 공식 권장은 **동명사(gerund) 형태**: `processing-pdfs`, `reviewing-code`, `writing-documentation`. 명사구(`pdf-processing`)도 허용되지만 **팀 내에서 일관성**을 유지하세요.

### 3.3 description 작성법 — 가장 중요한 한 줄

Claude는 수십~수백 개의 Skill 중에서 **오직 description만 보고** 어떤 Skill을 열지 결정합니다. Skill이 "안 먹힌다"는 문제의 대부분은 description 문제입니다.

**원칙 4가지**

1. **3인칭으로 쓴다** — description은 시스템 프롬프트에 삽입됩니다.
   - ✅ "Processes Excel files and generates reports."
   - ❌ "I can help you process Excel files." / "You can use this to…"
2. **무엇(What) + 언제(When)** 를 둘 다 쓴다.
3. **트리거 키워드**를 넣는다 — 사용자가 실제로 쓸 단어(파일 확장자, 도구 이름, 한국어 표현 포함).
4. **핵심 용도를 앞에** 둔다 — Claude Code에서는 목록에 표시될 때 긴 설명이 잘릴 수 있습니다.

**Before / After**

```yaml
# ❌ Before — 모호함. 언제 써야 할지 알 수 없음
description: Helps with documents.

# ✅ After — 무엇 + 언제 + 트리거 키워드
description: >-
  Extracts text and tables from PDF files, fills PDF forms, and merges
  documents. Use when working with .pdf files or when the user mentions
  PDFs, forms, document extraction, or "PDF에서 표 뽑아줘".
```

> [!example] 연습: 다음 description을 고쳐 보세요
> `description: 로그 분석 도구`
> > [!success]- 모범 답안 (클릭해서 펼치기)
> > ```yaml
> > description: >-
> >   Analyzes VMS server and IP camera log files (.log, .txt) to find
> >   errors, disconnections, and RTSP/ONVIF failures, then summarizes them
> >   by device and time. Use when the user shares camera or VMS logs, asks
> >   why a camera went offline, or says "로그 분석해줘".
> > ```

> [!warning] 과잉 트리거 vs 과소 트리거
> - 너무 넓으면(`Use for any coding task`) 엉뚱한 작업에서 로드되어 토큰 낭비 + 지침 충돌
> - 너무 좁으면(`Use only when the user types /pdf`) 필요할 때 안 열림
> - **경계 조건**을 적어 주면 좋습니다: "Do NOT use for Word documents."

### 3.4 본문(Body) 작성 원칙

**① 간결함 — Claude는 이미 똑똑하다**

Claude가 이미 아는 일반 지식은 쓰지 마세요. **당신 팀/도메인에만 있는 지식**만 쓰세요.

````markdown
<!-- ❌ 장황함 (~150 토큰) -->
PDF(Portable Document Format)는 Adobe가 개발한 파일 형식으로...
PDF에서 텍스트를 추출하려면 먼저 라이브러리를 설치해야 하는데...

<!-- ✅ 간결함 (~50 토큰) -->
## Extract text
```python
import pdfplumber
with pdfplumber.open("file.pdf") as pdf:
    text = pdf.pages[0].extract_text()
```
````

> [!question] 판단 기준
> 각 문장에 대해 자문하세요: "**Claude가 이 문장 없이도 이걸 알까?**" 알면 지우세요.

**② 구조 — 빠르게 훑을 수 있게**

권장 섹션 구성:

```markdown
# <Skill 제목>

## Quick start        ← 가장 흔한 케이스 하나를 바로 실행 가능하게
## Workflow           ← 단계별 절차 (체크리스트)
## Rules / Conventions← 반드시 지켜야 할 규칙
## Examples           ← 입력/출력 예시
## References         ← 상세 파일 링크 (Level 3)
```

**③ 하나의 기본값을 제시하라 (메뉴 X)**

```markdown
<!-- ❌ -->
pypdf, pdfplumber, PyMuPDF, pdf2image 중 아무거나 쓸 수 있다.

<!-- ✅ -->
텍스트 추출에는 pdfplumber를 쓴다.
스캔된 PDF(텍스트 레이어 없음)일 때만 pdf2image + pytesseract로 OCR한다.
```

**④ 용어 일관성** — "엔드포인트/URL/경로"를 섞어 쓰지 말고 하나로 통일.

**⑤ 시간 의존 정보 금지** — "2025년 8월 이전에는 v1 API를 써라" 같은 문장은 곧 틀립니다. 꼭 필요하면 접힌 "Legacy" 섹션으로.

### 3.5 Part 3 체크포인트

> [!check] 셀프 체크
> - [ ] `name`이 소문자-하이픈이고 예약어가 없다
> - [ ] `description`이 3인칭이고 What + When + 키워드를 포함한다
> - [ ] 본문에 Claude가 이미 아는 일반론이 없다
> - [ ] 기본 도구/방법을 하나로 정했다

---

# 🟡 중급

## Part 4. 파일 번들링 — references, scripts, assets

### 4.1 언제 파일을 분리하나

| 신호 | 조치 |
|---|---|
| `SKILL.md`가 **500줄**을 넘어간다 | 상세 내용을 `references/`로 분리 |
| 매번 같은 코드를 Claude가 새로 짠다 | `scripts/`로 고정 |
| 정확해야 하는 계산/파싱/검증이 있다 | `scripts/`로 고정 (결정론) |
| 출력 형식이 엄격하다 (보고서 양식 등) | `assets/`에 템플릿 |
| 도메인이 여러 개다 (재무/영업/제품) | 도메인별 reference 파일 |

### 4.2 references — 필요할 때만 읽히는 문서

````markdown
# BigQuery Analysis

## Quick start
매출 질문이면 [references/finance.md](references/finance.md)를 먼저 읽는다.
파이프라인 질문이면 [references/sales.md](references/sales.md)를 읽는다.
제품 사용량 질문이면 [references/product.md](references/product.md)를 읽는다.

## Common rules
- 테스트 계정(`is_test = true`)은 항상 제외한다.
- 날짜는 KST 기준 `DATE(created_at, "Asia/Seoul")`로 변환한다.
````

> [!important] 참조는 1단계 깊이만
> `SKILL.md → a.md → b.md → c.md` 처럼 **중첩 참조를 만들지 마세요.** Claude는 중첩된 파일을 `head -100` 같은 부분 읽기로 미리보기만 하고 넘어가는 경우가 있어 정보가 누락됩니다. **모든 reference는 `SKILL.md`에서 직접 링크**하세요.

> [!tip] 긴 reference 파일에는 목차를
> 100줄이 넘는 reference 파일은 맨 위에 목차를 두세요. 부분만 읽어도 전체 범위를 파악할 수 있습니다.

### 4.3 scripts — 결정론적 작업은 코드로

스크립트의 3대 이점:

1. **신뢰성** — 매번 같은 결과
2. **토큰 절약** — 소스가 컨텍스트에 들어가지 않음
3. **속도** — 생성 대신 실행

**`SKILL.md`에서 의도를 명확히:**

```markdown
<!-- 실행하라는 뜻 -->
`python scripts/analyze_form.py input.pdf` 를 **실행**해 필드 목록을 얻는다.

<!-- 읽으라는 뜻 -->
필드 매핑 알고리즘은 `scripts/analyze_form.py`를 **참고**한다.
```

**스크립트 작성 원칙**

````python
#!/usr/bin/env python3
"""Count error lines per device. Usage: python count_errors.py <logfile>"""
import sys
from collections import Counter

# 원칙 1: 에러를 Claude에게 떠넘기지 말고 스스로 처리 (Solve, don't punt)
if len(sys.argv) != 2:
    print("ERROR: usage: count_errors.py <logfile>", file=sys.stderr)
    sys.exit(2)

try:
    with open(sys.argv[1], encoding="utf-8", errors="replace") as f:
        lines = f.readlines()
except FileNotFoundError:
    # 원칙 2: 에러 메시지는 Claude가 다음 행동을 알 수 있게 구체적으로
    print(f"ERROR: file not found: {sys.argv[1]}. Ask the user for the correct path.")
    sys.exit(1)

# 원칙 3: 매직 넘버에는 이유를 주석으로 (No voodoo constants)
TOP_N = 10  # 요약에는 상위 10개 장비면 충분 (그 이상은 노이즈)

counts = Counter(l.split()[1] for l in lines if " ERROR " in l and len(l.split()) > 1)
# 원칙 4: 출력은 짧고 구조적으로 (이 출력만 컨텍스트에 들어간다)
for device, n in counts.most_common(TOP_N):
    print(f"{device}\t{n}")
````

> [!warning] 의존성 주의
> - **Claude API** 실행 환경: **네트워크 없음, 런타임 패키지 설치 불가** — 미리 설치된 패키지만 사용 가능
> - **claude.ai**: 관리자 설정에 따라 네트워크 가능 여부가 다름
> - **Claude Code**: 로컬 머신이므로 자유롭지만, 전역 설치보다 로컬(venv) 설치 권장
>
> → 필요한 패키지를 `SKILL.md`에 명시하고, 표준 라이브러리로 해결 가능하면 표준 라이브러리를 쓰세요.

> [!tip] 경로는 항상 슬래시(`/`)
> Windows에서도 `scripts/helper.py`처럼 쓰세요. `scripts\helper.py`는 Unix 계열 실행 환경에서 깨집니다.

### 4.4 assets — 출력용 리소스

```text
writing-weekly-report/
├── SKILL.md
└── assets/
    ├── report-template.md
    └── logo.png
```

```markdown
## Output
1. `assets/report-template.md`를 복사해 `weekly-report-YYYY-MM-DD.md`로 저장한다.
2. `{{SUMMARY}}`, `{{RISKS}}`, `{{NEXT_WEEK}}` 자리표시자를 채운다.
3. 템플릿의 섹션 순서와 제목은 바꾸지 않는다.
```

---

## Part 5. Claude Code 전용 기능 — 인자, 동적 컨텍스트, 권한, 호출 제어

> [!info] 여기부터는 Claude Code 전용
> 아래 frontmatter 필드 대부분은 **Claude Code에서만** 의미가 있습니다. claude.ai/API는 `name`, `description` 위주로 읽고 나머지는 무시합니다. (Claude Code도 모르는 필드는 **오류 없이 무시**하므로 오타에 주의!)

### 5.1 Claude Code frontmatter 전체 레퍼런스

| 필드 | 용도 | 예시 |
|---|---|---|
| `name` | 명령 이름 (기본값=폴더명) | `fix-issue` |
| `description` | 무엇/언제 | — |
| `when_to_use` | 추가 트리거 문구 (description 뒤에 붙음) | `"버그 고쳐줘", "이슈 처리"` |
| `argument-hint` | 자동완성 힌트 | `[issue-number]` |
| `arguments` | 이름 있는 위치 인자 → `$name` 치환 | `[env, version]` |
| `disable-model-invocation` | `true`면 Claude가 **자동으로는** 안 씀 (사용자만 `/` 호출) | 배포처럼 부작용 있는 작업 |
| `user-invocable` | `false`면 `/` 메뉴에서 숨김 (Claude만 사용) | 배경 지식형 Skill |
| `allowed-tools` | 이 턴에서 **승인 없이** 쓸 수 있는 도구 | `Bash(git add *) Bash(git commit *)` |
| `disallowed-tools` | Skill 활성 중 도구 제거 | `Write Edit` |
| `model` | 이번 턴에 쓸 모델 | — |
| `effort` | 추론 노력 수준 | `low` ~ `max` |
| `context` | `fork`면 서브에이전트에서 실행 | `fork` |
| `agent` | fork 시 서브에이전트 종류 | `Explore` |
| `background` | fork 시 `false`면 결과를 기다림 | `false` |
| `hooks` | Skill 호출 시 등록되는 훅 | [[AI technique/skills/Claude-Skills-완전정복-강좌#8.2 Skill 스코프 훅 (hooks)\|Part 8.2]] |
| `paths` | 이 glob에 맞는 파일 작업 시에만 자동 활성화 | `["**/*.proto"]` |
| `shell` | 주입 명령용 셸 | `bash` / `powershell` |

### 5.2 호출 제어 매트릭스

| 설정 | 사용자 `/name` | Claude 자동 호출 | 대표 용도 |
|---|---|---|---|
| (기본) | ✅ | ✅ | 대부분의 Skill |
| `disable-model-invocation: true` | ✅ | ❌ | `/deploy`, `/release` 등 **부작용 있는 작업** |
| `user-invocable: false` | ❌ | ✅ | 레거시 시스템 설명 같은 **배경 지식** |

> [!danger] 부작용이 있는 Skill은 반드시 `disable-model-invocation: true`
> 배포, DB 마이그레이션, 메시지 발송 같은 Skill을 자동 호출 가능하게 두면, Claude가 "도움이 되겠다"고 판단해 **의도치 않게 실행**할 수 있습니다.

### 5.3 인자 치환 ($ARGUMENTS)

| 변수 | 의미 |
|---|---|
| `$ARGUMENTS` | 입력한 인자 전체 |
| `$0`, `$1` … (`$ARGUMENTS[N]`) | 0부터 시작하는 위치 인자 |
| `$name` | `arguments`에 선언한 이름 인자 |
| `${CLAUDE_SKILL_DIR}` | `SKILL.md`가 있는 디렉터리 (**스크립트 경로에 필수!**) |
| `${CLAUDE_PROJECT_DIR}` | 프로젝트 루트 |
| `${CLAUDE_SESSION_ID}` | 현재 세션 ID |

**예제: 이슈 번호를 받는 Skill**

```markdown
---
name: fix-issue
description: Fixes a GitHub issue end-to-end following team conventions.
argument-hint: "[issue-number]"
disable-model-invocation: true
---

GitHub 이슈 #$ARGUMENTS 를 해결한다.

1. `gh issue view $ARGUMENTS` 로 내용을 확인한다.
2. 재현 테스트를 먼저 작성한다 (실패해야 함).
3. 수정 후 테스트를 통과시킨다.
4. 커밋 메시지 footer에 `Fixes #$ARGUMENTS` 를 넣는다.
```

```text
> /fix-issue 482
```

**이름 있는 인자:**

```markdown
---
name: deploy
description: Deploys a service to an environment.
arguments: [service, env]
argument-hint: "[service] [env]"
disable-model-invocation: true
---

`$service` 를 `$env` 환경에 배포한다.
`$env` 가 `prod` 이면 반드시 사용자에게 한 번 더 확인받는다.
```

```text
> /deploy media-gateway staging
> /deploy "recording service" prod     ← 따옴표로 공백 포함 인자
```

> [!tip] `${CLAUDE_SKILL_DIR}`로 스크립트 경로 고정
> Claude의 현재 작업 디렉터리는 프로젝트 루트입니다. Skill 폴더 안 스크립트는 이렇게 가리키세요:
> ```markdown
> `python ${CLAUDE_SKILL_DIR}/scripts/validate.py <file>` 를 실행한다.
> ```

### 5.4 동적 컨텍스트 주입 — `` !`command` ``

Skill 내용이 Claude에게 전달되기 **전에** 셸 명령을 실행하고, 그 출력으로 자리를 치환합니다. "Claude가 명령을 실행할지 판단"하는 게 아니라 **전처리**입니다.

````markdown
---
name: summarizing-changes
description: Summarizes current uncommitted changes and suggests a commit message.
disable-model-invocation: true
---

## 현재 브랜치
!`git branch --show-current`

## 변경 파일
!`git status --short`

## Diff
!`git diff HEAD || true`

위 변경 사항을 3줄로 요약하고 Conventional Commits 형식의 커밋 메시지를 제안하라.
````

여러 줄 명령은 ` ```! ` 펜스 블록으로:

````markdown
```!
echo "== Recent commits =="
git log --oneline -10
echo "== Test status =="
npm test --silent 2>&1 | tail -5 || true
```
````

> [!warning] 주의사항
> - 명령이 **0이 아닌 코드로 종료하면 Skill 호출 전체가 중단**됩니다 → 실패 가능한 명령엔 `|| true`
> - 주입 명령도 **권한 규칙의 검사 대상**입니다
> - 관리자는 `"disableSkillShellExecution": true` 설정으로 이 기능을 끌 수 있습니다
> - 출력이 큰 명령(`git diff` 전체 등)은 토큰을 많이 먹습니다 → `| head -300` 등으로 제한

### 5.5 도구 권한 — allowed-tools / disallowed-tools

```markdown
---
name: committing
description: Stages and commits changes with a conventional commit message.
disable-model-invocation: true
allowed-tools: Bash(git add *) Bash(git commit *) Bash(git status *) Bash(git diff *)
---
```

- `allowed-tools`: 해당 턴에서 **승인 프롬프트 없이** 쓸 수 있게 미리 허용 (전체 도구를 제한하는 게 아님)
- `disallowed-tools`: Skill 활성 동안 도구를 **아예 제거** — "읽기 전용 리뷰 Skill" 같은 경우에 유용

```markdown
---
name: reviewing-security
description: Performs a read-only security review of the codebase.
disallowed-tools: Write Edit NotebookEdit
---
```

### 5.6 Skill과 Slash Command의 관계

`.claude/commands/review.md` 파일은 여전히 `/review` 명령을 만듭니다. 하지만 Skill은 그 상위 호환입니다:

| | `.claude/commands/x.md` | `.claude/skills/x/SKILL.md` |
|---|---|---|
| `/x` 호출 | ✅ | ✅ |
| 부가 파일 (scripts 등) | ❌ | ✅ |
| Claude 자동 호출 | ❌ | ✅ |
| 호출 제어 필드 | 제한적 | ✅ |

이름이 겹치면 **Skill이 우선**합니다. 새로 만든다면 **Skill로 만드세요.**

### 5.7 우선순위와 위치

```text
Enterprise(관리형)  >  Personal(~/.claude/skills)  >  Project(.claude/skills)
Plugin Skill은 /plugin-name:skill-name 으로 네임스페이스가 분리되어 충돌하지 않음
Nested: packages/api/.claude/skills/...  → 그 하위 디렉터리 파일을 건드릴 때 로드
```

> [!tip] 모노레포 팁
> `apps/web/.claude/skills/`, `services/recorder/.claude/skills/` 처럼 **하위 디렉터리별 Skill**을 두면, 해당 영역 작업 시에만 로드되어 컨텍스트가 깔끔해집니다.

---

## Part 6. 실전 예제 3종

### 6.1 예제 ① — 커밋 메시지 Skill (지침만)

````markdown
---
name: writing-commit-messages
description: >-
  Writes git commit messages following the team's Conventional Commits rules.
  Use when the user asks to commit, write a commit message, or says "커밋해줘".
---

# Writing Commit Messages

## Format
```
<type>(<scope>): <subject>

<body>

Refs: <JIRA-KEY>
```

## Rules
- type: feat | fix | refactor | perf | test | docs | chore | build | ci
- scope: 최상위 모듈 디렉터리명 (예: `recorder`, `player`, `onvif`)
- subject: 영어 명령형, 50자 이내, 마침표 없음
- body: "왜" 바꿨는지 설명, 72자 줄바꿈
- 브랜치명에 `VMS-123` 패턴이 있으면 footer에 `Refs: VMS-123`

## Examples
Input: player의 seek 시 프레임 드롭 수정 (브랜치 fix/VMS-881-seek-drop)
Output:
```
fix(player): prevent frame drops when seeking to keyframe

Seeking to a non-keyframe flushed the decoder twice, dropping
up to 12 frames. Seek now snaps to the nearest prior keyframe.

Refs: VMS-881
```
````

> [!note] 포인트
> 규칙을 장황하게 설명하는 대신 **입력/출력 예시 한 쌍**을 넣었습니다. 스타일 전달에는 예시가 설명보다 훨씬 효과적입니다.

### 6.2 예제 ② — PR 리뷰 Skill (지침 + reference 분리)

```text
reviewing-pull-requests/
├── SKILL.md
└── references/
    ├── security.md
    ├── performance.md
    └── style.md
```

**SKILL.md**

````markdown
---
name: reviewing-pull-requests
description: >-
  Reviews code changes or pull requests for bugs, security issues, and
  performance problems using the team checklist. Use when asked to review a
  PR, a diff, or changed files, or when the user says "코드 리뷰해줘".
---

# Reviewing Pull Requests

## Workflow
1. 변경 범위를 파악한다 (`git diff --stat main...HEAD`).
2. 변경 유형에 따라 필요한 체크리스트**만** 읽는다:
   - 인증/입력 처리/외부 호출 변경 → [references/security.md](references/security.md)
   - 루프/쿼리/스트리밍/메모리 변경 → [references/performance.md](references/performance.md)
   - 항상 → [references/style.md](references/style.md)
3. 발견 사항을 아래 형식으로 보고한다. 심각도 순 정렬.

## Output format
| 심각도 | 파일:라인 | 문제 | 제안 |
|---|---|---|---|
| 🔴 Critical / 🟠 Major / 🟡 Minor | `src/x.ts:42` | 한 문장 | 코드 또는 한 문장 |

발견 사항이 없으면 "No issues found"와 확인한 체크리스트 목록만 출력한다.
````

**references/security.md (일부)**

```markdown
# Security checklist

## Contents
- Input validation
- Credentials
- Network calls

## Input validation
- 외부 입력(HTTP, RTSP URL, ONVIF 응답)은 길이·형식 검증 후 사용
- SQL은 파라미터 바인딩만 허용, 문자열 연결 금지

## Credentials
- 카메라 계정/비밀번호가 로그에 출력되지 않는지 확인 (rtsp://user:pass@ 형태 포함)
...
```

### 6.3 예제 ③ — 설정 검증 Skill (스크립트 + 피드백 루프)

```text
validating-camera-config/
├── SKILL.md
└── scripts/
    └── validate_config.py
```

**SKILL.md**

````markdown
---
name: validating-camera-config
description: >-
  Validates and fixes camera configuration JSON files (cameras.json) for
  required fields, IP format, duplicate IDs, and stream settings. Use when
  editing or creating camera config files or when the user asks to check
  a camera configuration.
---

# Validating Camera Config

## Workflow (반드시 이 루프를 따른다)
1. 설정 파일을 수정한다.
2. 검증을 실행한다:
   `python ${CLAUDE_SKILL_DIR}/scripts/validate_config.py <path>`
3. `ERROR`가 있으면 메시지대로 고치고 **2번으로 돌아간다**.
4. `OK`가 출력될 때만 작업 완료를 보고한다.

## Rules
- 스크립트의 검증 규칙을 우회하거나 스크립트를 수정하지 않는다.
````

**scripts/validate_config.py**

```python
#!/usr/bin/env python3
"""Validate cameras.json. Prints 'OK' or one 'ERROR: ...' line per problem."""
import ipaddress
import json
import sys

REQUIRED = ("id", "name", "ip", "rtsp_port", "fps")
MAX_FPS = 60  # 지원 인코더 최대치 (사양서 기준)


def validate(cameras):
    errors, seen = [], set()
    for i, cam in enumerate(cameras):
        where = f"cameras[{i}]"
        for key in REQUIRED:
            if key not in cam:
                errors.append(f"{where}: missing required field '{key}'")
        cid = cam.get("id")
        if cid in seen:
            errors.append(f"{where}: duplicate id '{cid}'")
        seen.add(cid)
        try:
            ipaddress.ip_address(cam.get("ip", ""))
        except ValueError:
            errors.append(f"{where}: invalid ip '{cam.get('ip')}'")
        port = cam.get("rtsp_port")
        if not isinstance(port, int) or not 1 <= port <= 65535:
            errors.append(f"{where}: rtsp_port must be int 1-65535, got {port!r}")
        fps = cam.get("fps")
        if not isinstance(fps, int) or not 1 <= fps <= MAX_FPS:
            errors.append(f"{where}: fps must be int 1-{MAX_FPS}, got {fps!r}")
    return errors


def main():
    if len(sys.argv) != 2:
        print("ERROR: usage: validate_config.py <cameras.json>")
        return 2
    try:
        with open(sys.argv[1], encoding="utf-8") as f:
            data = json.load(f)
    except FileNotFoundError:
        print(f"ERROR: file not found: {sys.argv[1]}")
        return 1
    except json.JSONDecodeError as e:
        print(f"ERROR: invalid JSON at line {e.lineno} col {e.colno}: {e.msg}")
        return 1
    cameras = data.get("cameras") if isinstance(data, dict) else None
    if not isinstance(cameras, list):
        print("ERROR: top-level object must contain a 'cameras' array")
        return 1
    errors = validate(cameras)
    for e in errors:
        print(f"ERROR: {e}")
    if not errors:
        print(f"OK: {len(cameras)} cameras valid")
    return 1 if errors else 0


if __name__ == "__main__":
    sys.exit(main())
```

**실행 예**

```text
$ python validate_config.py cameras.json
ERROR: cameras[1]: duplicate id 'cam-01'
ERROR: cameras[2]: invalid ip '192.168.1.300'
ERROR: cameras[2]: fps must be int 1-60, got 120
```

> [!success] 이 예제가 중급의 핵심인 이유
> - **검증은 결정론적 스크립트**, **수정은 Claude** — 각자 잘하는 일을 분담
> - 에러 메시지가 "무엇을 어떻게 고칠지"를 알려주므로 Claude가 자율적으로 루프를 돈다
> - "OK가 나올 때만 완료" 규칙으로 **조기 종료를 방지**


---

# 🔴 고급

## Part 7. 고급 패턴 — 워크플로·검증 루프·자유도 설계

### 7.1 자유도(Degrees of Freedom) 설계

모든 지침을 같은 강도로 쓰면 안 됩니다. **작업이 얼마나 깨지기 쉬운가**에 맞춰 자유도를 조절하세요.

```mermaid
flowchart LR
    H["🟢 높은 자유도<br/>텍스트 가이드<br/>예: 코드 리뷰 관점"] --- M["🟡 중간 자유도<br/>의사코드 / 파라미터 스크립트<br/>예: 보고서 생성"] --- L["🔴 낮은 자유도<br/>정확한 명령<br/>예: DB 마이그레이션"]
```

| 자유도 | 언제 | 작성 방식 |
|---|---|---|
| 높음 | 여러 접근이 모두 유효, 맥락 판단이 중요 | "~를 고려하라", 관점 목록 |
| 중간 | 선호 패턴은 있지만 변형 허용 | 템플릿, 파라미터가 있는 스크립트 |
| 낮음 | 순서·정확성이 치명적 | `python scripts/migrate.py --verify --backup` + "**명령을 수정하지 마라**" |

> [!example] 비유
> 높은 자유도 = 넓은 들판(어느 길로 가도 됨), 낮은 자유도 = 양옆이 절벽인 좁은 다리(정해진 길만).

### 7.2 체크리스트 워크플로

복잡한 작업은 Claude가 **복사해서 체크해 나갈 수 있는** 체크리스트를 주세요.

````markdown
## Release workflow

다음 체크리스트를 응답에 복사하고 진행하면서 체크한다:

```
Release Progress:
- [ ] 1. CHANGELOG 초안 생성 (scripts/changelog.py)
- [ ] 2. 버전 번호 결정 (semver 규칙: references/versioning.md)
- [ ] 3. 버전 파일 업데이트
- [ ] 4. 전체 테스트 통과 확인
- [ ] 5. 릴리스 노트 사용자 확인 받기
```

**4번이 실패하면 5번으로 넘어가지 않는다.**
````

### 7.3 조건 분기 워크플로

```markdown
## 작업 유형 판별
- **새 문서 작성?** → [Creation workflow](#creation-workflow)
- **기존 문서 수정?** → [Editing workflow](#editing-workflow)
- **포맷 변환만?** → `scripts/convert.py` 실행 후 종료
```

### 7.4 Plan → Validate → Execute 패턴 (고위험 일괄 작업)

수백 개 파일 수정, 대량 DB 업데이트처럼 **되돌리기 어려운 일괄 작업**에 씁니다.

```mermaid
flowchart LR
    A[Claude: 변경 계획 작성<br/>changes.json] --> B{scripts/validate_plan.py}
    B -- "ERROR: 구체적 메시지" --> A
    B -- OK --> C[사용자 확인]
    C --> D[scripts/apply.py changes.json]
    D --> E[scripts/verify.py]
```

````markdown
## Bulk rename workflow
1. 바로 수정하지 말고 먼저 `changes.json`을 작성한다:
   ```json
   [{"from": "src/old_name.ts", "to": "src/new_name.ts"}]
   ```
2. `python scripts/validate_plan.py changes.json` — 충돌, 존재하지 않는 경로, import 깨짐 검사
3. 오류가 있으면 계획을 고치고 2번 반복
4. 계획 요약을 사용자에게 보여주고 승인을 받는다
5. `python scripts/apply.py changes.json`
6. `python scripts/verify.py` 로 빌드/테스트 확인
````

> [!important] 왜 효과적인가
> 1. 실행 전에 오류를 잡는다 (중간 산출물이 검증 가능)
> 2. 에러 메시지가 구체적이어서 Claude가 스스로 고친다
> 3. 사람이 검토할 수 있는 **체크포인트**가 생긴다

### 7.5 템플릿: 엄격 vs 유연

```markdown
## 엄격 (기계가 읽는 출력 — 형식을 정확히 지킨다)
출력은 반드시 아래 JSON 스키마를 따른다. 다른 텍스트를 붙이지 않는다.
{"severity": "high|medium|low", "device": "string", "summary": "string"}

## 유연 (사람이 읽는 출력 — 상황에 맞게 조정 가능)
아래는 권장 구조다. 내용에 따라 섹션을 합치거나 생략해도 된다.
```

### 7.6 MCP 도구와 결합하기

Skill 안에서 MCP 도구를 언급할 때는 **완전한 이름(`서버명:도구명`)** 을 쓰세요. MCP 서버가 여러 개일 때 Claude가 도구를 못 찾는 것을 방지합니다.

```markdown
## Workflow
1. `Jira:search_issues` 로 `project = VMS AND status = "In Review"` 이슈를 조회한다.
2. 각 이슈의 PR을 `GitHub:get_pull_request` 로 가져온다.
3. [references/triage-rules.md](references/triage-rules.md) 기준으로 우선순위를 매긴다.
4. 결과를 `Slack:post_message` 로 `#vms-dev` 채널에 게시한다 (사용자 승인 후).
```

> [!tip] MCP + Skill 시너지
> MCP는 **능력**(도구)을, Skill은 **절차**(언제 어떤 도구를 어떤 순서로)를 제공합니다. 같은 MCP 서버라도 Skill에 따라 "버그 트리아지", "스프린트 리포트", "릴리스 체크" 등 다른 업무로 재사용됩니다.

### 7.7 Skill 조합 (Composability)

Skill들은 **자동으로 조합**됩니다. 예: "카메라 로그 분석해서 엑셀 보고서로 만들어줘"
→ `analyzing-camera-logs` Skill(분석) + `xlsx` Skill(출력)이 함께 로드됨.

설계 원칙:

- **한 Skill = 한 책임** (분석 Skill이 엑셀 서식까지 책임지지 않게)
- 출력은 **다른 Skill이 소비하기 좋은 형태**(JSON, CSV)로
- Skill끼리 서로를 직접 호출하도록 강하게 묶지 말 것 — 조합은 Claude가 한다

---

## Part 8. 서브에이전트, 훅, 경로 기반 활성화

### 8.1 `context: fork` — 서브에이전트에서 실행

Skill이 대량의 파일을 읽어야 하면 메인 대화 컨텍스트가 오염됩니다. `context: fork`로 **별도 컨텍스트의 서브에이전트**에서 실행하고 **요약만** 돌려받으세요.

```markdown
---
name: mapping-codebase
description: Maps the architecture of an unfamiliar codebase and reports modules, entry points, and data flow. Use when onboarding to a new repository or asked "이 프로젝트 구조 파악해줘".
context: fork
agent: Explore
---

$ARGUMENTS 범위의 코드베이스 구조를 파악한다.

1. Glob/Grep으로 엔트리포인트, 설정, 빌드 파일을 찾는다.
2. 주요 모듈별 책임을 파악한다.
3. 아래 형식으로 **500단어 이내** 요약을 반환한다:
   - 모듈 표 (이름 | 책임 | 주요 파일)
   - 데이터 흐름 mermaid 다이어그램
   - 다음에 읽어야 할 파일 Top 5
```

```mermaid
flowchart LR
    Main[메인 대화<br/>컨텍스트 깨끗하게 유지] -- "/mapping-codebase src/" --> Sub[Explore 서브에이전트<br/>수백 개 파일 읽음]
    Sub -- "500단어 요약만" --> Main
```

> [!tip] fork가 유리한 경우
> - 대량 탐색/조사 (코드베이스 매핑, 로그 전수 조사)
> - 결과만 필요하고 과정은 필요 없는 작업
> - `background: false`로 두면 결과를 기다렸다가 이어서 작업

### 8.2 Skill 스코프 훅 (hooks)

Skill이 호출되었을 때만 활성화되는 훅을 등록할 수 있습니다. 형식은 Claude Code의 settings 훅과 같습니다.

```yaml
---
name: editing-protobuf
description: Edits .proto files and regenerates code. Use when modifying protobuf definitions.
paths: ["**/*.proto"]
hooks:
  PostToolUse:
    - matcher: "Edit|Write"
      hooks:
        - type: command
          command: "buf lint || true"
---
```

> [!example] 활용 아이디어
> - 파일 수정 후 자동 포맷터/린터 실행
> - 특정 위험 명령 차단 (PreToolUse에서 exit code로 거부)
> - Skill 사용 로그 기록 (감사용)

### 8.3 `paths` — 파일 패턴 기반 자동 활성화

```yaml
paths: ["**/*.proto", "proto/**"]
```

해당 glob에 맞는 파일을 다룰 때만 자동 활성화 후보가 됩니다. 범용적인 이름의 Skill이 엉뚱한 곳에서 트리거되는 것을 막는 **정밀 타깃팅** 도구입니다.

### 8.4 설정으로 Skill 제어 (코드 수정 없이)

| 방법 | 용도 |
|---|---|
| `/permissions` 에서 `Skill(name)`, `Skill(name *)` 규칙 | 특정 Skill 허용/거부 |
| settings의 `skillOverrides` | `"on"`, `"name-only"`, `"user-invocable-only"`, `"off"` 로 Skill 상태 변경 |
| `/skill-doctor` | 각 Skill의 컨텍스트 비용과 사용 빈도 리포트 |
| `/reload-skills` | 새 최상위 skills 디렉터리 생성 후 재로딩 |

> [!tip] 컨텍스트 다이어트
> Skill이 많아지면 `/skill-doctor`로 **비용 대비 사용 빈도가 낮은 Skill**을 찾아 `name-only` 또는 `off`로 돌리세요. Claude Code 목록에서 `description`+`when_to_use`는 약 1,536자에서 잘리므로 **핵심을 앞에** 두세요.

---

## Part 9. Claude API & Agent SDK에서 Skills 쓰기

### 9.1 API 개념 구조

```mermaid
flowchart LR
    App[내 애플리케이션] -- "messages.create<br/>container.skills=[...]<br/>tools=[code_execution]" --> API[Claude API]
    API --> C[코드 실행 컨테이너<br/>Skill 파일 마운트]
    C -- "file_id" --> API
    App -- "files.download(file_id)" --> API
```

필수 3요소:

1. `container.skills` — 사용할 Skill 목록 (요청당 **최대 20개**)
2. `tools` 에 **code execution 도구** (`code_execution_20250825`)
3. 생성 파일은 **Files API**로 다운로드

> [!note] 베타 헤더
> 초기에는 `anthropic-beta: skills-2025-10-02` 헤더가 필요했지만, 현재 Skills API는 **GA(정식)** 이며 베타 헤더가 필요 없습니다. 최신 SDK에서는 `client.beta.skills` 대신 `client.skills`를 사용합니다. (구버전 SDK를 쓰면 예제가 다를 수 있습니다.)

### 9.2 기본 제공 Skill 사용 (Python)

```python
import anthropic

client = anthropic.Anthropic()  # ANTHROPIC_API_KEY 환경 변수 사용

response = client.messages.create(
    model="claude-opus-5-5",           # 사용 가능한 최신 모델 ID로 교체
    max_tokens=4096,
    container={
        "skills": [
            {"type": "anthropic", "skill_id": "xlsx", "version": "latest"}
        ]
    },
    messages=[{"role": "user", "content": "월별 카메라 장애 건수 추이 엑셀 템플릿을 만들어줘"}],
    tools=[{"type": "code_execution_20250825", "name": "code_execution"}],
)
```

| 필드 | 값 |
|---|---|
| `type` | `"anthropic"` (기본 제공) 또는 `"custom"` |
| `skill_id` | 기본 제공: `pptx`, `xlsx`, `docx`, `pdf` / 커스텀: `skill_01...` |
| `version` | 기본 제공: 날짜형(예 `20251013`) 또는 `latest` / 커스텀: `skver_01...` 또는 `latest` |

### 9.3 생성된 파일 다운로드

```python
def extract_file_ids(response):
    file_ids = []
    for item in response.content:
        if item.type == "bash_code_execution_tool_result":
            result = item.content
            if result.type == "bash_code_execution_result":
                for out in result.content:
                    file_ids.append(out.file_id)
    return file_ids

for file_id in extract_file_ids(response):
    meta = client.files.retrieve_metadata(file_id=file_id)
    client.files.download(file_id=file_id).write_to_file(meta.filename)
    print("Downloaded:", meta.filename)
```

### 9.4 커스텀 Skill 업로드 & 버전 관리

```python
import anthropic
from anthropic.lib import files_from_dir

client = anthropic.Anthropic()

# 1) 생성 (최초 1회) — SDK 버전에 따라 파라미터명이 다를 수 있으니 API 레퍼런스 확인
skill = client.skills.create(
    display_title="Camera Log Analyzer",
    files=files_from_dir("skills/analyzing-camera-logs"),
)
print(skill.id)  # skill_01...

# 2) 새 버전 업로드 (폴더 전체 스냅샷, SKILL.md의 name이 기존과 같아야 함)
v2 = client.skills.versions.create(
    skill_id=skill.id,
    files=files_from_dir("skills/analyzing-camera-logs"),
)
print(v2.version)  # skver_01... 형태

# 3) 사용 — 프로덕션에서는 버전 고정(pin)!
response = client.messages.create(
    model="claude-opus-5-5",
    max_tokens=4096,
    container={"skills": [
        {"type": "custom", "skill_id": skill.id, "version": v2.version},
        {"type": "anthropic", "skill_id": "xlsx", "version": "latest"},
    ]},
    messages=[{"role": "user", "content": "첨부 로그 분석해서 엑셀로 정리해줘"}],
    tools=[{"type": "code_execution_20250825", "name": "code_execution"}],
)
```

CLI로도 가능합니다:

```bash
ant apply skills/analyzing-camera-logs
```

> [!warning] 업로드 제약
> - 전체 업로드 **30MB 미만** (압축 해제 기준)
> - `name` / `description` 규칙은 [[AI technique/skills/Claude-Skills-완전정복-강좌#3.2 공통 frontmatter 규칙 (모든 환경)\|Part 3.2]]와 동일
> - API 실행 환경은 **네트워크 없음 / 패키지 설치 불가** → 스크립트는 표준 라이브러리 또는 사전 설치 패키지만
> - 관련 엔드포인트: `GET /v1/skills/{id}`, `DELETE /v1/skills/{id}`, `GET /v1/skills/{id}/versions/latest`

> [!important] 프로덕션 원칙: 버전 고정
> `latest`는 Skill이 업데이트되면 **배포된 앱의 동작이 조용히 바뀝니다.** 프로덕션에서는 반드시 특정 버전 ID를 고정하고, 새 버전은 Eval([[AI technique/skills/Claude-Skills-완전정복-강좌#Part 11. 평가 주도 개발 (Eval-Driven Skill Development)\|Part 11]]) 통과 후 교체하세요.

### 9.5 멀티턴 & 장시간 작업

```python
# 컨테이너 재사용 — 이전 턴에서 만든 파일이 유지됨
response2 = client.messages.create(
    model="claude-opus-5-5",
    max_tokens=4096,
    container={"id": response.container.id, "skills": [...]},
    messages=[...이전 대화..., {"role": "user", "content": "차트도 추가해줘"}],
    tools=[{"type": "code_execution_20250825", "name": "code_execution"}],
)

# stop_reason == "pause_turn" 이면 응답 content를 그대로 assistant 메시지로 붙여
# 같은 container id로 다시 요청 → Claude가 이어서 작업
```

### 9.6 Agent SDK에서 Skill 쓰기

Agent SDK는 Claude Code와 같은 엔진이므로 **파일시스템 Skill**(`.claude/skills/`)을 그대로 씁니다. 핵심은 (1) 설정 소스를 로드하고 (2) `Skill` 도구를 허용하는 것입니다.

```python
import asyncio
from claude_agent_sdk import query, ClaudeAgentOptions

options = ClaudeAgentOptions(
    cwd="/path/to/project",                 # .claude/skills/ 가 있는 프로젝트
    setting_sources=["user", "project"],    # ~/.claude/skills, .claude/skills 로드
    allowed_tools=["Skill", "Read", "Grep", "Glob", "Bash"],
)

async def main():
    async for message in query(prompt="logs/ 폴더의 카메라 로그 분석해줘", options=options):
        print(message)

asyncio.run(main())
```

> [!note]
> SDK 버전에 따라 옵션 이름이 다를 수 있습니다. 핵심 개념(설정 소스 로드 + Skill 도구 허용)만 기억하고 세부는 SDK 문서를 확인하세요.

---

## Part 10. 배포 — 팀 공유와 플러그인

### 10.1 배포 전략 매트릭스

| 대상 | 방법 | 장점 | 단점 |
|---|---|---|---|
| 나 혼자 | `~/.claude/skills/` | 즉시 | 공유 불가 |
| 한 저장소 팀 | `.claude/skills/` 를 **git 커밋** | 코드 리뷰·버전 관리 | 저장소 단위 |
| 여러 저장소/조직 | **Plugin + Marketplace** | 중앙 배포, 버전, 네임스페이스 | 초기 셋업 |
| 서비스/앱 | **Skills API** 업로드 | 워크스페이스 공유, 버전 고정 | API 환경 제약 |
| claude.ai 사용자 | zip 업로드 (개인) / 조직 관리 기능 | 비개발자도 사용 | 개별 업로드 |

### 10.2 Plugin으로 묶기 (Claude Code / Cowork)

```text
vms-dev-toolkit/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   ├── writing-commit-messages/SKILL.md
│   ├── reviewing-pull-requests/
│   │   ├── SKILL.md
│   │   └── references/...
│   └── analyzing-camera-logs/
│       ├── SKILL.md
│       └── scripts/analyze_logs.py
├── commands/          (선택)
├── agents/            (선택: 서브에이전트 정의)
├── hooks/             (선택)
└── .mcp.json          (선택: MCP 서버 정의)
```

**`.claude-plugin/plugin.json`**

```json
{
  "name": "vms-dev-toolkit",
  "version": "1.2.0",
  "description": "VMS 개발팀 공용 Skills: 커밋, 리뷰, 카메라 로그 분석",
  "author": { "name": "VMS SW Team" }
}
```

설치 후 Skill은 `/vms-dev-toolkit:analyzing-camera-logs` 처럼 **네임스페이스**가 붙어 다른 Skill과 충돌하지 않습니다. 플러그인 내부 스크립트 경로는 `${CLAUDE_PLUGIN_ROOT}`를 사용하세요.

> [!tip] 사내 마켓플레이스
> git 저장소 하나에 `marketplace.json`으로 여러 플러그인을 나열하면 사내 마켓플레이스가 됩니다. 팀원은 `/plugin marketplace add <repo>` → `/plugin install <name>` 으로 설치합니다.

### 10.3 Single Source of Truth 운영 구조

```mermaid
flowchart TB
    Repo[(git: team-skills 저장소<br/>원본)] -->|CI: plugin 빌드| P[Claude Code Plugin<br/>Marketplace]
    Repo -->|CI: ant apply / SDK| A[Skills API<br/>버전 생성]
    Repo -->|CI: zip 아티팩트| Z[claude.ai 업로드용 zip]
    Repo -->|CI: lint + eval| E{품질 게이트}
    E -.통과해야 배포.-> P & A & Z
```

**CI 예시 (GitHub Actions 개념)**

```yaml
name: skills-ci
on: [push]
jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: python tools/validate_skill.py skills/*/
      - run: python tools/run_evals.py --all   # Part 11
  publish:
    needs: validate
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: for d in skills/*/; do ant apply "$d"; done
        env: { ANTHROPIC_API_KEY: "${{ secrets.ANTHROPIC_API_KEY }}" }
```

### 10.4 Skill 린터 — `validate_skill.py`

CI와 로컬에서 쓰는 frontmatter 검증기입니다. (표준 라이브러리만 사용)

```python
#!/usr/bin/env python3
"""Lint Agent Skill directories. Usage: validate_skill.py <skill_dir> [...]"""
import re
import sys
from pathlib import Path

NAME_RE = re.compile(r"^[a-z0-9]+(-[a-z0-9]+)*$")
RESERVED = ("anthropic", "claude")
MAX_NAME, MAX_DESC = 64, 1024      # 공식 제한
MAX_BODY_LINES = 500               # 공식 권장치
XML_TAG = re.compile(r"<[^>]+>")


def parse_frontmatter(text):
    if not text.startswith("---\n"):
        return None, "frontmatter must start at line 1 with '---'"
    end = text.find("\n---", 4)
    if end == -1:
        return None, "closing '---' not found"
    fm, body = text[4:end], text[end + 4:]
    fields, key = {}, None
    for line in fm.splitlines():
        m = re.match(r"^([A-Za-z_-]+):\s*(.*)$", line)
        if m:
            key, val = m.group(1), m.group(2).strip()
            fields[key] = "" if val in (">", ">-", "|", "|-") else val.strip("\"'")
        elif key and line.startswith((" ", "\t")):
            fields[key] = (fields[key] + " " + line.strip()).strip()
    return (fields, body), None


def lint(skill_dir):
    errs, warns = [], []
    path = Path(skill_dir) / "SKILL.md"
    if not path.is_file():
        return [f"{path}: missing SKILL.md"], warns
    parsed, err = parse_frontmatter(path.read_text(encoding="utf-8"))
    if err:
        return [f"{path}: {err}"], warns
    fields, body = parsed
    name, desc = fields.get("name", ""), fields.get("description", "")
    if not name:
        warns.append("name missing (Claude Code uses dir name; API requires it)")
    else:
        if len(name) > MAX_NAME:
            errs.append(f"name longer than {MAX_NAME} chars")
        if not NAME_RE.match(name):
            errs.append(f"name '{name}' must be lowercase letters, digits, hyphens")
        if any(r in name.lower() for r in RESERVED):
            errs.append(f"name '{name}' contains reserved word")
        if name != Path(skill_dir).resolve().name:
            warns.append(f"name '{name}' differs from directory name")
    if not desc:
        errs.append("description is empty")
    elif len(desc) > MAX_DESC:
        errs.append(f"description is {len(desc)} chars (> {MAX_DESC})")
    if XML_TAG.search(name + desc):
        errs.append("XML tags are not allowed in name/description")
    if desc and re.match(r"(?i)^(i |you |i can|you can)", desc):
        warns.append("description should be third person")
    if desc and not re.search(r"(?i)\buse (when|for|this)", desc):
        warns.append("description should say WHEN to use the skill")
    n = body.count("\n")
    if n > MAX_BODY_LINES:
        warns.append(f"body is {n} lines (> {MAX_BODY_LINES}); split into references")
    if "\\" in "".join(re.findall(r"\]\(([^)]+)\)", body)):
        errs.append("use forward slashes in file links")
    return errs, warns


def main(argv):
    if not argv:
        print("usage: validate_skill.py <skill_dir> [...]")
        return 2
    failed = False
    for d in argv:
        errs, warns = lint(d)
        for w in warns:
            print(f"WARN  {d}: {w}")
        for e in errs:
            print(f"ERROR {d}: {e}")
        if not errs:
            print(f"OK    {d}")
        failed |= bool(errs)
    return 1 if failed else 0


if __name__ == "__main__":
    sys.exit(main(sys.argv[1:]))
```

```text
$ python validate_skill.py skills/*/
WARN  skills/Claude_Helper/: description should be third person
WARN  skills/Claude_Helper/: description should say WHEN to use the skill
ERROR skills/Claude_Helper/: name 'Claude_Helper' must be lowercase letters, digits, hyphens
ERROR skills/Claude_Helper/: name 'Claude_Helper' contains reserved word
OK    skills/analyzing-camera-logs/
WARN  skills/utils/: description should say WHEN to use the skill
OK    skills/utils/
```

---

## Part 11. 평가 주도 개발 (Eval-Driven Skill Development)

> [!quote] 고급 사용자와 중급 사용자를 가르는 단 하나의 습관
> **"Skill을 쓰기 전에 Eval부터 만든다."** — TDD의 Skill 버전입니다.

### 11.1 프로세스

```mermaid
flowchart LR
    A[1. Skill 없이 실제 작업 실행] --> B[2. 실패/부족한 점 기록]
    B --> C[3. Eval 시나리오 3개 이상 작성]
    C --> D[4. 베이스라인 측정]
    D --> E[5. 최소한의 지침 작성]
    E --> F[6. Eval 재실행]
    F -- 미달 --> E
    F -- 통과 --> G[배포]
```

### 11.2 Eval 시나리오 형식

```json
{
  "skills": ["analyzing-camera-logs"],
  "query": "logs/nvr-0912.log 분석해서 오프라인 된 카메라랑 원인 알려줘",
  "files": ["fixtures/nvr-0912.log"],
  "expected_behavior": [
    "scripts/analyze_logs.py 를 실행한다 (직접 파싱 코드를 새로 쓰지 않는다)",
    "CAM-07 이 RTSP timeout 으로 3회 끊긴 것을 보고한다",
    "장비별 표와 시간대별 요약을 모두 포함한다",
    "로그에 있는 비밀번호(rtsp://user:pass@)를 출력하지 않는다"
  ],
  "must_not_trigger_on": ["엑셀 수식 고쳐줘", "PR 리뷰해줘"]
}
```

> [!tip] 트리거 Eval도 반드시
> "써야 할 때 쓰는가"(positive)와 "쓰지 말아야 할 때 안 쓰는가"(negative, `must_not_trigger_on`)를 **둘 다** 테스트하세요. description 튜닝은 이 두 지표의 균형 맞추기입니다.

### 11.3 Claude A / Claude B 반복 개발법

| 역할 | 인스턴스 | 하는 일 |
|---|---|---|
| **Claude A** (작성자) | Skill 개발용 대화 | Skill 초안 작성, 수정 |
| **Claude B** (사용자) | Skill이 로드된 **새** 대화 | 실제 작업 수행 → 관찰 대상 |
| **나** (관찰자) | — | B의 실패를 A에게 피드백 |

관찰 포인트:

- B가 **예상하지 못한 순서**로 파일을 읽는가? → 구조가 직관적이지 않음
- 특정 reference를 **매번** 읽는가? → 그 내용은 `SKILL.md` 본문으로 올릴 것
- 어떤 파일을 **한 번도** 안 읽는가? → 불필요하거나 링크가 약함
- 스크립트 대신 **코드를 새로 짜는가?** → "실행하라"는 지시가 불명확

> [!tip] 모델별 테스트
> Haiku는 더 많은 안내가 필요하고, Opus는 설명이 적어도 됩니다. 여러 모델에서 쓸 Skill이면 **가장 작은 모델 기준으로 충분히 명확하게**, 가장 큰 모델 기준으로 **장황하지 않게** 균형을 잡으세요.

### 11.4 skill-creator로 Eval 자동화

claude.ai / Cowork의 `skill-creator` Skill은 Skill 작성뿐 아니라 **Eval 실행, 벤치마크, description 최적화**까지 지원합니다. "이 Skill의 트리거 정확도를 측정하고 description을 개선해줘"처럼 요청해 보세요.

---

## Part 12. 보안, 성능, 운영

### 12.1 보안 — Skill은 "소프트웨어 설치"다

> [!danger] 신뢰할 수 있는 출처의 Skill만 사용하세요
> Skill은 Claude에게 지시를 내리고 코드를 실행시킵니다. 악성 Skill은 데이터 유출, 의도치 않은 도구 사용을 유발할 수 있습니다.

**외부 Skill 감사 체크리스트**

- [ ] `SKILL.md`와 **모든** 번들 파일(스크립트, 이미지, 리소스)을 읽었다
- [ ] 예상치 못한 네트워크 호출(`curl`, `requests`, `fetch`)이 없다
- [ ] Skill 목적과 무관한 파일 접근(`~/.ssh`, `.env`, 자격 증명)이 없다
- [ ] 외부 URL에서 지시를 가져오는 구조가 아니다 (가져온 콘텐츠가 프롬프트 인젝션일 수 있음)
- [ ] 의존성이 고정(pin)되어 있다 — 신뢰하던 Skill도 의존성 변경으로 오염될 수 있음
- [ ] 부작용 있는 Skill은 `disable-model-invocation: true`

**자체 Skill 작성 시**

- 비밀 값(API 키, 비밀번호)을 Skill 파일에 **절대** 넣지 말 것 → 환경 변수 사용
- 스크립트 출력에 민감 정보가 섞이지 않게 마스킹 (출력이 컨텍스트로 들어가므로)
- 데이터 보존: Agent Skills는 **ZDR(Zero Data Retention) 적용 대상이 아님** — 민감 데이터 처리 시 정책 확인

### 12.2 성능 — 토큰 예산 관리

| 항목 | 비용 | 최적화 |
|---|---|---|
| 메타데이터 | Skill당 ~100 토큰 × 항상 | description 간결하게, 안 쓰는 Skill은 끄기 |
| SKILL.md 본문 | 트리거 시 전부 | 500줄 이하, 일반론 제거 |
| reference | 읽을 때 | 도메인별 분할, 목차 |
| 스크립트 | **출력만** | 출력 요약·제한 (`TOP_N`, `--max-lines`) |
| 동적 주입 `!cmd` | 출력 전부, 매 호출 | `| head`, `--stat` 등으로 축소 |

> [!tip] 가장 큰 효과를 내는 최적화
> "Claude가 읽고 계산하던 것"을 "스크립트가 계산하고 결과만 출력"하도록 바꾸는 것. 로그 10MB를 읽게 하지 말고, 스크립트가 요약 30줄을 출력하게 하세요.

### 12.3 운영 — Skill 라이프사이클

```mermaid
stateDiagram-v2
    [*] --> Draft: 반복 작업 발견
    Draft --> Eval: 시나리오 작성
    Eval --> Draft: 실패
    Eval --> Published: 통과
    Published --> Monitoring: 사용
    Monitoring --> Draft: 실패 사례 / 요구 변경
    Monitoring --> Deprecated: 사용 빈도↓ (/skill-doctor)
    Deprecated --> [*]
```

- **언제 Skill을 만드나?** 같은 지시를 **3번 이상** 반복했을 때
- 버전은 semver로, CHANGELOG 유지
- 정기적으로 `/skill-doctor`로 비용/사용량 점검


---

# 🏁 마무리

## Part 13. 캡스톤 프로젝트 — 카메라 로그 분석 Skill

지금까지 배운 모든 것을 하나의 프로덕션급 Skill에 적용합니다.

> [!abstract] 요구사항
> VMS/NVR 로그 파일을 받아서
> 1. 장비별·레벨별·컴포넌트별 에러를 집계하고
> 2. 오프라인/재연결 패턴과 시간대 분포를 찾고
> 3. **자격 증명을 마스킹**한 채로
> 4. 사람이 읽을 보고서(Markdown) 또는 다른 Skill이 소비할 JSON으로 출력한다.

### 13.1 설계 결정

| 결정 | 선택 | 이유 (배운 원칙) |
|---|---|---|
| 파싱 | 스크립트 | 결정론 + 대용량 로그 토큰 절약 ([[AI technique/skills/Claude-Skills-완전정복-강좌#4.3 scripts — 결정론적 작업은 코드로\|4.3]]) |
| 원인 해석 | Claude + reference | 맥락 판단이 필요 → 높은 자유도 ([[AI technique/skills/Claude-Skills-완전정복-강좌#7.1 자유도(Degrees of Freedom) 설계\|7.1]]) |
| 에러 코드 사전 | `references/error-codes.md` | 필요할 때만 로드 ([[AI technique/skills/Claude-Skills-완전정복-강좌#4.2 references — 필요할 때만 읽히는 문서\|4.2]]) |
| 출력 | `--format md|json` | 조합성 — xlsx Skill이 JSON 소비 ([[AI technique/skills/Claude-Skills-완전정복-강좌#7.7 Skill 조합 (Composability)\|7.7]]) |
| 의존성 | 표준 라이브러리만 | API 환경 호환 ([[AI technique/skills/Claude-Skills-완전정복-강좌#9.4 커스텀 Skill 업로드 & 버전 관리\|9.4]]) |
| 보안 | 스크립트에서 마스킹 | 출력이 컨텍스트로 들어가므로 ([[AI technique/skills/Claude-Skills-완전정복-강좌#12.1 보안 — Skill은 "소프트웨어 설치"다\|12.1]]) |

### 13.2 디렉터리 구조

```text
analyzing-camera-logs/
├── SKILL.md
├── references/
│   └── error-codes.md
├── scripts/
│   └── analyze_logs.py
└── evals/
    ├── fixtures/sample.log
    └── cases.json
```

### 13.3 SKILL.md

````markdown
---
name: analyzing-camera-logs
description: >-
  Analyzes VMS, NVR, and IP camera log files to find errors, disconnections,
  and RTSP/ONVIF failures, summarizing them by device, component, and hour.
  Use when the user shares .log files from cameras or VMS servers, asks why a
  camera went offline, or says "카메라 로그 분석해줘". Do not use for
  application crash dumps or non-log data files.
---

# Analyzing Camera Logs

## Quick start
```bash
python ${CLAUDE_SKILL_DIR}/scripts/analyze_logs.py <logfile> --format md
```
로그를 직접 읽거나 파싱 코드를 새로 작성하지 말고, **반드시 이 스크립트를 실행**한다.
여러 파일이면 파일 경로를 공백으로 나열한다.

## Workflow
1. 스크립트를 `--format md` 로 실행한다.
2. `Unparsed lines` 가 전체의 10%를 넘으면 사용자에게 로그 형식 샘플 3줄을 보여주고 형식이 맞는지 확인한다.
3. 에러 코드나 컴포넌트 의미가 불분명하면 [references/error-codes.md](references/error-codes.md)를 읽는다.
4. 아래 형식으로 보고한다.

## Report format
1. **한 줄 결론** — 가장 심각한 문제와 영향받는 장비
2. **스크립트 요약 표** (그대로 붙인다)
3. **원인 추정** — 장비별 1~2문장, 근거가 된 로그 패턴 명시
4. **권장 조치** — 우선순위 순 최대 5개

## Rules
- 스크립트가 마스킹한 값을 복원하거나 원본 로그의 자격 증명을 인용하지 않는다.
- 사용자가 엑셀/표 파일을 원하면 `--format json` 결과를 다른 Skill(xlsx 등)에 넘긴다.
- 추정과 사실을 구분한다 ("로그상 확인됨" vs "추정").
````

### 13.4 scripts/analyze_logs.py

```python
#!/usr/bin/env python3
"""Summarize VMS/camera logs.

Expected line format (one event per line):
  <ISO-8601 timestamp> <DEVICE-ID> <LEVEL> [<component>] <message>
Example:
  2026-09-12T08:01:13+09:00 CAM-07 ERROR [rtsp] RTSP timeout after 10s

Usage: analyze_logs.py <logfile> [<logfile> ...] [--format md|json] [--top N]
"""
import argparse
import json
import re
import sys
from collections import Counter, defaultdict

LINE_RE = re.compile(
    r"^(?P<ts>\d{4}-\d{2}-\d{2}T(?P<hour>\d{2}):\d{2}:\d{2}\S*)\s+"
    r"(?P<device>\S+)\s+(?P<level>DEBUG|INFO|WARN|WARNING|ERROR|FATAL)\s+"
    r"\[(?P<component>[^\]]+)\]\s+(?P<msg>.*)$"
)
# rtsp://user:pass@host, password=..., pwd=... 를 마스킹
SECRET_RES = [
    (re.compile(r"(\w+://)[^/\s:@]+:[^/\s@]+@"), r"\1***:***@"),
    (re.compile(r"(?i)\b(password|passwd|pwd|token)=\S+"), r"\1=***"),
]
ERROR_LEVELS = {"ERROR", "FATAL"}
OFFLINE_RE = re.compile(r"(?i)\b(offline|disconnect(ed)?|connection lost)\b")
RECOVER_RE = re.compile(r"(?i)\b(online|reconnect(ed)?|recovered)\b")
SAMPLE_PER_DEVICE = 2  # 장비당 대표 메시지 2개면 원인 추정에 충분, 더 많으면 토큰 낭비


def mask(text):
    for pattern, repl in SECRET_RES:
        text = pattern.sub(repl, text)
    return text


def normalize(msg):
    """숫자를 '#'로 치환해 같은 유형의 메시지를 묶는다."""
    return re.sub(r"\d+", "#", msg)[:120]


def analyze(paths):
    total = unparsed = 0
    levels, components, hours = Counter(), Counter(), Counter()
    dev_errors, offline, recover = Counter(), Counter(), Counter()
    patterns = Counter()
    samples = defaultdict(list)
    for path in paths:
        try:
            fh = open(path, encoding="utf-8", errors="replace")
        except FileNotFoundError:
            raise SystemExit(f"ERROR: file not found: {path}")
        with fh:
            for raw in fh:
                line = raw.strip()
                if not line:
                    continue
                total += 1
                m = LINE_RE.match(line)
                if not m:
                    unparsed += 1
                    continue
                level = "WARN" if m["level"] == "WARNING" else m["level"]
                msg = mask(m["msg"])
                levels[level] += 1
                if level in ERROR_LEVELS:
                    dev, comp = m["device"], m["component"]
                    dev_errors[dev] += 1
                    components[comp] += 1
                    hours[m["hour"]] += 1
                    patterns[normalize(f"[{comp}] {msg}")] += 1
                    if len(samples[dev]) < SAMPLE_PER_DEVICE:
                        samples[dev].append(f"{m['ts']} [{comp}] {msg}")
                if OFFLINE_RE.search(msg) and not RECOVER_RE.search(msg):
                    offline[m["device"]] += 1
                elif RECOVER_RE.search(msg):
                    recover[m["device"]] += 1
    return {
        "total_lines": total,
        "unparsed_lines": unparsed,
        "levels": dict(levels),
        "errors_by_device": dict(dev_errors.most_common()),
        "errors_by_component": dict(components.most_common()),
        "errors_by_hour": dict(sorted(hours.items())),
        "offline_events": dict(offline.most_common()),
        "recover_events": dict(recover.most_common()),
        "top_patterns": patterns.most_common(),
        "samples": dict(samples),
    }


def to_markdown(r, top):
    out = ["## Log summary", ""]
    pct = (r["unparsed_lines"] / r["total_lines"] * 100) if r["total_lines"] else 0
    out.append(f"- Total lines: {r['total_lines']}  |  Unparsed lines: "
               f"{r['unparsed_lines']} ({pct:.1f}%)")
    out.append("- Levels: " + ", ".join(f"{k}={v}" for k, v in sorted(r["levels"].items())))
    out += ["", "| Device | Errors | Offline | Recovered |", "|---|---|---|---|"]
    devices = list(r["errors_by_device"])
    devices += [d for d in r["offline_events"] if d not in devices]
    for d in devices[:top]:
        out.append(f"| {d} | {r['errors_by_device'].get(d, 0)} | "
                   f"{r['offline_events'].get(d, 0)} | {r['recover_events'].get(d, 0)} |")
    out += ["", "| Component | Errors |", "|---|---|"]
    out += [f"| {c} | {n} |" for c, n in list(r["errors_by_component"].items())[:top]]
    out += ["", "Errors by hour: " + (", ".join(
        f"{h}h={n}" for h, n in r["errors_by_hour"].items()) or "none")]
    out += ["", "### Top error patterns"]
    out += [f"{i}. ({n}x) `{p}`" for i, (p, n) in enumerate(r["top_patterns"][:top], 1)]
    out += ["", "### Samples (masked)"]
    for d, lines in r["samples"].items():
        out += [f"- **{d}**"] + [f"  - `{s}`" for s in lines]
    return "\n".join(out)


def main():
    ap = argparse.ArgumentParser(description=__doc__.splitlines()[0])
    ap.add_argument("files", nargs="+")
    ap.add_argument("--format", choices=("md", "json"), default="md")
    ap.add_argument("--top", type=int, default=10,
                    help="rows per table (10 keeps output small for the context)")
    args = ap.parse_args()
    result = analyze(args.files)
    if result["total_lines"] == 0:
        print("ERROR: no log lines found. Check that the file is not empty.")
        return 1
    if args.format == "json":
        result["top_patterns"] = result["top_patterns"][:args.top]
        print(json.dumps(result, ensure_ascii=False, indent=2))
    else:
        print(to_markdown(result, args.top))
    return 0


if __name__ == "__main__":
    sys.exit(main())
```

### 13.5 references/error-codes.md (예시)

```markdown
# Error code & component reference

## Contents
- Components
- Common patterns and likely causes

## Components
| component | 의미 |
|---|---|
| rtsp | 스트림 수신 (RTSP/RTP) |
| onvif | 장비 제어/이벤트 (ONVIF SOAP) |
| rec | 녹화 엔진, 디스크 쓰기 |
| net | 네트워크 링크 상태 |

## Common patterns and likely causes
| 패턴 | 가능 원인 | 확인 방법 |
|---|---|---|
| `RTSP timeout` 반복 + 같은 시간대 다수 장비 | 스위치/업링크 대역폭 포화 | 같은 시간대 net 로그, 스위치 포트 통계 |
| `RTSP timeout` 단일 장비 반복 | 카메라 과부하, PoE 전력 부족 | 카메라 CPU, PoE 예산 |
| `401 Unauthorized` (onvif) | 비밀번호 변경/잠금 | 장비 계정 상태 |
| `disk write latency` (rec) | 디스크 노화, RAID 리빌드 | SMART, RAID 상태 |
```

### 13.6 테스트 로그와 실행 결과

**evals/fixtures/sample.log**

```text
2026-09-12T08:00:01+09:00 CAM-01 INFO [rtsp] stream started rtsp://admin:Secret123@10.0.0.1/stream1
2026-09-12T08:01:13+09:00 CAM-07 ERROR [rtsp] RTSP timeout after 10s
2026-09-12T08:01:20+09:00 CAM-07 WARN [net] connection lost, retry 1
2026-09-12T08:01:45+09:00 CAM-07 INFO [net] reconnected
2026-09-12T08:15:02+09:00 CAM-07 ERROR [rtsp] RTSP timeout after 10s
2026-09-12T09:02:10+09:00 CAM-03 ERROR [onvif] 401 Unauthorized password=hunter2
2026-09-12T09:30:00+09:00 NVR-01 ERROR [rec] disk write latency 850ms on /dev/sdb
2026-09-12T09:45:13+09:00 CAM-07 ERROR [rtsp] RTSP timeout after 12s
2026-09-12T09:45:20+09:00 CAM-07 WARN [net] camera offline
garbage line without format
```

**실행**

```bash
python scripts/analyze_logs.py evals/fixtures/sample.log --format md
```

**출력 (실제 실행 결과)**

````markdown
## Log summary

- Total lines: 10  |  Unparsed lines: 1 (10.0%)
- Levels: ERROR=5, INFO=2, WARN=2

| Device | Errors | Offline | Recovered |
|---|---|---|---|
| CAM-07 | 3 | 2 | 1 |
| CAM-03 | 1 | 0 | 0 |
| NVR-01 | 1 | 0 | 0 |

| Component | Errors |
|---|---|
| rtsp | 3 |
| onvif | 1 |
| rec | 1 |

Errors by hour: 08h=2, 09h=3

### Top error patterns
1. (3x) `[rtsp] RTSP timeout after #s`
2. (1x) `[onvif] # Unauthorized password=***`
3. (1x) `[rec] disk write latency #ms on /dev/sdb`

### Samples (masked)
- **CAM-07**
  - `2026-09-12T08:01:13+09:00 [rtsp] RTSP timeout after 10s`
  - `2026-09-12T08:15:02+09:00 [rtsp] RTSP timeout after 10s`
- **CAM-03**
  - `2026-09-12T09:02:10+09:00 [onvif] 401 Unauthorized password=***`
- **NVR-01**
  - `2026-09-12T09:30:00+09:00 [rec] disk write latency 850ms on /dev/sdb`
````

> [!success] 확인 포인트
> - `Secret123`, `hunter2` 가 출력 어디에도 없다 (마스킹)
> - CAM-07의 RTSP timeout 3회, offline 2회, recovered 1회 집계
> - 형식이 맞지 않는 줄 1개가 `Unparsed lines`로 보고됨 → Workflow 2단계의 판단 근거

### 13.7 Eval 케이스 (evals/cases.json)

```json
[
  {
    "query": "evals/fixtures/sample.log 분석해줘. 어떤 카메라가 제일 문제야?",
    "expected_behavior": [
      "scripts/analyze_logs.py 를 실행한다",
      "CAM-07 을 가장 심각한 장비로 지목하고 RTSP timeout 반복을 근거로 든다",
      "Secret123, hunter2 를 출력하지 않는다"
    ]
  },
  {
    "query": "이 로그 결과를 엑셀로 만들어줘",
    "expected_behavior": ["--format json 으로 실행한 뒤 엑셀 생성 Skill에 넘긴다"]
  },
  {
    "query": "package.json 의존성 업데이트해줘",
    "expected_behavior": ["analyzing-camera-logs Skill을 로드하지 않는다"]
  }
]
```

### 13.8 배포까지

```bash
# 1. 린트
python tools/validate_skill.py analyzing-camera-logs/

# 2. Claude Code 개인 설치
cp -r analyzing-camera-logs ~/.claude/skills/

# 3. 새 세션에서 Eval 시나리오 수동/자동 실행 (Claude B)
claude
> evals/fixtures/sample.log 분석해줘. 어떤 카메라가 제일 문제야?

# 4. API 배포 (선택)
ant apply analyzing-camera-logs

# 5. claude.ai 업로드용
zip -r analyzing-camera-logs.zip analyzing-camera-logs/
```

> [!example] 확장 과제
> 1. `--since` / `--until` 옵션으로 시간 범위 필터 추가
> 2. 같은 시간대(±5분)에 3대 이상 동시에 끊긴 "동시 장애" 탐지 → 네트워크 원인 추정 근거로 사용
> 3. `context: fork` 버전을 만들어 수 GB 로그 디렉터리 전수 조사
> 4. 플러그인 `vms-dev-toolkit`에 포함해 팀 배포

---

## Part 14. 트러블슈팅

| 증상 | 원인 | 해결 |
|---|---|---|
| Skill이 **전혀 트리거되지 않음** | description이 모호 / 키워드 부족 | What + When + 실제 사용 단어 추가, `when_to_use` 활용 |
| frontmatter가 **무시됨** | 첫 줄이 `---`가 아님 (BOM, 빈 줄), YAML 문법 오류 | 첫 줄 확인, 따옴표/콜론 이스케이프, YAML 린터 |
| 필드가 안 먹힘 | 필드명 오타 (`allowed_tools` vs `allowed-tools`) | Claude Code는 모르는 필드를 **조용히 무시** → 레퍼런스와 대조 |
| `/` 메뉴에 안 보임 | `user-invocable: false`, 이름에 금지 문자 | 설정 확인, `claude --debug` 로그 확인 |
| 하위 폴더 Skill이 안 보임 | Nested Skill은 해당 디렉터리 파일 접근 시 로드 | 그 디렉터리 파일을 열거나 `/add-dir` |
| 새 skills 폴더가 인식 안 됨 | 최상위 디렉터리 신규 생성 | `/reload-skills` |
| 엉뚱한 작업에서 트리거됨 | description이 너무 넓음 | 경계 조건("Do not use for…"), `paths` 로 범위 제한 |
| 스크립트 대신 코드를 새로 짬 | "실행하라" 지시가 약함 | "직접 파싱하지 말고 **반드시** 이 스크립트를 실행한다" |
| 스크립트 경로를 못 찾음 | 상대 경로가 작업 디렉터리 기준 | `${CLAUDE_SKILL_DIR}/scripts/...` |
| `!cmd` 때문에 Skill 호출 실패 | 명령이 non-zero 종료 | `|| true` 추가 |
| API에서 패키지 import 실패 | 런타임 설치 불가 | 표준 라이브러리 / 사전 설치 패키지만 사용 |
| 중간에 지침을 안 따름 | 본문이 너무 길어 핵심이 묻힘 | 500줄 이하, 핵심 규칙을 상단에, 체크리스트화 |
| `anthropic-skills` 이름 Skill이 로드 안 됨 | 예약된 이름 (claude.ai 동기화용) | 다른 이름 사용 |

---

## 부록 A. 연습문제와 해답

> [!question] 문제 1 (초급)
> CLAUDE.md에 넣어야 할 것과 Skill로 만들어야 할 것을 구분하세요.
> (a) `npm run build`로 빌드한다 (b) 분기별 투자자 보고서 작성 절차 (c) 들여쓰기는 2칸 (d) ONVIF 이벤트 구독 디버깅 절차
> > [!success]- 해답
> > CLAUDE.md: (a), (c) — 모든 작업에 항상 필요한 상식
> > Skill: (b), (d) — 특정 작업에서만 필요한 절차 지식

> [!question] 문제 2 (초급)
> 다음 frontmatter의 문제점을 모두 찾으세요.
> ```yaml
> name: Claude_PDF_Tool
> description: I can help you with PDFs.
> ```
> > [!success]- 해답
> > 1. 대문자·언더스코어 사용 → 소문자-하이픈만
> > 2. 예약어 `claude` 포함
> > 3. description이 1인칭
> > 4. "언제 쓰는지"가 없음, 구체적 기능/키워드 없음
> > 수정: `name: processing-pdfs` / `description: Extracts text and tables from PDF files and fills PDF forms. Use when working with .pdf files or when the user mentions PDFs or forms.`

> [!question] 문제 3 (중급)
> `/deploy` Skill을 만들었는데, Claude가 "코드 고쳤으니 배포도 해둘게요"라며 자동 실행했습니다. 무엇을 추가해야 하나요?
> > [!success]- 해답
> > `disable-model-invocation: true`. 추가로 `prod` 환경일 때 사용자 재확인 규칙, `allowed-tools`는 최소 범위로.

> [!question] 문제 4 (중급)
> 2,000줄짜리 API 레퍼런스를 SKILL.md에 통째로 넣었더니 응답 품질이 떨어졌습니다. 어떻게 재구성하나요?
> > [!success]- 해답
> > SKILL.md는 개요 + 워크플로 + 가장 흔한 3~5개 사용 예시(500줄 이하)로 줄이고, 레퍼런스는 도메인별(`references/auth.md`, `references/streams.md` …)로 나눠 **SKILL.md에서 직접 링크**(1단계 깊이). 각 reference 파일 상단에 목차.

> [!question] 문제 5 (고급)
> 사내 Skill 20개를 Claude Code, claude.ai, API 세 환경에 일관되게 배포하고, 프로덕션 앱의 동작이 예기치 않게 바뀌지 않도록 하려면?
> > [!success]- 해답
> > git 저장소를 단일 원본으로 두고 CI에서 ①`validate_skill.py` 린트 ②Eval 실행 ③통과 시 Plugin(Claude Code) / `ant apply`(API) / zip(claude.ai) 산출. API 프로덕션 앱은 `version: "latest"` 대신 **특정 `skver_...` 고정**, 새 버전은 Eval 통과 후 명시적으로 교체.

> [!question] 문제 6 (고급)
> 코드베이스 전체 보안 감사 Skill을 만들려 합니다. 메인 대화 컨텍스트를 보호하고, 감사 중 실수로 파일이 수정되지 않게 하려면 어떤 필드를 쓰나요?
> > [!success]- 해답
> > `context: fork` + `agent: Explore`(읽기 전용 탐색 에이전트)로 별도 컨텍스트에서 실행하고 요약만 반환. 추가로 `disallowed-tools: Write Edit NotebookEdit`.

---

## 부록 B. 치트시트

### 최소 Skill

```markdown
---
name: doing-something
description: Does X for Y. Use when the user asks for Z or mentions "키워드".
---
# Doing Something
1. ...
```

### 위치

| 범위 | 경로 |
|---|---|
| 개인 | `~/.claude/skills/<name>/SKILL.md` |
| 프로젝트 | `.claude/skills/<name>/SKILL.md` |
| 하위 디렉터리 | `<subdir>/.claude/skills/<name>/SKILL.md` |
| 플러그인 | `<plugin>/skills/<name>/SKILL.md` → `/plugin:name` |

### 자주 쓰는 Claude Code 필드

```yaml
disable-model-invocation: true      # 사용자만 호출 (부작용 작업)
user-invocable: false               # Claude만 호출 (배경 지식)
argument-hint: "[file]"             # 자동완성 힌트
arguments: [service, env]           # $service, $env
allowed-tools: Bash(git *)          # 승인 없이 허용
disallowed-tools: Write Edit        # 도구 제거
context: fork                       # 서브에이전트 실행
agent: Explore
paths: ["**/*.proto"]               # 파일 패턴 한정
```

### 치환 변수

`$ARGUMENTS` · `$0 $1` · `$name` · `${CLAUDE_SKILL_DIR}` · `${CLAUDE_PROJECT_DIR}` · `${CLAUDE_SESSION_ID}` · `${CLAUDE_PLUGIN_ROOT}` · `` !`cmd` ``

### API 한 장 요약

```python
client.messages.create(
    model=..., max_tokens=...,
    container={"skills": [{"type": "anthropic"|"custom", "skill_id": ..., "version": ...}]},  # ≤ 20
    tools=[{"type": "code_execution_20250825", "name": "code_execution"}],
    messages=[...],
)
client.skills.create(display_title=..., files=files_from_dir(dir))
client.skills.versions.create(skill_id=..., files=files_from_dir(dir))
client.files.download(file_id=...)
```

### 작성 전 최종 체크리스트

- [ ] description: 3인칭, What + When, 트리거 키워드, 경계 조건
- [ ] name: 소문자-하이픈, 64자 이하, 예약어 없음, 폴더명과 일치
- [ ] SKILL.md 본문 500줄 이하, 일반론 없음, 기본값 하나
- [ ] reference는 1단계 깊이, 100줄 넘으면 목차
- [ ] 결정론적 작업은 스크립트, 에러 메시지는 구체적, 상수에 이유 주석
- [ ] 검증 루프 (validate → fix → repeat)
- [ ] 경로는 `/`, 스크립트는 `${CLAUDE_SKILL_DIR}` 기준
- [ ] 부작용 있으면 `disable-model-invocation: true`
- [ ] 비밀 값 없음, 출력 마스킹
- [ ] Eval 3개 이상 (positive + negative 트리거 포함)
- [ ] 사용할 모든 모델(Haiku/Sonnet/Opus)에서 테스트

### 고급 사용자 로드맵 — 다음 단계

```mermaid
mindmap
  root((Claude 고급 사용자))
    Skills
      Eval 자동화
      사내 Marketplace
      버전 고정 운영
    MCP
      사내 시스템 연결
      MCP + Skill 조합
    Subagents
      역할별 에이전트 정의
      context fork
    Hooks
      자동 린트/포맷
      위험 명령 차단
    Agent SDK
      Skill 내장 커스텀 에이전트
      CI 자동화
```

---

## 부록 C. 참고 자료

- [Agent Skills 개요 (Claude Platform Docs)](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/)
- [Skill 작성 Best Practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices)
- [Skills API 가이드](https://platform.claude.com/docs/en/build-with-claude/skills-guide)
- [Claude Code Skills 레퍼런스](https://code.claude.com/docs/en/skills)

> [!info] 관련 노트 (Obsidian)
> 이 강좌와 연결해 두면 좋은 노트: [[Claude Code 기본 사용법\|Claude Code 기본 사용법]] · [[MCP 서버 개발\|MCP 서버 개발]] · [[Claude Agent SDK\|Claude Agent SDK]] · [[Prompt Engineering\|Prompt Engineering]]
> 

#claude/skills #ai/agent #tutorial
