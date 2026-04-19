# 환경설정
## 사용자 설정(전역 단위 설정)
- `~./claude/settings.json` 에 정의되고, 모든 프로젝트에 적용되는 설정 파일
- 모든 프로젝트에 적용되었으면 하는 claude setting을 명시

## 프로젝트 폴더 단위로 설정
## 1. settings.json
- 팀과 공유하는 설정 파일
- 예시:
`{
    "plansDirectory":".claude/plans/",
    "allow":[]
}`


## 2. settings.local.json
- 사용자 개인선호도에 맞는 설정들을 명시
- 예시:
`
{"permissions": {
    "allow": [
      "Read(//private/tmp/**)",
      "Bash(unzip -q /Users/hyeongdohun/Documents/claude-code-gym/portfolio.pptx -d portfolio_extracted)"
    ]
  },
  "outputStyle": "Intermediate AI Engineer"
}`


# CLAUDE.md
- 프로젝트, 개인 워크플로우 또는 전체 조직에 대해 Claude에 지속적인 지침을 제공하는 마크다운 파일  
- 주로 작성하는 내용 : 코드 스타일, Git 규칙, 작업 방식 등등

## Anthropic 에서 제시하는 효과적인 CLAUDE.md 파일 작성 규칙
- 반드시 지켜야 하는 중요한 내용에는 [IMPORTANT], [MUST], [중요] 등을 명시해줄 것!
- CLAUDE.md 의 내용은 200자 이내로 작성하는 것을 권장함(너무 길어지면, 컨텍스트를 많이 차지함).
- CLAUDE.md 파일이 너무 길어지는 경우, `@` 를 활용해서 추가 파일들을 임포트 해오는 구조로 작성하여, 길이를 줄일 수 있다.
- 구체적으로 작성, 구조적으로 작성(마크다운 형식에 맞게 작성)

## ./claude/rules/
### 배경
- 기존에는 CLAUDE.md 파일이 길어지는 것을 방지하기 위해서 `@` 문법을 통해서 외부의 파일들을 임포트하는 식으로 CLAUDE.md 파일의 내용을 줄이고자 하였다.

### 문제점
- CLAUDE.md 파일에 적용되는 규칙을 변경하고 싶을 때마다, CLAUDE.md 자체를 고치거나, CLAUDE.md 파일에 임포트 되어있는 `@` 문법으로 임포트되는 파일들에 적힌 규칙들을 변경해야 했음.
- 특정 규칙을 특정 디렉토리에만 적용하고 싶은 경우가 있는데, CLAUDE.md 파일 하나에서 메모리를 모두 관리하다보니, 특정 디렉토리에 특정 규칙을 적용시키기가 어려웠음.

### 해결방안 - 규칙 설정
- `./claude/rules` 를 통해 특정 파일 경로별로 지침을 별도로 지정 및 관리할 수 있음.
`
your-project/
├── .claude/
│   ├── CLAUDE.md           # 주 프로젝트 지침
│   └── rules/
│       ├── code-style.md   # 코드 스타일 가이드라인
│       ├── testing.md      # 테스트 규칙
│       └── security.md     # 보안 요구사항
`

- 프로젝트의 `.claude/rules` 디렉토리에 마크다운 파일들을 배치하고, 각 파일들은 code-style.md, testing.md 등과 같은 한 가지 주제에 대한 규칙들을 다루도록 작성해야 함.

### 특정 경로의 특정 파일에 특정 규칙을 적용하고자 하는 경우
- YAML Frontmatter 부분의 paths에 파일 이름을 지정하여, 규칙을 적용하고자 하는 파일을 지정해줄 수 있음.
```
---
paths:
  - "src/api/**/*.ts"
---

# API 개발 규칙

- 모든 API 엔드포인트는 입력 검증을 포함해야 합니다
- 표준 오류 응답 형식을 사용합니다
- OpenAPI 문서 주석을 포함합니다
```

### `.claude/rules/`의 모범 사례
- 규칙 집중 : 각 파일은 하나의 주제를 다루어야함.
- 설명적인 파일명 사용: 파일명은 규칙이 다루는 내용을 나타내야함.
- 조건부 규칙을 드물게 사용함: 규칙이 특정 파일 유형에 정말로 적용될 때만 paths 프론트매터를 추가.
- 서브디렉토리로 구성 : 관련된 규칙들은 그룹화할 것.

## Automemory
- 사용자가 아닌, Claude가 자체적으로 기록하는 메모리
- `~./.claude/{프로젝트 폴더}/{세션}/memory/MEMORY.md` 에 저장되어 있음.