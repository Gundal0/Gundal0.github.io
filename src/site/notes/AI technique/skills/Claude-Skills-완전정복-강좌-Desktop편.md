---
{"dg-publish":true,"permalink":"/ai-technique/skills/claude-skills-desktop/","title":"Claude Skills 완전 정복 — Claude Desktop 편","tags":["claude/skills","claude/desktop","claude/cowork","tutorial"],"dg-note-properties":{"title":"Claude Skills 완전 정복 — Claude Desktop 편","aliases":["Claude Skills 강좌 (Desktop)","Claude Desktop Skills 튜토리얼"],"tags":["claude/skills","claude/desktop","claude/cowork","tutorial"],"level":"초급 → 중급 → 고급","audience":"개발자 (Claude Desktop 사용자)","created":"2026-10-19","status":"complete"}}
---


# Claude Skills 완전 정복 — Claude Desktop 편

> [!abstract] 이 강좌로 얻는 것
> - Skill이 **무엇이고 왜 필요하며, Claude가 어떻게 불러오는지** 정확히 이해합니다.
> - **Claude Desktop**의 Chat · Cowork · Code 세 탭에서 Skill을 **만들고, 켜고, 호출하고, 공유**합니다.
> - 스크립트·검증 루프·커넥터(MCP)·플러그인·평가(Eval)까지 **고급 패턴**을 실전 예제로 익힙니다.
> - 캡스톤 프로젝트를 끝내면 팀에서 Skill을 설계하고 배포하는 사람이 됩니다.

