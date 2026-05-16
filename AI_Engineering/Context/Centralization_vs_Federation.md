# 기업용 AI의 핵심: Glean의 중앙 집중형 인덱싱과 MCP 성능 분석

**AI가 질문을 받았을 때 비로소 정보를 찾으러 떠나는 것(Federated MCP Call)보다, 이미 사내의 모든 정보가 누구와 어떻게 연결되어 있는지 '계보도'를 그리고 이를 기반으로 정보를 찾는 것이(Cetralized MCP Call) 훨씬 빠르고 정확하게 답할 수 있다.**

## 1. 핵심 내용 요약
* **주제:** AI 에이전트(Claude Cowork 등)의 실질적 성능은 모델 자체보다 **데이터 컨텍스트(Context Layer)**를 어떻게 제공하느냐에 결정됨.
* **Glean의 강점:** 모든 사내 데이터를 미리 통합하여 **지식 그래프(Knowledge Graph)**를 구축하는 방식이 일반적인 실시간 앱 연동 방식보다 압도적 효율을 보임.
* **주요 성과:** 일반 MCP 서버 대비 **사용자 선호도 2.5배**, **토큰 비용 30% 절감**, 복잡한 작업 수행 능력 **73% 달성**.

---

## 2. 구체적인 내용

### ① 기술 구조의 차이: 페더레이션 vs. 중앙 집중형 인덱싱
* **일반 MCP (Federated Search):** AI가 필요할 때마다 각 앱(Slack, Drive 등)에 개별적으로 검색을 요청.
    * 검색 품질이 각기 다르고, 모델이 여러 답변을 직접 취합해야 하므로 '토큰 세금(Token Tax)'이라 불리는 비용과 지연이 발생함.
* **Glean (Centralized Indexing):** 수백 개의 엔터프라이즈 앱 데이터를 사전에 수집 및 정규화하여 하나의 **Graph 기반 지식 레이어** 구축.
    * 단순 텍스트를 넘어 사람, 팀, 문서 간의 관계를 인덱싱하여 모델에 가장 정교한 맥락을 한 번에 전달함.


### ② 지식 그래프(Knowledge Graph)의 상세 구성
Glean은 단순히 텍스트를 저장하는 것이 아니라, 데이터 간의 **'맥락적 연결 고리'**를 인덱싱합니다.

* **구성 요소 (Nodes & Edges):**
    * **엔터티(점):** 문서(Notion, Drive), 메시지(Slack), 사람(임직원), 팀, 프로젝트, Jira 티켓 등.
    * **관계(선):** "누가 작성했는가?", "어느 채널에서 언급되었는가?", "누가 이 문서의 전문가인가?", "사용자에게 열람 권한(ACL)이 있는가?"
* **구축 방식:**
    1. **정규화:** 다양한 SaaS 앱의 데이터를 Glean 표준 모델로 통합.
    2. **교차 신호 추출:** 서로 다른 앱(예: Gmail 요청 -> Jira 티켓 생성) 간의 연관 관계 파악.
    3. **지능형 랭킹:** 나와 협업하는 사람이 만든 최신 문서 등 그래프상의 거리를 계산해 우선순위 부여.

### ② 벤치마크 결과 (Glean vs. Off-the-shelf MCP)
[Glean](https://www.glean.com/blog/cowork-mcp-eval?utm_source=aiengineering.beehiiv.com&utm_medium=referral&utm_campaign=train-llm-25-faster-without-touching-the-kernels)이 Claude Sonnet 3.5 모델을 통해 실시한 실험 결과는 다음과 같습니다.

| 평가 항목 | Glean (Remote MCP) | 일반 MCP 도구 |
| :--- | :--- | :--- |
| **사용자 선호도** | **약 2.5배 높음** | 낮음 |
| **평균 토큰 사용량** | **44k (안정적)** | 57k (비효율적) |
| **복잡한 작업 승률** | **73%** | 27% |
| **최대 토큰 소모** | **43k** | 83k (정답을 찾기 위해 불필요한 루프 반복) |

### ③ 인덱싱 기술이 업무에 미치는 영향
* **비용 절감:** 검색 정확도가 낮으면 모델은 정답을 찾기 위해 여러 번 도구를 호출하며 추론 비용을 낭비함. Glean은 첫 호출에서 정답에 가까운 정보를 제공해 이를 방지함.
* **업무 준비도(Work-ready):** 뉴스레터 제작이나 장애 분석(SSAT Alert) 시, Glean은 단순 파일 조회를 넘어 관련 고객사 현황과 Slack의 논의 맥락까지 포함하여 바로 사용 가능한 수준의 결과물을 생성함.
* **보안 및 권한:** 기업 내 복잡한 접근 권한(ACL)을 실시간으로 반영하여 사용자가 볼 권한이 있는 정보만 안전하게 인덱싱함.

---

## 3. Reference
* **Glean Official Blog:** [Glean vs. Off-the-Shelf MCP Benchmark](https://www.glean.com/blog/cowork-mcp-eval?utm_source=aiengineering.beehiiv.com&utm_medium=referral&utm_campaign=train-llm-25-faster-without-touching-the-kernels)
* **AI Engineering Newsletter:** [Centralized Context Made Claude Cowork 10x Better](https://aiengineering.beehiiv.com/p/train-llm-25-faster-without-touching-the-kernels?utm_source=aiengineering.beehiiv.com&utm_medium=newsletter&utm_campaign=train-llm-25-faster-without-touching-the-kernels&_bhlid=d32c6ae338cd71fa492fe49681428b6a6aeb10af)