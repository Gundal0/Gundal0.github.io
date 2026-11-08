---
{"dg-publish":true,"permalink":"/ai-technique/skills/skills/","dg-note-properties":{}}
---

# skills 마스터 시리즈 — 전체 목차

## 1. skill의 정의
- [ ] skill은 AI agent에게 명령을 내릴 때마다 반복적으로 전달하는 내용을 규칙으로 설정하여 기본 설정으로 만드는 방법이다.
- [ ] 지침([SKILL.md](http://skill.md/)), 참고 문서, 스크립트, 템플릿을 하나의 폴더로 묶은 것으로, Claude가 관련 작업을 만났을 때 스스로 불러와 사용하는 전문 기술 모듈입니다.
- [ ] 비유하자면, 프롬프트가 "오늘 할 일에 대한 지시"라면 Skill은 "회사의 업무 매뉴얼 바인더"입니다. Claude는 바인더의 목차(이름과 설명)만 항상 기억하고, 필요할 때만 해당 장을 펼쳐 읽습니다.

## 2. 핵심 원리: 점진적 공개
```mermaid
flowchart LR
    A["① 메타데이터<br/>name + description<br/>(항상 로드, 수십 토큰)"] -->|관련 작업 감지| B["② SKILL.md 본문<br/>(필요할 때 로드)"]
    B -->|더 자세한 정보 필요| C["③ 참고 파일·스크립트<br/>(요청 시에만 읽거나 실행)"]
```

```mermaid
flowchart LR
    A["① YAML 메타데이터<br/>name + description<br/>(항상 로드, 수십 토큰)"] -->|해당되는 작업이라고 감지되었을 때| B["② SKILL.md 본문<br/>(필요할 때 로드)"]
    B -->|더 자세한 정보 필요할 때| C["③ 참고 파일·스크립트<br/>(요청 시에만 읽거나 실행)"]
```

> [!abstract] skill의 구성
> 모든 skill은 name과 description으로 구성된다.
> name: name of skill
> description: explaination about this skill
> ---
> 이 구조때문에 수십개의 skill을 설치해도 컨텍스트를 거의 차지하지 않습니다. 그래서 description을 잘 쓰는 것이 skill 품질의 절반입니다.
> claude는 description만 보고 이 skill을 언제 사용할지 결정합니다.

## 3. skill의 폴더 구조

weekly-report/
├── SKILL.md            # (필수) 메타데이터 + 지침
├── reference/
│   ├── style-guide.md  # 필요할 때만 읽는 상세 자료
│   └── examples.md
├── templates/
│   └── report.docx     # 결과물 템플릿
└── scripts/
    └── build_chart.py  # Claude가 실행하는 스크립트


## 4. skill.md 작성하기
`skill.md`는 맨 위의 YAML 프론트메타와 아래의 markdown 본문으로 구성됩니다.

```markdown
---
name: weekly-report 
description: 팀의 주간 업무 보고서를 회사 표준 양식으로 작성한다. 사용자가 "주간 보고", "위클리 리포트", "이번 주 업무 정리"를 요청하거나 업무 목록을 보고서로 만들어 달라고 할 때 사용한다.
---

# 주간 보고서 작성 

## 절차 
1. 사용자에게서 이번 주 업무 목록을 받는다. 없으면 연결된 도구(Jira, 캘린더)에서 찾는다. 
2. 업무를 "완료 / 진행 중 / 이슈" 세 범주로 분류한다. 
3. `reference/style-guide.md` 의 문체 규칙을 따라 작성한다. 
4. 수치 데이터가 있으면 `scripts/build_chart.py` 를 실행해 차트를 만든다. 
5. `templates/report.docx` 양식에 맞춰 Word 파일로 출력한다. 

## 규칙 
- 각 항목은 "무엇을 했고 → 결과는 무엇이며 → 다음은 무엇"의 구조로 쓴다. 
- 이슈에는 반드시 필요한 지원과 기한을 적는다. 
  
## 예시 
자세한 예시는 `reference/examples.md` 를 참고한다.
```