> [!info] 기준 시점과 범위
> - **2026년 10월** 공식 문서 기준입니다. 메뉴 이름은 앱 업데이트로 바뀔 수 있습니다.
> - 이 문서는 **Claude Desktop 앱** 사용자를 위한 버전입니다. 터미널(Claude Code CLI)이나 API 중심 내용은 [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#부록 D. 개발자 확장 — Code 탭, CLI, API\|부록 D]]에 따로 정리했습니다.
> - UI 경로는 `Customize > Skills`처럼 **굵은 메뉴 > 하위 메뉴** 형식으로 표기합니다.

---

## 목차

- [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#Part 0. 학습 로드맵과 Claude Desktop 구조\|#Part 0. 학습 로드맵과 Claude Desktop 구조]]
- **🟢 초급**
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#Part 1. 개념 — Skill이란 무엇인가\|#Part 1. 개념 — Skill이란 무엇인가]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#Part 2. 준비 — Desktop에서 Skills 켜고 써 보기\|#Part 2. 준비 — Desktop에서 Skills 켜고 써 보기]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#Part 3. 첫 번째 Skill 만들기 — 세 가지 방법\|#Part 3. 첫 번째 Skill 만들기 — 세 가지 방법]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#Part 4. SKILL.md 해부학\|#Part 4. SKILL.md 해부학]]
- **🟡 중급**
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#Part 5. 파일 번들링 — references, scripts, assets\|#Part 5. 파일 번들링 — references, scripts, assets]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#Part 6. 탭별 동작 차이 — Chat · Cowork · Code\|#Part 6. 탭별 동작 차이 — Chat · Cowork · Code]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#Part 7. 실전 예제 4종\|#Part 7. 실전 예제 4종]]
- **🔴 고급**
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#Part 8. 고급 설계 패턴\|#Part 8. 고급 설계 패턴]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#Part 9. Cowork에서 Skill 200% 활용하기\|#Part 9. Cowork에서 Skill 200% 활용하기]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#Part 10. 플러그인 — Skill 묶어서 배포하기\|#Part 10. 플러그인 — Skill 묶어서 배포하기]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#Part 11. 공유와 조직 배포\|#Part 11. 공유와 조직 배포]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#Part 12. 평가 주도 개발 (Eval)\|#Part 12. 평가 주도 개발 (Eval)]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#Part 13. 보안과 운영\|#Part 13. 보안과 운영]]
- **🏁 마무리**
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#Part 14. 캡스톤 — 카메라 로그 분석 Skill\|#Part 14. 캡스톤 — 카메라 로그 분석 Skill]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#Part 15. 트러블슈팅\|#Part 15. 트러블슈팅]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#부록 A. 연습문제와 해답\|#부록 A. 연습문제와 해답]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#부록 B. 치트시트\|#부록 B. 치트시트]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#부록 C. 참고 자료\|#부록 C. 참고 자료]]
  - [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#부록 D. 개발자 확장 — Code 탭, CLI, API\|#부록 D. 개발자 확장 — Code 탭, CLI, API]]

---

## Part 0. 학습 로드맵과 Claude Desktop 구조

### 0.1 로드맵

```mermaid
flowchart LR
    A[개념<br/>Part 1] --> B[Desktop 준비<br/>Part 2]
    B --> C[첫 Skill<br/>Part 3]
    C --> D[SKILL.md 해부<br/>Part 4]
    D --> E[파일 번들링<br/>Part 5]
    E --> F[탭별 차이<br/>Part 6]
    F --> G[실전 예제<br/>Part 7]
    G --> H[고급 패턴 / Cowork<br/>Part 8~9]
    H --> I[플러그인 / 공유<br/>Part 10~11]
    I --> J[Eval / 보안<br/>Part 12~13]
    J --> K((캡스톤<br/>Part 14))
```

| 단계 | 목표 | 예상 소요 |
|---|---|---|
| 초급 (Part 1~4) | 개념 이해, Desktop에서 첫 Skill 업로드·실행 | 1~2시간 |
| 중급 (Part 5~7) | 스크립트·참조 파일이 있는 실무형 Skill, 탭별 차이 이해 | 3~4시간 |
| 고급 (Part 8~13) | 검증 루프, Cowork, 플러그인, 조직 배포, Eval, 보안 | 4~6시간 |
| 캡스톤 (Part 14) | 하나의 Skill을 설계 → 테스트 → 배포까지 | 2~3시간 |

### 0.2 Claude Desktop 한눈에 보기

Claude Desktop에는 성격이 다른 **세 개의 작업 공간(탭)** 이 있고, Skill은 세 곳 모두에서 동작합니다.

```mermaid
flowchart TB
    subgraph Desktop["Claude Desktop 앱"]
        direction LR
        Chat["💬 Chat<br/>일반 대화<br/>클라우드 샌드박스에서 코드 실행"]
        Cowork["🤝 Cowork<br/>에이전트형 작업 공간<br/>내 컴퓨터 폴더 직접 읽기/쓰기"]
        Code["👩‍💻 Code<br/>Claude Code (코딩 에이전트)"]
    end
    Customize["⚙️ Customize (사이드바)<br/>Skills · Connectors · Plugins"]
    Customize -- "계정에 저장된 Skill 동기화" --> Chat & Cowork & Code
```

| 탭 | 한 줄 설명 | Skill 관점 핵심 |
|---|---|---|
| **Chat** | 웹 claude.ai와 같은 대화 | 업로드한 Skill이 클라우드 샌드박스에 복사되어 실행 |
| **Cowork** | Claude Code와 같은 에이전트 구조를 터미널 없이 쓰는 작업 공간 | 로컬 폴더 접근, 서브에이전트, 플러그인의 agents/hooks까지 동작 |
| **Code** | Claude Code (데스크톱 탭) | Claude Code 전용 frontmatter 필드까지 전부 동작 |

> [!important] 모든 Skill 관리는 `Customize`에서
> 사이드바의 **Customize**에 **Skills / Connectors / Plugins** 탭이 있습니다. 여기서 켠 Skill은 **계정에 붙어** Chat·Cowork·Code 탭 모두에서 쓸 수 있습니다.
> (구버전 앱에서는 `Settings > Capabilities > Skills`에 있었습니다.)

> [!tip] 실습 준비물
> - Claude **Pro / Max / Team / Enterprise** 플랜 (Skills는 유료 플랜 기능)
> - Claude Desktop 최신 버전
> - 실습 폴더 하나 (예: `~/claude-skills-lab`) — Cowork에서 연결해 사용
> - (선택) Python 3.10+ — 스크립트 예제를 로컬에서 직접 돌려볼 때

---

# 🟢 초급

## Part 1. 개념 — Skill이란 무엇인가

### 1.1 한 문장 정의

> [!quote] 정의
> **Skill = Claude가 필요할 때 스스로 꺼내 쓰는 "업무 매뉴얼 폴더"**
> `SKILL.md`(지침) 파일 하나와, 필요하면 스크립트·참조 문서·템플릿을 담은 **폴더**입니다. Claude는 요청이 Skill의 설명과 맞을 때만 그 내용을 불러옵니다.

개발자 비유:

| 개발 개념 | Skill에서의 대응 |
|---|---|
| 라이브러리 `README` + `docs/` | `SKILL.md` + `references/` |
| CLI 유틸리티 (`bin/`) | `scripts/` |
| `package.json`의 name/description | YAML frontmatter |
| Lazy loading / 동적 import | Progressive Disclosure (단계적 로딩) |
| 패키지 매니저 / 확장 마켓 | Plugins + Directory(Discover) |

### 1.2 왜 필요한가

매번 이런 설명을 붙여 넣은 경험이 있을 겁니다.

```text
우리 팀 주간보고는 "요약 → 진행 현황 → 리스크 → 다음 주 계획" 순서고,
리스크는 상/중/하로 표시하고, 수치는 전주 대비 증감을 꼭 넣고…
```

| 문제 | Skill이 해결하는 방식 |
|---|---|
| 대화마다 반복 붙여넣기 | 한 번 만들어 두면 요청에 맞을 때 자동 로드 |
| 항상 넣어 두면 컨텍스트 낭비 | 평소엔 이름+설명만, 필요할 때만 본문 |
| 정확해야 하는 계산도 LLM이 매번 추론 | 스크립트로 고정해 결정론적으로 |
| 팀원마다 다른 버전의 프롬프트 | Share / Publish to org로 같은 Skill 공유 |

### 1.3 핵심 원리: Progressive Disclosure (단계적 로딩)

==이 개념 하나가 Skill 설계의 80%입니다.==

```mermaid
flowchart TB
    subgraph L1["① 알고만 있음 — 항상 (Skill당 ~100 토큰)"]
        M["name + description"]
    end
    subgraph L2["② 지침 로드 — 요청이 맞을 때"]
        B["SKILL.md 본문 (500줄 이하 권장)"]
    end
    subgraph L3["③ 필요한 파일만 — 단계가 요구할 때"]
        R["references/*.md (읽을 때 로드)"]
        S["scripts/*.py (실행 결과만 들어옴)"]
        A["assets/* (템플릿 등)"]
    end
    U[사용자 요청] --> M
    M -- "description과 일치" --> B
    B --> R & S & A
```

> [!important] 세 가지 핵심 통찰
> 1. Skill을 많이 켜 두어도 평소 비용은 **이름+설명** 정도입니다.
> 2. 스크립트는 **소스가 아니라 실행 결과만** 대화에 들어옵니다.
> 3. Claude가 Skill을 쓸지 말지 판단하는 근거는 **오직 `description`** 입니다. → [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#4.3 description 작성법 — 가장 중요한 한 줄\|Part 4.3]]

### 1.4 Desktop의 비슷한 기능과 비교 (가장 헷갈리는 부분)

| 기능 | 위치 | 로딩 시점 | 언제 쓰나 |
|---|---|---|---|
| **개인 설정(Preferences)** | Settings | **모든 대화**에 항상 | 말투, 언어 등 항상 적용할 선호 |
| **Projects** | 사이드바 Projects | 그 프로젝트 대화에 **항상** | 특정 주제의 배경 지식·문서 |
| **Skills** | Customize > Skills | 요청이 **맞을 때만** | 특정 작업의 절차·노하우·도구 |
| **Connectors (MCP)** | Customize > Connectors | 도구로 노출 | Jira, Slack, Drive 등 **외부 서비스 데이터·액션** |
| **Plugins** | Customize > Plugins | 설치 시 | Skill + 커넥터 + 명령 + 에이전트 **묶음** |

> [!tip] 기억법
> - **Connector = 손과 발** (외부 서비스에 닿는 능력)
> - **Skill = 노하우** (그 능력을 *어떻게* 쓰는지)
> - **Project / Preferences = 상식** (항상 알고 있어야 하는 것)
> - **Plugin = 상자** (위의 것들을 한 번에 배포)
>
> 예: Jira 커넥터는 "이슈를 만들 수 *있게*" 하고, `triaging-bugs` Skill은 "우리 팀 방식으로 버그를 분류하고 *어떤 프로젝트·라벨로* 이슈를 만드는지"를 알려줍니다.

> [!warning] Skill이 할 수 없는 것
> Skill은 **외부 서비스의 실시간 데이터에 직접 접근하지 못합니다.** 그건 커넥터의 일입니다. Skill은 커넥터를 *어떻게 쓸지* 알려줄 수 있을 뿐입니다.

### 1.5 Skill의 종류 (Desktop 기준)

`Customize > Skills > Your skills` 탭에서 출처별로 묶여 보입니다.

| 그룹 | 설명 |
|---|---|
| **From Anthropic & Partners** | Anthropic 기본 Skill(Excel, Word, PowerPoint, PDF 생성 등)과 파트너 Skill |
| **From your organization** | Team/Enterprise에서 관리자가 배포한 Skill |
| **Shared with you** | 동료가 공유한 Skill (직접 켜야 사용됨) |
| **Created by you** | 내가 만들거나 업로드한 Skill |

> [!note] 오픈 표준
> Skill 포맷은 **Agent Skills 사양(agentskills.io)** 이라는 오픈 표준을 따릅니다. 잘 만든 Skill은 Claude Code CLI나 이 표준을 지원하는 다른 도구에서도 그대로 쓸 수 있습니다.

### 1.6 Part 1 요약

- [x] Skill = `SKILL.md`가 들어 있는 폴더
- [x] 평소엔 이름+설명만, 필요할 때 본문, 더 필요할 때 부가 파일
- [x] 스크립트는 출력만 대화에 들어온다
- [x] 커넥터는 능력, Skill은 노하우, Project는 상시 배경 지식
- [x] Desktop에서는 `Customize`에서 관리하고 세 탭 모두에서 쓴다

---

## Part 2. 준비 — Desktop에서 Skills 켜고 써 보기

### 2.1 사전 조건: 코드 실행 켜기

Skill은 Claude의 코드 실행 환경(샌드박스)에서 동작하므로 **Code execution and file creation** 기능이 켜져 있어야 합니다.

| 플랜 | 설정 위치 |
|---|---|
| Pro / Max | `Settings > Capabilities` → **Code execution and file creation** 켜기 |
| Team | 조직 단위로 기본 활성화 (Owner가 끌 수 있음) |
| Enterprise | Owner가 `Organization settings`에서 코드 실행과 Skills를 먼저 활성화 |

> [!warning] Skill이 회색으로 비활성화되어 보인다면
> 개인 또는 조직 설정에서 코드 실행이나 Skills가 꺼져 있는 경우입니다. 회사 계정이면 관리자에게 문의하세요.

### 2.2 Customize 화면 투어

```text
사이드바 > Customize
├── Skills
│   ├── Your skills   ← 내가 가진 Skill (출처별 그룹)
│   └── Discover      ← 추가할 수 있는 Skill 디렉터리
├── Connectors
│   └── Discover      ← 서비스 연결 (Connect → 로그인)
└── Plugins
    ├── Yours / Shared with you / Your organization
    └── Discover      ← 플러그인 마켓
```

각 Skill 행에서 할 수 있는 것:

- **Turn on** 버튼 또는 Skill 페이지 상단의 스위치로 켜기/끄기
- Skill을 열어 `SKILL.md`와 포함된 파일 **미리보기**
- (Team/Enterprise) **Share**, **Publish to org**, 사용량(**Adoption / Activity / You**) 확인

### 2.3 실습 ① — 기본 Skill로 첫 경험

1. `Customize > Skills > Your skills`에서 **From Anthropic & Partners** 그룹의 Excel(xlsx) Skill이 켜져 있는지 확인
2. **Chat** 탭에서 새 대화 시작
3. 입력:

```text
카메라 50대의 월별 장애 건수를 기록하는 엑셀 템플릿을 만들어줘.
월별 합계와 전월 대비 증감률 수식을 넣어줘.
```

4. Claude가 Skill을 불러오고(사고 과정에 Skill을 읽는 단계가 보임) `.xlsx` 파일을 만들어 줍니다.

> [!success] 확인 포인트
> 요청에 "Skill을 써라"는 말이 없었는데도 Claude가 알아서 Excel Skill을 골랐습니다. 이것이 **description 기반 자동 선택**입니다.

### 2.4 실습 ② — Skill을 직접 지정해서 호출하기

자동 선택 말고 내가 고르고 싶을 때:

- 메시지 입력창에 **`/`** 를 입력 → 목록에서 Skill 선택
- 또는 문장으로 지정: "**pdf skill을 사용해서** 이 계약서의 표를 추출해줘"

### 2.5 실습 ③ — Discover에서 Skill 추가하기

1. `Customize > Skills` → **+** 버튼 → **Browse skills** (또는 **Discover** 탭)
2. 원하는 Skill에서 **Add**
3. 추가된 Skill은 기본으로 켜짐. 끄면 목록에는 남아 있다가 다시 켤 수 있음

> [!note] 디렉터리 Skill은 읽기 전용
> Discover에서 추가한 Skill은 수정할 수 없습니다. 고쳐 쓰고 싶다면 **복사본을 다운로드 → 수정 → 내 Skill로 업로드**하세요.

> [!danger] 켜기 전에 읽어 보세요
> 내가 업로드하거나 동료가 공유한 Skill은 **Anthropic이 검토하지 않습니다.** Skill의 지침과 스크립트는 대화 안에서 실행되므로, 켜기 전에 `SKILL.md`와 파일들을 열어 확인하는 습관을 들이세요. ([[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#Part 13. 보안과 운영\|Part 13]])

---

## Part 3. 첫 번째 Skill 만들기 — 세 가지 방법

| 방법 | 난이도 | 추천 상황 |
|---|---|---|
| **A. skill-creator와 대화로 만들기** | ⭐ | 처음 만들 때, 아이디어만 있을 때 |
| **B. 직접 작성 → ZIP 업로드** | ⭐⭐ | 구조를 정확히 통제하고 싶을 때 (개발자 추천) |
| **C. Cowork에서 로컬 폴더에 만들기 → 업로드** | ⭐⭐ | 스크립트를 로컬에서 테스트하며 만들 때 |

### 3.1 방법 A — skill-creator와 대화로 만들기

`skill-creator`는 Anthropic이 제공하는 "Skill을 만들어 주는 Skill"입니다.

1. `Customize > Skills`에서 **skill-creator**(From Anthropic)가 켜져 있는지 확인
2. Chat 또는 Cowork에서:

```text
skill-creator를 사용해서 Skill을 하나 만들고 싶어.
목적: 코드 설명 요청을 받으면 "한 줄 요약 → 비유 → ASCII 다이어그램 →
단계별 설명 → 주의할 점" 순서로 한국어로 설명하는 Skill.
```

3. Claude가 질문(언제 써야 하는지, 예시 입력/출력 등)을 하면 답합니다.
4. 결과로 Skill 파일(또는 ZIP)이 나오면 저장 버튼으로 내 계정에 추가하거나, 내려받아 **방법 B**의 업로드 절차로 올립니다.
5. **반드시 내용을 열어 읽고** 필요한 부분을 고칩니다.

> [!tip] 초안은 Claude, 품질은 나
> skill-creator가 만든 초안을 이 강좌 [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#Part 4. SKILL.md 해부학\|Part 4]]의 원칙(특히 description)으로 다듬으면 품질이 크게 올라갑니다.

### 3.2 방법 B — 직접 작성하고 ZIP으로 업로드 (개발자 추천)

**Step 1 — 폴더와 SKILL.md 만들기**

```text
explaining-code/          ← 폴더 이름 = name 필드 (반드시 일치!)
└── SKILL.md
```

```markdown
---
name: explaining-code
description: Explains code with a real-world analogy and an ASCII diagram, in Korean. Use when the user asks how code works, asks to explain a file or function, or says "이 코드 설명해줘".
---

# Explaining Code

코드를 설명할 때 항상 다음 순서를 따른다.

1. **한 줄 요약**: 이 코드가 하는 일을 한 문장으로.
2. **비유**: 일상생활의 비유 하나.
3. **ASCII 다이어그램**: 데이터/제어 흐름을 그린다.
4. **단계별 설명**: 핵심 로직을 순서대로.
5. **주의할 점**: 흔한 실수나 엣지 케이스 1~2개.

코드 식별자(함수명, 변수명)는 번역하지 않고 원문 그대로 둔다.
```

**Step 2 — ZIP으로 묶기 (가장 많이 실수하는 단계)**

ZIP 안의 **최상위 항목이 Skill 폴더**여야 합니다.

```text
✅ 올바른 구조                     ❌ 틀린 구조 (인식 안 됨)
explaining-code.zip               explaining-code.zip
└── explaining-code/              └── SKILL.md
    └── SKILL.md
```

macOS 터미널에서 **부모 폴더**에 서서:

```bash
cd ~/claude-skills-lab
zip -r explaining-code.zip explaining-code/
unzip -l explaining-code.zip      # 모든 항목이 explaining-code/ 로 시작하는지 확인
```

> [!tip] Finder로 압축할 때
> `SKILL.md` 파일이 아니라 **`explaining-code` 폴더 자체**를 우클릭 → "압축"하세요. 폴더 안 파일들을 선택해서 압축하면 틀린 구조가 됩니다.

**Step 3 — 업로드**

1. `Customize > Skills` → **+** (또는 **Add**) → **Upload skill**
2. ZIP 선택
3. **Created by you** 그룹에 나타나면 **Turn on**

**Step 4 — 테스트**

```text
(Chat 탭, 새 대화)
아래 함수가 어떻게 동작하는지 설명해줘.

def debounce(fn, wait):
    timer = None
    def wrapper(*args):
        nonlocal timer
        if timer: timer.cancel()
        timer = threading.Timer(wait, fn, args)
        timer.start()
    return wrapper
```

비유 → 다이어그램 → 단계별 설명 순서로 답하면 성공입니다. 사고 과정에서 `explaining-code` Skill을 읽는 단계가 보이는지도 확인하세요.

### 3.3 방법 C — Cowork에서 로컬 폴더에 만들기

Cowork는 **내 컴퓨터의 폴더를 직접 읽고 쓸 수 있으므로** Skill 개발 작업대로 쓰기 좋습니다.

1. **Cowork** 탭에서 새 작업 시작 → 실습 폴더(`~/claude-skills-lab`) 연결
2. 요청:

```text
~/claude-skills-lab 안에 explaining-code 라는 Skill 폴더를 만들어줘.
Agent Skills 사양에 맞게 SKILL.md를 작성하고,
업로드용 explaining-code.zip 도 올바른 구조로 만들어줘.
```

3. Claude가 폴더·파일·ZIP을 만들면 내용을 확인하고 **방법 B의 Step 3**으로 업로드합니다.

> [!important] Cowork는 `~/.claude/skills`를 읽지 않습니다
> 터미널용 Claude Code CLI는 `~/.claude/skills/` 폴더의 Skill을 읽지만, **Cowork와 Chat은 계정(Customize)에 등록된 Skill만 사용**합니다. 로컬 폴더에 만든 Skill은 **반드시 Customize에 업로드**해야 Cowork·Chat에서 쓸 수 있습니다.

### 3.4 Skill 디렉터리 구조

```text
explaining-code/
└── SKILL.md            ← 필수 (이것만 있어도 Skill)

# 실무형 Skill은 보통 이렇게 성장합니다
writing-weekly-report/
├── SKILL.md            ← 개요 + 절차 (500줄 이하)
├── references/
│   └── style-guide.md  ← 필요할 때만 읽는 상세 문서
├── scripts/
│   └── calc_delta.py   ← 실행만 하고 소스는 대화에 안 들어옴
└── assets/
    └── template.md     ← 채워 넣을 템플릿
```

---

## Part 4. SKILL.md 해부학

### 4.1 전체 구조

````markdown
---                                  ← 반드시 파일의 첫 줄
name: reviewing-pull-requests        ← 메타데이터 (①단계)
description: Reviews pull requests for ...
---

# Reviewing Pull Requests            ← 본문 (②단계)

## Workflow
...

## References
- 보안 체크리스트: `references/security.md`   ← ③단계
````

### 4.2 frontmatter 필수 규칙

| 필드 | 규칙 |
|---|---|
| `name` | 최대 **64자**, **소문자·숫자·하이픈만**, XML 태그 금지, **"anthropic", "claude" 포함 금지**, **폴더 이름과 일치** |
| `description` | 비어 있으면 안 됨, 최대 **1,024자**, XML 태그 금지, **무엇을 하는지 + 언제 쓰는지** |

```yaml
# ✅ 좋은 예
name: processing-pdfs
name: writing-weekly-reports
name: analyzing-camera-logs

# ❌ 나쁜 예
name: PDF_Helper        # 대문자, 언더스코어
name: claude-helper     # 예약어 포함
name: utils             # 너무 모호
```

> [!tip] 이름 짓기 관례
> 공식 권장은 **동명사(gerund) 형태**: `processing-pdfs`, `reviewing-code`, `writing-documentation`. 팀 안에서 일관성만 지키면 명사형(`pdf-processing`)도 괜찮습니다.

> [!warning] 업로드 실패 원인 Top 4
> 1. 폴더 이름과 `name` 불일치
> 2. `SKILL.md` 누락 또는 ZIP 구조 오류
> 3. `name`/`description`에 허용되지 않는 문자
> 4. ZIP 용량 초과

### 4.3 description 작성법 — 가장 중요한 한 줄

Claude는 켜진 모든 Skill 중에서 **description만 보고** 무엇을 열지 결정합니다. "Skill이 안 먹힌다"는 문제의 대부분은 description 문제입니다.

**원칙 4가지**

1. **3인칭으로 쓴다** — description은 Claude의 시스템 안내에 들어갑니다.
   - ✅ "Processes Excel files and generates reports."
   - ❌ "I can help you…" / "You can use this to…"
2. **무엇(What) + 언제(When)** 를 둘 다 쓴다.
3. **사용자가 실제로 쓸 단어**를 넣는다 — 파일 확장자, 도구 이름, **한국어 표현**까지.
4. **핵심 용도를 앞에** 둔다.

**Before / After**

```yaml
# ❌ Before — 언제 써야 할지 알 수 없음
description: 문서 작업 도우미

# ✅ After — 무엇 + 언제 + 트리거 단어 + 경계
description: >-
  Writes the team's weekly status report from meeting notes, Jira exports,
  or bullet points, using the fixed section order and risk levels. Use when
  the user asks for a weekly report, 주간보고, or status update.
  Do not use for monthly business reviews.
```

> [!example] 연습: 이 description을 고쳐 보세요
> `description: 로그 분석 도구`
> > [!success]- 모범 답안 (클릭해서 펼치기)
> > ```yaml
> > description: >-
> >   Analyzes VMS server and IP camera log files (.log, .txt) to find
> >   errors, disconnections, and RTSP/ONVIF failures, then summarizes them
> >   by device and hour. Use when the user shares camera or VMS logs, asks
> >   why a camera went offline, or says "로그 분석해줘".
> > ```

> [!warning] 과잉 트리거 vs 과소 트리거
> - 너무 넓으면(`Use for any document task`) 엉뚱한 작업에서 로드 → 지침 충돌
> - 너무 좁으면(`Use only when the user says "주간보고 skill"`) 필요할 때 안 열림
> - **경계 조건**("Do not use for…")을 함께 적으면 정확도가 올라갑니다.

### 4.4 본문 작성 원칙

**① 간결함 — Claude는 이미 똑똑하다**

Claude가 이미 아는 일반 지식은 빼고, **우리 팀·도메인에만 있는 지식**만 쓰세요.

````markdown
<!-- ❌ 장황함 -->
주간보고란 한 주 동안의 업무 진행 상황을 정리하여 상급자에게 보고하는
문서로, 일반적으로 다음과 같은 요소를 포함하는데…

<!-- ✅ 간결함 -->
## 섹션 순서 (변경 금지)
1. 요약 (3줄)  2. 진행 현황 (표)  3. 리스크 (상/중/하)  4. 다음 주 계획
````

> [!question] 판단 기준
> 각 문장마다 "**Claude가 이 문장 없이도 이걸 알까?**" — 알면 지우세요.

**② 구조 — 훑어보기 쉽게**

```markdown
# <Skill 제목>
## Quick start         ← 가장 흔한 케이스
## Workflow            ← 단계별 절차 (체크리스트)
## Rules               ← 반드시 지킬 규칙
## Examples            ← 입력/출력 예시
## References          ← 상세 파일 안내
```

**③ 기본값 하나만 제시하라 (메뉴 X)**

```markdown
<!-- ❌ -->
pypdf, pdfplumber, PyMuPDF 중 아무거나 써도 된다.

<!-- ✅ -->
텍스트 추출에는 pdfplumber를 쓴다.
스캔된 PDF(텍스트 레이어 없음)일 때만 OCR을 쓴다.
```

**④ 예시가 설명보다 강하다** — 스타일은 입력/출력 예시 한 쌍으로 전달하세요.

**⑤ 용어 통일, 시간 의존 정보 금지** — "올해 3월 이후에는…" 같은 문장은 곧 틀립니다.

### 4.5 Part 4 체크포인트

> [!check] 셀프 체크
> - [ ] `name`이 소문자-하이픈이고, 예약어가 없고, 폴더명과 같다
> - [ ] `description`이 3인칭이고 What + When + 트리거 단어를 포함한다
> - [ ] 본문에 Claude가 이미 아는 일반론이 없다
> - [ ] 기본 방법을 하나로 정했고, 예시가 있다


---

# 🟡 중급

## Part 5. 파일 번들링 — references, scripts, assets

### 5.1 언제 파일을 분리하나

| 신호 | 조치 |
|---|---|
| `SKILL.md`가 **500줄**을 넘어간다 | 상세 내용을 `references/`로 분리 |
| Claude가 매번 같은 코드를 새로 짠다 | `scripts/`로 고정 |
| 정확해야 하는 계산·파싱·검증이 있다 | `scripts/`로 고정 (결정론) |
| 출력 형식이 엄격하다 (보고서 양식 등) | `assets/`에 템플릿 |
| 도메인이 여러 개다 (영업/제품/기술) | 도메인별 reference 파일 |

### 5.2 references — 필요할 때만 읽는 문서

````markdown
# Writing Product Requirement Docs

## Workflow
1. 요청 유형을 판단한다.
   - 신규 기능 PRD → `references/prd-template-guide.md` 를 읽는다.
   - 경쟁사 비교가 필요하면 → `references/competitors.md` 를 읽는다.
   - 용어가 헷갈리면 → `references/glossary.md` 를 읽는다.
2. ...
````

> [!important] 참조는 1단계 깊이만
> `SKILL.md → a.md → b.md` 처럼 **중첩 참조를 만들지 마세요.** 중첩된 파일은 일부만 미리보고 넘어가 정보가 누락될 수 있습니다. **모든 reference는 `SKILL.md`에서 직접 안내**하세요.

> [!tip] 100줄이 넘는 reference에는 맨 위에 목차를
> 일부만 읽어도 전체 범위를 파악할 수 있게 됩니다.

### 5.3 scripts — 결정론적 작업은 코드로

스크립트의 3대 이점: **신뢰성**(매번 같은 결과) · **토큰 절약**(소스가 대화에 안 들어옴) · **속도**.

**스크립트 경로 표기 (Desktop 기준 권장)**

```markdown
`python3 ${CLAUDE_SKILL_DIR}/scripts/validate.py <file>` 를 **실행**한다.
```

| 탭 | `${CLAUDE_SKILL_DIR}` 처리 |
|---|---|
| Cowork, Code | Skill 폴더의 실제 경로로 **자동 치환** |
| Chat | Skill 폴더 전체가 샌드박스로 복사됨 → **`SKILL.md` 기준 상대 경로(`scripts/validate.py`)로도 읽히게** 써 두면 안전 |

**의도를 명확히 쓰기**

```markdown
<!-- 실행하라는 뜻 -->
`scripts/analyze.py` 를 **실행**해 결과를 얻는다. 파싱 코드를 새로 작성하지 않는다.

<!-- 참고하라는 뜻 -->
매핑 규칙은 `scripts/analyze.py` 의 `RULES` 상수를 **참고**한다.
```

**스크립트 작성 4원칙**

````python
#!/usr/bin/env python3
"""Count error lines per device. Usage: python3 count_errors.py <logfile>"""
import sys
from collections import Counter

# 원칙 1: 에러를 Claude에게 떠넘기지 말고 스스로 처리
if len(sys.argv) != 2:
    print("ERROR: usage: count_errors.py <logfile>")
    sys.exit(2)
try:
    with open(sys.argv[1], encoding="utf-8", errors="replace") as f:
        lines = f.readlines()
except FileNotFoundError:
    # 원칙 2: 다음 행동을 알 수 있는 구체적 메시지
    print(f"ERROR: file not found: {sys.argv[1]}. Ask the user for the correct path.")
    sys.exit(1)

# 원칙 3: 매직 넘버에는 이유를 주석으로
TOP_N = 10  # 요약에는 상위 10개 장비면 충분 (그 이상은 노이즈)

counts = Counter(l.split()[1] for l in lines if " ERROR " in l and len(l.split()) > 1)
# 원칙 4: 출력은 짧고 구조적으로 (이 출력만 대화에 들어간다)
for device, n in counts.most_common(TOP_N):
    print(f"{device}\t{n}")
````

> [!warning] 실행 환경과 의존성
> - **Chat**: 클라우드 샌드박스. 네트워크·패키지 설치 가능 여부는 **계정/조직 설정에 따라 다름**, 세션 간 데이터는 유지되지 않음
> - **Cowork**: 내 컴퓨터의 격리된 작업 환경에서 실행, 연결한 폴더에 접근
> - **Code**: 내 컴퓨터에서 직접 실행
>
> → **표준 라이브러리로 해결**하는 것이 가장 이식성이 좋습니다. 외부 패키지가 필요하면 `SKILL.md`에 명시하세요.

> [!danger] 비밀 값 금지
> API 키·비밀번호를 스크립트나 Skill 어디에도 넣지 마세요. **공유받은 사람 모두가 파일을 받습니다.** 외부 서비스 접근은 **커넥터**를 쓰게 하세요(각자 자기 계정으로 로그인).

### 5.4 assets — 출력용 템플릿·리소스

```text
writing-weekly-report/
├── SKILL.md
└── assets/
    └── report-template.md
```

```markdown
## Output
1. `assets/report-template.md` 를 복사해 `weekly-report-YYYY-MM-DD.md` 로 만든다.
2. `{{SUMMARY}}`, `{{PROGRESS}}`, `{{RISKS}}`, `{{NEXT_WEEK}}` 를 채운다.
3. 섹션 순서와 제목은 바꾸지 않는다.
```

---

## Part 6. 탭별 동작 차이 — Chat · Cowork · Code

### 6.1 한눈에 비교

| 항목 | 💬 Chat | 🤝 Cowork | 👩‍💻 Code |
|---|---|---|---|
| Skill 출처 | Customize (계정) | Customize (계정) | Customize(동기화) + 로컬 `~/.claude/skills`, `.claude/skills` |
| 실행 위치 | 클라우드 샌드박스 | 내 컴퓨터의 격리 환경 | 내 컴퓨터 |
| 로컬 파일 접근 | ❌ (첨부만) | ✅ 연결한 폴더 | ✅ 프로젝트 폴더 |
| `/` 로 직접 호출 | ✅ | ✅ | ✅ |
| `${CLAUDE_SKILL_DIR}` 치환 | 폴더 복사 (상대 경로 병행) | ✅ | ✅ |
| 플러그인의 Skills / Commands | ✅ / Skill로 로드 | ✅ / `/plugin:command` | ✅ / ✅ |
| 플러그인의 Agents / Hooks | ❌ 무시 | ✅ | ✅ |
| 원격 MCP 커넥터 | ✅ (Connectors 탭에서 연결) | ✅ | ✅ |
| 로컬 MCP 서버 | ❌ | ✅ (내 컴퓨터에서 실행될 때) | ✅ |
| Claude Code 전용 frontmatter | 무시될 수 있음 | 일부 | ✅ 전부 |

> [!tip] 어느 탭에서 쓸까?
> - **Chat**: 첨부 파일 하나 처리, 문서 생성, 빠른 질의
> - **Cowork**: 폴더 단위 작업(여러 파일 정리·변환·분석), 브라우저 연동, 오래 걸리는 다단계 작업
> - **Code**: 코드베이스 작업, 개발 워크플로 자동화

### 6.2 Code 탭(Claude Code)에서만 확실히 쓰는 frontmatter

개발자라면 Code 탭에서 더 세밀하게 제어할 수 있습니다. 상세는 [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#부록 D. 개발자 확장 — Code 탭, CLI, API\|부록 D]].

| 필드 | 용도 |
|---|---|
| `disable-model-invocation: true` | Claude가 **자동으로는** 못 씀 (배포처럼 부작용 있는 작업) |
| `user-invocable: false` | `/` 메뉴에서 숨김 (배경 지식형) |
| `allowed-tools` / `disallowed-tools` | 승인 없이 허용할 도구 / 제거할 도구 |
| `context: fork`, `agent` | 서브에이전트에서 실행 |
| `argument-hint`, `arguments`, `$ARGUMENTS` | 인자 받기 |
| `` !`command` `` | 실행 전 셸 결과 주입 |

> [!warning] 모르는 필드는 조용히 무시됩니다
> 오류가 나지 않으므로 "넣었는데 왜 안 되지?"가 생깁니다. **Chat·Cowork에서도 쓸 Skill이라면 `name`과 `description`만으로 동작하도록** 설계하고, 추가 필드는 보너스로 생각하세요.

---

## Part 7. 실전 예제 4종

### 7.1 예제 ① — 주간보고 Skill (지침 + 템플릿) · Chat/Cowork

```text
writing-weekly-reports/
├── SKILL.md
└── assets/
    └── report-template.md
```

**SKILL.md**

````markdown
---
name: writing-weekly-reports
description: >-
  Writes the VMS team's weekly status report from meeting notes, Jira
  exports, or bullet points, using a fixed section order, RAG risk levels,
  and week-over-week deltas. Use when the user asks for a weekly report,
  주간보고, 주간 업무 보고, or a status update. Do not use for monthly reviews.
---

# Writing Weekly Reports

## Workflow
1. 입력에서 완료/진행/지연 항목과 수치를 추출한다.
2. `assets/report-template.md` 의 구조를 그대로 사용한다.
3. 수치가 있으면 전주 대비 증감을 `▲3 / ▼2 / -` 형식으로 쓴다.
4. 입력에 없는 사실은 만들지 않는다. 비어 있으면 "(확인 필요)"로 둔다.

## Rules
- 요약은 3줄 이내, 각 줄은 결과 중심("~완료", "~지연")
- 리스크 등급: 🔴 상(일정 영향) / 🟠 중(대응 필요) / 🟢 하(모니터링)
- 고객사명은 약어 대신 정식 명칭

## Example
Input: "녹화 엔진 v2 머지 완료. ONVIF Profile M 테스트 2주 지연(장비 미입고). 버그 41→35"
Output (일부):
| 항목 | 상태 | 비고 |
|---|---|---|
| 녹화 엔진 v2 | ✅ 완료 | main 머지 |
| ONVIF Profile M 테스트 | ⏳ 지연 | 장비 미입고, 2주 |
| 오픈 버그 | 35 (▼6) | |
````

**assets/report-template.md**

```markdown
# 주간보고 ({{WEEK}})

## 1. 요약
{{SUMMARY}}

## 2. 진행 현황
| 항목 | 상태 | 비고 |
|---|---|---|
{{PROGRESS_ROWS}}

## 3. 리스크
{{RISKS}}

## 4. 다음 주 계획
{{NEXT_WEEK}}
```

> [!note] 포인트
> 규칙을 길게 설명하는 대신 **입력/출력 예시**와 **템플릿**으로 형식을 고정했습니다.

### 7.2 예제 ② — 경쟁 제품 비교 Skill (references 분리) · Chat/Cowork

상품기획 업무처럼 **배경 지식이 많은** Skill은 reference 분리가 핵심입니다.

```text
comparing-vms-competitors/
├── SKILL.md
└── references/
    ├── evaluation-criteria.md   ← 평가 항목과 가중치
    ├── competitor-notes.md      ← 경쟁사별 공개 정보 메모
    └── terminology.md           ← 용어 정의
```

**SKILL.md**

````markdown
---
name: comparing-vms-competitors
description: >-
  Builds feature and positioning comparisons between our VMS and competing
  video management products using the team's weighted evaluation criteria.
  Use when the user asks to compare VMS products, 경쟁사 비교, feature gap
  analysis, or positioning for a proposal.
---

# Comparing VMS Competitors

## Workflow
1. 비교 대상과 목적(제안서용 / 내부 로드맵용)을 확인한다.
2. `references/evaluation-criteria.md` 의 항목과 가중치로 표를 만든다.
3. 경쟁사 정보는 `references/competitor-notes.md` 와 사용자가 준 자료만 사용한다.
   **최신 정보가 필요하면 웹 검색 결과에 출처를 붙이고, 추정은 "추정"으로 표시한다.**
4. 결과: 가중 점수표 → 강점/약점 3개씩 → 우리 제품 Gap 상위 5개 → 권장 액션

## Rules
- 경쟁사를 깎아내리는 표현 대신 사실 기반 비교
- 점수 근거를 셀 옆 비고에 한 줄로
````

### 7.3 예제 ③ — 설정 검증 Skill (스크립트 + 피드백 루프) · Cowork 추천

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
   `python3 ${CLAUDE_SKILL_DIR}/scripts/validate_config.py <path>`
3. `ERROR`가 있으면 메시지대로 고치고 **2번으로 돌아간다**.
4. `OK`가 출력될 때만 작업 완료를 보고한다.

## Rules
- 검증 규칙을 우회하거나 스크립트를 수정하지 않는다.
- 원본 파일은 `cameras.backup.json` 으로 먼저 복사해 둔다.
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

**실행 예 (Cowork에서 폴더 연결 후 "cameras.json 검증하고 고쳐줘")**

```text
ERROR: cameras[1]: duplicate id 'cam-01'
ERROR: cameras[2]: invalid ip '192.168.1.300'
ERROR: cameras[2]: fps must be int 1-60, got 120
→ Claude가 수정 → 재실행
OK: 3 cameras valid
```

> [!success] 중급의 핵심
> - **검증은 스크립트(결정론)**, **수정은 Claude(판단)** — 각자 잘하는 일을 분담
> - 구체적 에러 메시지 덕분에 Claude가 스스로 루프를 돈다
> - "OK일 때만 완료" 규칙으로 **조기 종료 방지**

### 7.4 예제 ④ — 커넥터 + Skill: 버그 트리아지 · Chat/Cowork

**준비**: `Customize > Connectors`에서 Jira(또는 사용하는 이슈 트래커)와 Slack을 **Connect**.

**SKILL.md**

````markdown
---
name: triaging-vms-bugs
description: >-
  Triages incoming VMS bug reports into the team's Jira project with the
  correct component, priority, and labels, then posts a summary to Slack.
  Use when the user shares a bug report, customer issue, or says
  "버그 등록해줘" or "이슈 분류해줘".
---

# Triaging VMS Bugs

## Workflow
1. 리포트에서 증상, 재현 절차, 장비 모델, 펌웨어/VMS 버전을 추출한다. 없으면 사용자에게 묻는다.
2. 중복 확인: Jira 커넥터의 이슈 검색 도구로 최근 30일 유사 이슈를 찾는다.
3. 아래 규칙으로 필드를 정한다.
4. **이슈를 만들기 전에** 필드 요약을 보여주고 사용자 승인을 받는다.
5. 생성 후 Slack 커넥터로 `#vms-qa` 채널에 3줄 요약을 게시한다.

## Field rules
| 조건 | Component | Priority |
|---|---|---|
| 녹화 누락/손상 | Recording | Highest |
| 라이브 영상 끊김 | Streaming | High |
| UI 표시 오류 | Client-UI | Medium |

- 라벨: `customer-reported` (고객 출처일 때), 장비 모델명 소문자
````

> [!tip] 커넥터 도구 이름은 정확하게
> 커넥터가 여러 개면 도구를 혼동할 수 있습니다. 도구 이름을 알면 `서버명:도구명` 형식(예: `Jira:search_issues`)으로 적으세요. 모르면 위처럼 "**Jira 커넥터의 이슈 검색 도구**"처럼 서비스를 명확히 지정합니다.

> [!important] 부작용이 있는 단계에는 승인 단계를
> 이슈 생성, 메시지 발송처럼 **되돌리기 어려운 동작 전에는 사용자 확인**을 받도록 Skill에 명시하세요.

---

# 🔴 고급

## Part 8. 고급 설계 패턴

### 8.1 자유도(Degrees of Freedom) 설계

작업이 **얼마나 깨지기 쉬운가**에 맞춰 지침의 강도를 조절합니다.

```mermaid
flowchart LR
    H["🟢 높은 자유도<br/>텍스트 가이드<br/>예: 기획 아이디어, 리뷰 관점"] --- M["🟡 중간 자유도<br/>템플릿 / 파라미터 스크립트<br/>예: 보고서"] --- L["🔴 낮은 자유도<br/>정확한 명령<br/>예: 데이터 마이그레이션"]
```

| 자유도 | 언제 | 쓰는 법 |
|---|---|---|
| 높음 | 여러 접근이 다 유효, 맥락 판단 중요 | "~를 고려하라", 관점 목록 |
| 중간 | 선호 패턴은 있지만 변형 허용 | 템플릿, 옵션 있는 스크립트 |
| 낮음 | 순서·정확성이 치명적 | `python3 scripts/migrate.py --verify --backup` + "**명령을 바꾸지 마라**" |

> [!example] 비유
> 높은 자유도 = 넓은 들판(어느 길로 가도 됨), 낮은 자유도 = 양옆이 절벽인 다리(정해진 길만).

### 8.2 체크리스트 워크플로

````markdown
## Release note workflow
다음 체크리스트를 응답에 복사하고 진행하며 체크한다:
```
- [ ] 1. 변경 목록 수집 (Jira 커넥터: fixVersion = 이번 릴리스)
- [ ] 2. 사용자 영향 기준으로 분류 (references/categories.md)
- [ ] 3. 초안 작성 (assets/release-note-template.md)
- [ ] 4. 금지 표현 검사 (scripts/lint_terms.py)
- [ ] 5. 사용자 검토 요청
```
**4번이 실패하면 5번으로 넘어가지 않는다.**
````

### 8.3 조건 분기 워크플로

```markdown
## 작업 유형 판별
- **새 문서 작성?** → Creation workflow
- **기존 문서 수정?** → Editing workflow (원본은 덮어쓰지 말고 새 파일로)
- **형식 변환만?** → `scripts/convert.py` 실행 후 종료
```

### 8.4 Plan → Validate → Execute (고위험 일괄 작업)

수백 개 파일 이름 변경, 대량 데이터 수정처럼 **되돌리기 어려운 작업**에 씁니다. Cowork에서 특히 유용합니다.

```mermaid
flowchart LR
    A[Claude: 변경 계획<br/>changes.json 작성] --> B{scripts/validate_plan.py}
    B -- "ERROR: 구체적 메시지" --> A
    B -- OK --> C[사용자 확인]
    C --> D[scripts/apply.py]
    D --> E[scripts/verify.py]
```

````markdown
## Bulk rename workflow
1. 바로 바꾸지 말고 `changes.json` 을 먼저 작성한다:
   ```json
   [{"from": "export/CAM01_0912.mp4", "to": "export/2026-09-12_CAM-01.mp4"}]
   ```
2. `python3 ${CLAUDE_SKILL_DIR}/scripts/validate_plan.py changes.json` — 충돌·누락 검사
3. 오류가 있으면 계획을 고치고 2번 반복
4. 변경 요약(건수, 예시 5개)을 보여주고 승인을 받는다
5. `apply.py` 실행 → `verify.py` 로 결과 확인
````

> [!important] 왜 효과적인가
> 실행 전에 오류를 잡고, 에러 메시지로 Claude가 스스로 고치며, 사람이 검토할 **체크포인트**가 생깁니다.

### 8.5 템플릿: 엄격 vs 유연

```markdown
## 엄격 (다른 Skill/프로그램이 읽는 출력)
반드시 이 JSON 형식만 출력한다. 다른 텍스트를 붙이지 않는다.
{"severity": "high|medium|low", "device": "string", "summary": "string"}

## 유연 (사람이 읽는 출력)
아래는 권장 구조다. 내용에 따라 섹션을 합치거나 생략해도 된다.
```

### 8.6 Skill 조합 (Composability)

Skill은 **자동으로 함께 쓰입니다.** 예: "카메라 로그 분석해서 엑셀 보고서로 만들어줘" → `analyzing-camera-logs`(분석) + Excel Skill(출력).

- **한 Skill = 한 책임** — 분석 Skill이 엑셀 서식까지 떠안지 않게
- 출력은 **다른 Skill이 쓰기 좋은 형태**(JSON, CSV)로도 낼 수 있게
- Skill끼리 강하게 엮지 말 것 — 조합은 Claude가 한다

---

## Part 9. Cowork에서 Skill 200% 활용하기

### 9.1 Cowork가 Skill에 주는 것

| Cowork 능력 | Skill 활용 |
|---|---|
| **로컬 폴더 읽기/쓰기** | 업로드 없이 폴더 전체(로그, 엑셀, 문서) 처리 |
| **서브에이전트 병렬 작업** | 큰 작업을 나눠 처리 (예: 파일 100개 분석) |
| **Claude in Chrome 연동** | 웹 페이지 조작이 필요한 절차를 Skill로 표준화 |
| **플러그인의 agents/hooks** | Chat에서 못 쓰는 고급 구성 요소 사용 |
| **긴 다단계 작업** | 결과물을 맡기고 나중에 확인 |

### 9.2 Cowork용 Skill 작성 팁

````markdown
## Workflow (Cowork)
1. 사용자가 연결한 폴더에서 `*.log` 파일을 찾는다. 하위 폴더 포함.
2. 파일이 20개를 넘으면 서브에이전트로 나눠 처리하고 결과(JSON)만 모은다.
3. 원본 파일은 수정하지 않는다. 결과는 원본 옆 `analysis/` 폴더에 새 파일로 만든다.
4. 마지막에 만든 파일 목록과 위치를 알려준다.
````

> [!tip] Cowork Skill의 3대 원칙
> 1. **원본 보존** — 변환·정리 결과는 새 파일/새 폴더로
> 2. **결과 위치 명시** — 어디에 무엇을 만들었는지 마지막에 보고
> 3. **대량 작업은 계획 먼저** — [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#8.4 Plan → Validate → Execute (고위험 일괄 작업)\|Plan → Validate → Execute]]

### 9.3 Cowork를 Skill 개발 작업대로 쓰기

```mermaid
flowchart LR
    A["Cowork: 실습 폴더 연결"] --> B["Skill 폴더 작성/수정"]
    B --> C["스크립트를 로컬에서 실행해 검증"]
    C --> D["ZIP 생성 + unzip -l 구조 확인"]
    D --> E["Customize > Skills 업로드"]
    E --> F["새 대화에서 테스트"]
    F -- 수정 필요 --> B
```

요청 예:

```text
~/claude-skills-lab/analyzing-camera-logs 를 점검해줘.
1) SKILL.md frontmatter가 Agent Skills 사양에 맞는지
2) scripts/ 의 스크립트를 evals/fixtures 의 샘플로 실행해 보고
3) 문제가 없으면 업로드용 ZIP을 올바른 구조로 만들어줘.
```


---

## Part 10. 플러그인 — Skill 묶어서 배포하기

### 10.1 플러그인이란

**Skill + 커넥터(MCP) + 명령 + 에이전트 + 훅**을 하나로 묶은 패키지입니다. "우리 팀 업무 세트"를 한 번에 설치하게 해 줍니다.

| 구성 요소 | 경로 | Chat | Cowork | Code |
|---|---|---|---|---|
| Skills | `skills/<name>/SKILL.md` | ✅ | ✅ | ✅ |
| Commands | `commands/*.md` | Skill로 로드 | `/plugin:command` | ✅ |
| Agents | `agents/*.md` | ❌ | ✅ | ✅ |
| Hooks | `hooks/hooks.json` | ❌ | ✅ | ✅ |
| 원격 MCP | `.mcp.json` (http/sse) | Connectors 탭에서 연결 | ✅ | ✅ |
| 로컬 MCP | `.mcp.json` (command) | ❌ | 내 컴퓨터 세션에서 ✅ | ✅ |
| `bin/` 실행 파일 | `bin/` | ⛔ **설치 거부** | ⛔ **설치 거부** | ✅ |

> [!danger] `bin/` 폴더 주의
> 플러그인 최상위에 `bin/`이 있으면 Chat·Cowork에서 **플러그인 전체가 설치되지 않습니다.** Desktop용 플러그인에는 넣지 마세요.

### 10.2 플러그인 만드는 세 가지 방법

`Customize > Plugins > Add` 메뉴:

| 메뉴 | 설명 |
|---|---|
| **Create with Claude** | 대화(또는 Cowork 작업)로 설명하면 Claude가 `.plugin` 파일을 만들어 줌 → 카드의 **Save plugin** |
| **Create a plugin** | 폼에 이름·용도를 입력하고 에디터에서 Skill·명령·커넥터를 직접 작성 |
| **Upload plugin** | 직접 만든 플러그인 폴더를 ZIP으로 업로드 |

### 10.3 직접 만들기 — 폴더 구조

```text
vms-team-toolkit/
├── .claude-plugin/
│   └── plugin.json            ← 필수: 매니페스트
├── skills/
│   ├── writing-weekly-reports/
│   │   ├── SKILL.md
│   │   └── assets/report-template.md
│   ├── triaging-vms-bugs/SKILL.md
│   └── analyzing-camera-logs/
│       ├── SKILL.md
│       └── scripts/analyze_logs.py
├── commands/
│   └── weekly.md              ← /vms-team-toolkit:weekly
├── agents/                    (선택, Cowork/Code)
├── .mcp.json                  (선택: 원격 MCP 서버)
├── README.md                  (디렉터리 공개 시 필수)
└── LICENSE                    (디렉터리 공개 시 필수)
```

**`.claude-plugin/plugin.json`**

```json
{
  "name": "vms-team-toolkit",
  "displayName": "VMS Team Toolkit",
  "version": "1.0.0",
  "description": "VMS 팀 공용 업무 세트: 주간보고, 버그 트리아지, 카메라 로그 분석",
  "author": { "name": "VMS SW Product Team" },
  "license": "MIT"
}
```

> [!important] `name`은 영구 식별자
> 설치 후 사람들이 이 값으로 플러그인을 참조합니다. **출시 후 바꾸지 마세요.** 표시 이름은 `displayName`으로 바꿉니다.

**`commands/weekly.md`**

```markdown
---
description: 이번 주 주간보고 초안 작성
---

이번 주 Jira 완료/진행 이슈와 사용자가 준 메모를 바탕으로
writing-weekly-reports Skill의 형식에 맞춰 주간보고 초안을 작성한다.
```

**`.mcp.json` (사내 원격 MCP 서버 예시)**

```json
{
  "mcpServers": {
    "vms-telemetry": {
      "type": "http",
      "url": "https://mcp.example.internal/mcp"
    }
  }
}
```

> [!warning] `.mcp.json`에 비밀 값 금지
> URL만 넣으세요. 인증은 각 사용자가 플러그인의 **Connectors** 탭에서 자기 계정으로 합니다.

### 10.4 업로드와 테스트

1. 플러그인 폴더를 ZIP으로 압축 (`.claude-plugin/plugin.json`이 ZIP 루트 또는 단일 최상위 폴더 바로 아래에 있어야 함)
2. `Customize > Plugins > Add > Upload plugin`
3. Chat에서 "플러그인에서 어떤 Skill을 받았는지 알려줘"로 확인
4. 플러그인의 **Connectors** 탭에서 커넥터 연결
5. agents가 있다면 **Cowork** 작업에서 확인

> [!tip] 개발자라면
> Claude Code CLI가 있다면 `claude plugin validate ./vms-team-toolkit` 로 업로드 전에 매니페스트와 Skill frontmatter를 검사할 수 있습니다 (`✔ Validation passed`).

### 10.5 팀 마켓플레이스 (Git 저장소)

여러 플러그인을 팀에 배포할 때는 Git 저장소를 마켓플레이스로 씁니다.

1. 저장소에 플러그인 폴더들과 `marketplace.json`을 둠
2. 팀원: `Customize > Plugins > Add > Add marketplace` → `https://github.com/owner/repo` 또는 `owner/repo`
3. 갱신: 마켓플레이스에서 **Update**

| 기본 한도 | 값 |
|---|---|
| 플러그인 크기 (압축 해제) | 200 MB |
| 플러그인당 파일 수 | 5,000 |
| 직접 추가 가능한 마켓플레이스 | 25개 |

> [!note] Code 탭과의 동기화
> Customize에서 계정에 설치한 플러그인은 다음 세션부터 Claude Code(Code 탭·CLI)에도 **동기화**됩니다. 반대로 CLI에서 설치한 플러그인은 계정에 올라가지 않습니다.

---

## Part 11. 공유와 조직 배포

### 11.1 공유 방식 비교

| 방식 | 플랜 | 방법 | 받는 쪽 |
|---|---|---|---|
| 개인 사용 | Pro 이상 | 업로드만 | 나만 |
| **특정 동료 공유** | Team / Enterprise | Skill 페이지 → **Share** | **Shared with you**에 표시, 직접 켜야 함, 읽기 전용 |
| **그룹 공유** | Enterprise | Share → 그룹 선택 | 그룹 구성원 |
| **조직 게시** | Team / Enterprise | Skill 페이지 → **Publish to org** | 조직 라이브러리에서 설치 |
| **관리자 배포(Provision)** | Team / Enterprise (Owner) | Organization settings | 전원에게 즉시, 기본 켜짐 |

### 11.2 관리자(Owner) 배포 절차

1. `Organization settings > Plugins & skills` → **Policy** 탭에서 코드 실행과 **Skills** 활성화 확인
2. 우측 상단 **Add** → **Upload a skill**(ZIP) 또는 **Create a skill**
3. 저장 즉시 모든 구성원에게 배포 (기본 켜짐, 사용자가 개별로 끌 수는 있지만 삭제 불가)

추가 정책 (Policy 탭):

| 설정 | 효과 |
|---|---|
| **User-created skills** 끄기 | 구성원이 Skill을 직접 만들지 못함 (배포된 Skill은 유지) |
| **Publishing** | 조직 게시를 Open / Requires review 등으로 통제 |
| 플러그인 상태 | **Not available / Available to install / Installed by default / Required** |

> [!tip] 특정 부서에만 배포하려면 (Enterprise)
> Skill을 **플러그인으로 묶어 그룹에 할당**합니다. 예: `vms-team-toolkit`은 VMS 개발 그룹에만.

### 11.3 사용량 확인

Team/Enterprise에서는 Skill 페이지에 **Adoption**(조직 내 사용 범위), **Activity**(사용 활동), **You**(내 사용량)가 표시됩니다. 많이 안 쓰이는 Skill은 description을 개선하거나 정리하세요.

---

## Part 12. 평가 주도 개발 (Eval)

> [!quote] 고급 사용자를 가르는 습관
> **"Skill을 쓰기 전에 테스트 시나리오부터 만든다."** — TDD의 Skill 버전입니다.

### 12.1 프로세스

```mermaid
flowchart LR
    A[1. Skill 없이 실제 작업] --> B[2. 부족한 점 기록]
    B --> C[3. 시나리오 3개 이상 작성]
    C --> D[4. 기준선 측정]
    D --> E[5. 최소한의 지침 작성]
    E --> F[6. 재측정]
    F -- 미달 --> E
    F -- 통과 --> G[공유/배포]
```

### 12.2 시나리오 형식

```json
{
  "skill": "analyzing-camera-logs",
  "query": "첨부한 nvr-0912.log 분석해서 오프라인 된 카메라랑 원인 알려줘",
  "files": ["fixtures/nvr-0912.log"],
  "expected_behavior": [
    "scripts/analyze_logs.py 를 실행한다 (파싱 코드를 새로 쓰지 않는다)",
    "CAM-07 의 RTSP timeout 반복을 가장 심각한 문제로 보고한다",
    "로그 안의 비밀번호를 출력하지 않는다"
  ],
  "must_not_trigger_on": ["엑셀 수식 고쳐줘", "주간보고 써줘"]
}
```

> [!tip] 트리거 테스트는 양방향으로
> "써야 할 때 쓰는가"와 "**쓰지 말아야 할 때 안 쓰는가**"를 둘 다 확인하세요. description 튜닝은 이 둘의 균형입니다.

### 12.3 skill-creator로 평가하기

`Customize > Skills`에서 **skill-creator**를 켜고 "내 analyzing-camera-logs Skill을 평가해줘"라고 요청합니다.

| 탭 | skill-creator 평가 방식 |
|---|---|
| **Chat** | 테스트 프롬프트를 하나씩 실행하고 결과를 대화에 보여줌 |
| **Cowork** | Skill **없는 기준선**도 함께 **병렬 실행**하고 통과율·소요 시간·토큰 수를 비교 |

> [!important] 진지한 평가는 Cowork에서
> 기준선 대비 개선을 숫자로 볼 수 있어 "이 Skill이 정말 도움이 되나?"에 답할 수 있습니다.

### 12.4 Claude A / Claude B 반복법

| 역할 | 하는 일 |
|---|---|
| **Claude A** (작성자 대화) | Skill 초안 작성·수정 |
| **Claude B** (새 대화, Skill 켜짐) | 실제 작업 수행 → 관찰 대상 |
| **나** | B의 실패를 A에게 전달 |

관찰 포인트:

- 특정 reference를 **매번** 읽는다 → 그 내용은 `SKILL.md` 본문으로 올린다
- 어떤 파일을 **한 번도** 안 읽는다 → 불필요하거나 안내가 약하다
- 스크립트 대신 **코드를 새로 짠다** → "반드시 실행하라" 지시가 약하다
- 엉뚱한 순서로 진행한다 → 체크리스트화한다

---

## Part 13. 보안과 운영

### 13.1 보안 — Skill 설치는 "소프트웨어 설치"다

> [!danger] 주요 위험: 프롬프트 인젝션과 데이터 유출
> Skill은 Claude에게 지시를 내리고 코드를 실행시킵니다. 업로드·공유된 Skill은 **Anthropic이 검토하지 않습니다.**

**외부 Skill을 켜기 전 체크리스트**

- [ ] `SKILL.md`와 **모든** 파일(스크립트, 이미지, 리소스)을 열어 읽었다
- [ ] 목적과 무관한 네트워크 호출(`curl`, `requests`, `fetch`)이 없다
- [ ] 목적과 무관한 파일 접근(`~/.ssh`, `.env`, 자격 증명)이 없다
- [ ] 외부 URL에서 지시를 받아오는 구조가 아니다
- [ ] 출처를 신뢰할 수 있다 (내가 만든 것, Anthropic, 사내 검증본)

**자체 Skill 작성 시**

- 비밀 값은 넣지 않는다 → 커넥터 사용
- 스크립트 출력에서 민감 정보 마스킹 (출력이 대화에 들어가므로)
- 부작용 있는 단계에는 **사용자 승인 단계**를 명시

> [!note] 조직 기능
> Enterprise에서는 claude.ai/Cowork에 업로드된 커스텀 Skill에 대한 **보안 스캔**을 켤 수 있습니다.

### 13.2 성능 — 컨텍스트 관리

| 항목 | 비용 | 최적화 |
|---|---|---|
| 켜진 Skill의 이름+설명 | 항상 | 안 쓰는 Skill은 끄기 |
| `SKILL.md` 본문 | 트리거 시 전체 | 500줄 이하, 일반론 제거 |
| reference | 읽을 때 | 주제별 분할 |
| 스크립트 | **출력만** | 출력을 요약·제한 |

> [!tip] 가장 효과 큰 최적화
> "Claude가 읽고 계산하던 것"을 "스크립트가 계산하고 결과만 출력"하게 바꾸기. 10MB 로그를 읽게 하지 말고 30줄 요약을 출력하게 하세요.

### 13.3 Skill 라이프사이클

```mermaid
stateDiagram-v2
    [*] --> Draft: 같은 지시를 3번 이상 반복
    Draft --> Eval: 시나리오 작성
    Eval --> Draft: 실패
    Eval --> Shared: 통과 → Share / Publish
    Shared --> Monitoring: Adoption / Activity 확인
    Monitoring --> Draft: 실패 사례 / 요구 변경
    Monitoring --> Retired: 사용 감소
    Retired --> [*]
```

- **언제 Skill을 만드나?** 같은 설명을 **3번 이상** 반복했을 때
- 업데이트는 ZIP 재업로드로, 변경 내역은 `SKILL.md` 하단이나 별도 CHANGELOG로 관리
- 원본은 **Git 저장소 하나**에 두고, 거기서 ZIP/플러그인을 만들어 배포

---

# 🏁 마무리

## Part 14. 캡스톤 — 카메라 로그 분석 Skill

지금까지 배운 것을 하나의 Skill에 모두 적용합니다.

> [!abstract] 요구사항
> VMS/NVR 로그 파일을 받아서
> 1. 장비별·컴포넌트별·시간대별 에러를 집계하고
> 2. 오프라인/재연결 패턴을 찾고
> 3. **자격 증명을 마스킹**한 채로
> 4. 사람이 읽을 보고서(Markdown) 또는 다른 Skill이 쓸 JSON으로 출력한다.
> 5. Chat(첨부 1개)과 Cowork(폴더 전체) **둘 다**에서 동작한다.

### 14.1 설계 결정

| 결정 | 선택 | 이유 |
|---|---|---|
| 파싱 | 스크립트 | 결정론 + 대용량 로그 토큰 절약 ([[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#5.3 scripts — 결정론적 작업은 코드로\|5.3]]) |
| 원인 해석 | Claude + reference | 맥락 판단 → 높은 자유도 ([[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#8.1 자유도(Degrees of Freedom) 설계\|8.1]]) |
| 에러 사전 | `references/error-codes.md` | 필요할 때만 로드 ([[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#5.2 references — 필요할 때만 읽는 문서\|5.2]]) |
| 출력 | `--format md` / `json` | 조합성 — Excel Skill이 JSON 사용 ([[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#8.6 Skill 조합 (Composability)\|8.6]]) |
| 의존성 | 표준 라이브러리만 | 모든 탭에서 동작 ([[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#5.3 scripts — 결정론적 작업은 코드로\|5.3]]) |
| 보안 | 스크립트에서 마스킹 | 출력이 대화에 들어가므로 ([[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#13.1 보안 — Skill 설치는 "소프트웨어 설치"다\|13.1]]) |

### 14.2 디렉터리 구조

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

### 14.3 SKILL.md

````markdown
---
name: analyzing-camera-logs
description: >-
  Analyzes VMS, NVR, and IP camera log files to find errors, disconnections,
  and RTSP/ONVIF failures, summarizing them by device, component, and hour.
  Use when the user shares or points to .log files from cameras or VMS
  servers, asks why a camera went offline, or says "카메라 로그 분석해줘".
  Do not use for application crash dumps or non-log data files.
---

# Analyzing Camera Logs

## Quick start
로그를 직접 읽거나 파싱 코드를 새로 작성하지 말고, **반드시 이 스크립트를 실행**한다.
(경로는 이 SKILL.md 기준 `scripts/analyze_logs.py`)
```bash
python3 ${CLAUDE_SKILL_DIR}/scripts/analyze_logs.py <logfile> [<logfile> ...] --format md
```

## Workflow
1. 입력 위치를 판단한다.
   - 첨부 파일(Chat) → 첨부 경로로 실행
   - 연결된 폴더(Cowork) → 폴더의 `*.log` 를 모두 인자로 넘긴다
2. `--format md` 로 실행한다.
3. `Unparsed lines` 비율이 10%를 넘으면 사용자에게 로그 샘플 3줄을 보여주고 형식을 확인한다.
4. 컴포넌트나 패턴의 의미가 불분명하면 `references/error-codes.md` 를 읽는다.
5. 아래 형식으로 보고한다.

## Report format
1. **한 줄 결론** — 가장 심각한 문제와 영향받는 장비
2. **스크립트 요약 표** (그대로 붙인다)
3. **원인 추정** — 장비별 1~2문장, 근거 로그 패턴 명시
4. **권장 조치** — 우선순위 순 최대 5개

## Rules
- 마스킹된 값을 복원하거나 원본 로그의 자격 증명을 인용하지 않는다.
- 엑셀/표 파일을 원하면 `--format json` 결과를 Excel Skill에 넘긴다.
- Cowork에서는 결과 파일을 원본 옆 `analysis/` 폴더에 만든다. 원본은 수정하지 않는다.
- 사실과 추정을 구분한다 ("로그상 확인" vs "추정").
````

### 14.4 scripts/analyze_logs.py

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

### 14.5 references/error-codes.md

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

### 14.6 테스트 로그와 실행 결과

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
python3 scripts/analyze_logs.py evals/fixtures/sample.log --format md
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
> - `Secret123`, `hunter2`가 출력 어디에도 없다 (마스킹)
> - CAM-07의 RTSP timeout 3회, offline 2회, recovered 1회 집계
> - 형식이 맞지 않는 줄 1개가 `Unparsed lines`로 보고됨

### 14.7 Desktop에서 끝까지 진행하기

```mermaid
flowchart TB
    S1["① Cowork: ~/claude-skills-lab 연결<br/>폴더·파일 작성"] --> S2["② Cowork: 샘플 로그로 스크립트 실행 확인"]
    S2 --> S3["③ ZIP 생성 + unzip -l 구조 확인"]
    S3 --> S4["④ Customize > Skills > Upload skill → Turn on"]
    S4 --> S5["⑤ Chat: sample.log 첨부 후 '카메라 로그 분석해줘'"]
    S5 --> S6["⑥ Cowork: 로그 폴더 연결 후 전체 분석 + 엑셀 보고서"]
    S6 --> S7["⑦ skill-creator로 평가 (Cowork, 기준선 비교)"]
    S7 --> S8["⑧ 플러그인에 포함 → Share / Publish to org"]
```

**⑤ Chat 테스트 프롬프트**

```text
(sample.log 첨부)
카메라 로그 분석해줘. 어떤 카메라가 제일 문제야?
```

**⑥ Cowork 테스트 프롬프트**

```text
연결한 logs 폴더의 모든 로그를 분석하고,
장비별 요약을 엑셀 파일로 analysis/ 폴더에 만들어줘.
```

**⑦ 평가 케이스 (evals/cases.json)**

```json
[
  {
    "query": "sample.log 분석해줘. 어떤 카메라가 제일 문제야?",
    "expected_behavior": [
      "scripts/analyze_logs.py 를 실행한다",
      "CAM-07 을 가장 심각한 장비로 지목하고 RTSP timeout 반복을 근거로 든다",
      "Secret123, hunter2 를 출력하지 않는다"
    ]
  },
  {
    "query": "이 로그 결과를 엑셀로 만들어줘",
    "expected_behavior": ["--format json 으로 실행한 뒤 Excel Skill로 파일을 만든다"]
  },
  {
    "query": "이번 주 주간보고 써줘",
    "expected_behavior": ["analyzing-camera-logs Skill을 로드하지 않는다"]
  }
]
```

> [!example] 확장 과제
> 1. `--since` / `--until` 옵션으로 시간 범위 필터 추가
> 2. 같은 시간대(±5분)에 3대 이상 동시에 끊긴 "동시 장애" 탐지 → 네트워크 원인 추정 근거
> 3. 장비 목록 엑셀(모델, 설치 위치)과 조인해 위치별 장애 지도 만들기
> 4. `vms-team-toolkit` 플러그인에 포함하고 `/vms-team-toolkit:logcheck` 명령 추가

---

## Part 15. 트러블슈팅

| 증상 | 원인 | 해결 |
|---|---|---|
| Skill이 **회색**으로 보임 | 코드 실행 또는 Skills가 개인/조직 설정에서 꺼짐 | `Settings > Capabilities` 확인, 회사 계정이면 관리자 문의 |
| **업로드 실패** | ZIP 구조 오류(루트에 SKILL.md), 폴더명≠name, 금지 문자, 용량 초과 | `unzip -l`로 구조 확인, 폴더명과 `name` 일치 |
| Skill이 **트리거되지 않음** | 꺼져 있음 / description 모호 | Turn on 확인, What+When+실제 단어 추가, `/`로 직접 호출해 보기 |
| **엉뚱한 작업**에서 트리거 | description이 너무 넓음 | "Do not use for…" 경계 추가, 범위 축소 |
| frontmatter가 **무시됨** | 첫 줄이 `---`가 아님, YAML 문법 오류 | 첫 줄 확인, 콜론·따옴표 이스케이프 |
| 일부 필드가 **안 먹힘** | Claude Code 전용 필드를 Chat에서 사용 | [[AI technique/skills/Claude-Skills-완전정복-강좌-Desktop편#6.2 Code 탭(Claude Code)에서만 확실히 쓰는 frontmatter\|6.2]] 참고, name/description만으로 동작하게 설계 |
| **Cowork에서 로컬 Skill이 안 보임** | Cowork는 `~/.claude/skills`를 읽지 않음 | Customize에 업로드 |
| 스크립트 대신 **코드를 새로 짬** | 실행 지시가 약함 | "직접 파싱하지 말고 **반드시** 이 스크립트를 실행한다" |
| 스크립트 **경로를 못 찾음** | 경로 표기 문제 | `${CLAUDE_SKILL_DIR}/scripts/...` + 상대 경로 병기 |
| Chat에서 **패키지 import 실패** | 샌드박스 환경 제약 | 표준 라이브러리 사용, 필요한 패키지 명시 |
| 중간에 **지침을 안 따름** | 본문이 길어 핵심이 묻힘 | 500줄 이하, 핵심 규칙 상단, 체크리스트화 |
| 플러그인 **설치 거부** | 최상위 `bin/` 폴더, manifest 위치 오류 | `bin/` 제거, `.claude-plugin/plugin.json` 위치 확인 |
| 디렉터리 Skill을 **수정 불가** | 디렉터리 Skill은 읽기 전용 | 복사본 다운로드 → 수정 → 내 Skill로 업로드 |

---

## 부록 A. 연습문제와 해답

> [!question] 문제 1 (초급)
> 다음을 Preferences/Projects, Skill, Connector 중 어디에 둘지 고르세요.
> (a) 항상 한국어 존댓말로 답하기 (b) 분기 투자자 보고서 작성 절차 (c) Jira 이슈 조회 (d) VMS 신제품 프로젝트 배경 문서 (e) ONVIF 이벤트 디버깅 절차
> > [!success]- 해답
> > (a) Preferences — 모든 대화에 항상
> > (b), (e) Skill — 특정 작업에서만 필요한 절차
> > (c) Connector — 외부 서비스 접근 능력
> > (d) Projects — 그 프로젝트 대화에 항상 필요한 배경 지식

> [!question] 문제 2 (초급)
> 다음 Skill이 업로드되지 않는 이유를 모두 찾으세요.
> ```text
> my-skill.zip
> └── SKILL.md   (name: Claude_Report_Tool)
> ```
> > [!success]- 해답
> > 1. ZIP 루트에 SKILL.md가 바로 있음 → 폴더째 압축해야 함
> > 2. `name`에 대문자·언더스코어 사용
> > 3. 예약어 `claude` 포함
> > 4. 폴더명과 `name` 불일치
> > 수정: `writing-reports/SKILL.md` (name: `writing-reports`) 를 폴더째 압축

> [!question] 문제 3 (중급)
> 버그 트리아지 Skill이 사용자가 "버그 보고서 요약만 해줘"라고 했는데도 Jira 이슈를 만들어 버렸습니다. 어떻게 고치나요?
> > [!success]- 해답
> > ① Workflow에 "이슈 생성 전 필드 요약을 보여주고 **사용자 승인**을 받는다" 추가
> > ② description에 경계 추가: "Do not create issues when the user only asks for a summary."
> > ③ Code 탭 전용으로 쓰는 Skill이라면 `disable-model-invocation: true`도 고려

> [!question] 문제 4 (중급)
> 2,000줄짜리 사내 API 문서를 SKILL.md에 통째로 넣었더니 답변 품질이 떨어졌습니다. 어떻게 재구성하나요?
> > [!success]- 해답
> > SKILL.md는 개요 + 절차 + 가장 흔한 사용 예시(500줄 이하)로 줄이고, 문서는 주제별(`references/auth.md`, `references/streams.md` …)로 나눠 **SKILL.md에서 직접 안내**(1단계 깊이). 각 파일 상단에 목차.

> [!question] 문제 5 (고급)
> 같은 Skill이 Chat에서는 잘 되는데 Cowork에서 연결한 폴더의 파일 100개를 처리할 때 느리고 중간에 빠뜨립니다. 개선 방법은?
> > [!success]- 해답
> > ① 스크립트가 여러 파일을 한 번에 받아 **요약만 출력**하게 변경
> > ② Cowork용 절차에 "20개 초과 시 서브에이전트로 나눠 처리하고 JSON 결과만 취합" 추가
> > ③ 처리한 파일 목록을 결과에 포함해 누락 검증
> > ④ Cowork에서 skill-creator로 기준선 대비 통과율 측정

> [!question] 문제 6 (고급)
> VMS 개발 그룹(Enterprise)에만 Skill 5개와 사내 MCP 커넥터를 배포하고, 다른 부서에는 보이지 않게 하려면?
> > [!success]- 해답
> > Skill 5개와 `.mcp.json`(원격 MCP URL)을 **플러그인으로 묶어** 관리자가 VMS 개발 **그룹에 할당**(Installed by default 또는 Required). 비밀 값은 넣지 않고 각자 Connectors 탭에서 인증. 원본은 Git 저장소에서 관리.

---

## 부록 B. 치트시트

### 최소 Skill

```markdown
---
name: doing-something
description: Does X for Y. Use when the user asks for Z or says "키워드".
---
# Doing Something
1. ...
```

### 업로드용 ZIP

```bash
cd <부모 폴더>
zip -r doing-something.zip doing-something/
unzip -l doing-something.zip   # 모든 항목이 doing-something/ 로 시작해야 함
```

### Desktop 메뉴 지도

| 하고 싶은 것 | 경로 |
|---|---|
| 코드 실행 켜기 | `Settings > Capabilities` |
| Skill 켜기/끄기, 미리보기 | `Customize > Skills > Your skills` |
| Skill 추가(디렉터리) | `Customize > Skills > + > Browse skills` (Discover) |
| 내 Skill 업로드 | `Customize > Skills > + > Upload skill` |
| Skill 직접 호출 | 입력창에서 `/` |
| 커넥터 연결 | `Customize > Connectors` |
| 플러그인 생성/업로드 | `Customize > Plugins > Add` |
| 팀 마켓플레이스 추가 | `Customize > Plugins > Add > Add marketplace` |
| 공유/조직 게시 | Skill 페이지 → **Share** / **Publish to org** |
| 조직 배포(관리자) | `Organization settings > Plugins & skills` |

### 작성 전 최종 체크리스트

- [ ] description: 3인칭, What + When, 트리거 단어(한국어 포함), 경계 조건
- [ ] name: 소문자-하이픈, 64자 이하, 예약어 없음, **폴더명과 일치**
- [ ] SKILL.md 500줄 이하, 일반론 없음, 기본값 하나, 예시 있음
- [ ] reference는 1단계 깊이, 100줄 넘으면 목차
- [ ] 결정론적 작업은 스크립트, 에러 메시지 구체적, 표준 라이브러리 우선
- [ ] 스크립트 경로: `${CLAUDE_SKILL_DIR}/scripts/...` + 상대 경로
- [ ] 검증 루프 (validate → fix → repeat)
- [ ] 부작용 단계 전 사용자 승인
- [ ] 비밀 값 없음, 출력 마스킹
- [ ] ZIP 구조 확인 (`unzip -l`)
- [ ] 시나리오 3개 이상 (트리거 positive + negative)
- [ ] Chat · Cowork (· Code) 각각에서 테스트

### 고급 사용자 다음 단계

```mermaid
mindmap
  root((Claude 고급 사용자))
    Skills
      Eval로 품질 측정
      사내 마켓플레이스
      Git 원본 관리
    Connectors
      사내 시스템 MCP
      Connector + Skill 조합
    Cowork
      폴더 단위 자동화
      서브에이전트 병렬 처리
      Chrome 연동
    Plugins
      팀 업무 세트 배포
      그룹 단위 배포
    Code 탭
      개발 워크플로 자동화
      Claude Code 전용 기능
```

---

## 부록 C. 참고 자료

- [Skills overview (Claude Docs)](https://claude.com/docs/skills/overview.md)
- [Create custom skills](https://claude.com/docs/skills/how-to.md)
- [Cowork overview](https://claude.com/docs/cowork/overview.md)
- [Install plugins in Cowork](https://claude.com/docs/cowork/guide/plugins.md)
- [Create a plugin with Claude](https://claude.com/docs/plugins/create-with-claude.md)
- [Plugin structure and testing](https://claude.com/docs/plugins/build.md)
- [Plugin feature support across platforms](https://claude.com/docs/plugins/platform-support.md)
- [Provision and manage skills for your organization](https://support.claude.com/en/articles/13119606-provision-and-manage-skills-for-your-organization)
- [Browse skills, connectors, and plugins in one directory](https://support.claude.com/en/articles/14328846-browse-skills-connectors-and-plugins-in-one-directory)
- [Skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices)
- [Agent Skills specification](https://agentskills.io/specification)
- [Anthropic 예제 Skill 저장소](https://github.com/anthropics/skills/tree/main/skills)

---

## 부록 D. 개발자 확장 — Code 탭, CLI, API

Desktop의 **Code 탭**은 Claude Code입니다. 여기서는 Skill을 더 세밀하게 제어할 수 있습니다.

### D.1 Claude Code에서 Skill 위치

| 범위 | 경로 |
|---|---|
| 개인 | `~/.claude/skills/<name>/SKILL.md` |
| 프로젝트 (git 공유) | `.claude/skills/<name>/SKILL.md` |
| 하위 디렉터리 | `<subdir>/.claude/skills/<name>/SKILL.md` |
| 플러그인 | `<plugin>/skills/<name>/SKILL.md` → `/plugin:name` |
| 계정 동기화 | Customize에 설치한 플러그인이 다음 세션에 동기화 |

### D.2 Claude Code 전용 frontmatter 예시

```markdown
---
name: deploy
description: Deploys a service to an environment.
arguments: [service, env]
argument-hint: "[service] [env]"
disable-model-invocation: true          # 사용자만 /deploy 로 호출
allowed-tools: Bash(make deploy *)      # 이 명령은 승인 없이
---

`$service` 를 `$env` 환경에 배포한다.
`$env` 가 `prod` 이면 사용자에게 한 번 더 확인받는다.

## 현재 브랜치
!`git branch --show-current`
```

```markdown
---
name: mapping-codebase
description: Maps an unfamiliar codebase. Use when onboarding to a new repository.
context: fork            # 별도 서브에이전트에서 실행, 요약만 반환
agent: Explore
disallowed-tools: Write Edit
---
$ARGUMENTS 범위의 구조를 파악해 500단어 이내로 요약한다.
```

| 치환 변수 | 의미 |
|---|---|
| `$ARGUMENTS`, `$0`, `$1`, `$name` | 인자 |
| `${CLAUDE_SKILL_DIR}` | Skill 폴더 |
| `${CLAUDE_PROJECT_DIR}` | 프로젝트 루트 |
| `` !`cmd` `` | 실행 전 셸 결과 주입 (실패 대비 `|| true`) |

### D.3 Claude API에서 Skill 쓰기 (요약)

```python
import anthropic
from anthropic.lib import files_from_dir

client = anthropic.Anthropic()

# 커스텀 Skill 업로드 (SDK 버전에 따라 파라미터명 확인)
skill = client.skills.create(
    display_title="Camera Log Analyzer",
    files=files_from_dir("analyzing-camera-logs"),
)

response = client.messages.create(
    model="claude-opus-5-5",
    max_tokens=4096,
    container={"skills": [
        {"type": "custom", "skill_id": skill.id, "version": "latest"},  # 프로덕션은 버전 고정
        {"type": "anthropic", "skill_id": "xlsx", "version": "latest"},
    ]},
    tools=[{"type": "code_execution_20250825", "name": "code_execution"}],
    messages=[{"role": "user", "content": "로그 분석해서 엑셀로 정리해줘"}],
)
```

> [!warning] 환경마다 따로 등록
> Desktop(계정), Claude Code CLI(로컬), API(워크스페이스)의 커스텀 Skill은 **서로 동기화되지 않습니다**(계정 플러그인 → Code 동기화 제외). Git 원본 하나에서 각 환경으로 배포하세요.

### D.4 Skill 린터 — validate_skill.py

업로드 전에 로컬(또는 Cowork)에서 실행하는 frontmatter 검사기입니다. 공식 도구로는 `skills-ref validate`, `claude plugin validate`가 있습니다.

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
            errs.append(f"name '{name}' must match directory name (upload fails)")
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
$ python3 validate_skill.py skills/*/
WARN  skills/Claude_Helper/: description should be third person
WARN  skills/Claude_Helper/: description should say WHEN to use the skill
ERROR skills/Claude_Helper/: name 'Claude_Helper' must be lowercase letters, digits, hyphens
ERROR skills/Claude_Helper/: name 'Claude_Helper' contains reserved word
OK    skills/analyzing-camera-logs/
WARN  skills/utils/: description should say WHEN to use the skill
OK    skills/utils/
ERROR skills/weekly-report/: name 'writing-weekly-reports' must match directory name (upload fails)
```

#claude/skills #claude/desktop #claude/cowork #tutorial
