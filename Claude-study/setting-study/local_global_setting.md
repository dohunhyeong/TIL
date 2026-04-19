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