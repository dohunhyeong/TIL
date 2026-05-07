# Seven Failure Points When Engineering a Retrieval Augmented Generation System
[link](https://arxiv.org/abs/2401.05856)
📑 RAG 시스템의 7가지 실패 지점 (Failure Points)

## Summary
논문은 RAG 프로세스를 크게 색인(Index), 쿼리(Query), 생성(Generation) 단계로 나누고, 각 단계에서 발생할 수 있는 문제점을 정의합니다.


## 주요 실패 요인 7가지 
1. Missing Content (콘텐츠 누락)
- 문제: 질문에 대한 답이 문서 저장소(Knowledge Base)에 존재하지 않는 경우입니다.
- 결과: 모델이 "모른다"고 답하거나, 최악의 경우 허위 정보(Hallucination)를 생성합니다.

2. Missed the Top Ranked Documents (검색 실패)
- 문제: 답이 문서에 있음에도 불구하고, 검색 알고리즘이 관련 문서를 상위 결과(Top-k)에 포함하지 못하는 경우입니다.
- 원인: 부적절한 임베딩 모델 사용이나 검색 쿼리의 모호성 등이 원인이 될 수 있습니다.

3. Not in Context - Consolidation Strategy (컨텍스트 한계)
- 문제: 관련 문서를 찾았지만, 모델에 전달하는 컨텍스트 창(Context Window)에 포함되지 않거나 순위가 밀려 무시되는 경우입니다.
- 현상: "중간 손실(Lost in the Middle)" 현상처럼 문서의 양이 너무 많을 때 발생하기 쉽습니다.

4. Not Extracted (정보 추출 실패)
- 문제: 답이 컨텍스트 안에 포함되어 있음에도 불구하고, LLM이 복잡한 내용 속에서 정확한 정보를 찾아내지 못하는 경우입니다.
- 원인: 컨텍스트 내에 노이즈(불필요한 정보)가 너무 많거나 상충하는 정보가 있을 때 발생합니다.

5. Wrong Format (잘못된 형식)
- 문제: 답변 내용은 맞지만, 사용자가 요구한 특정 형식(예: JSON, 표, 특정 언어 등)을 따르지 않는 경우입니다.

6. Incorrect Specificity (부적절한 구체성)
- 문제: 답변이 너무 일반적이어서 유용하지 않거나, 반대로 너무 지엽적인 정보만 제공하는 경우입니다.
- 원인: 사용자의 질문 의도를 정확히 파악하지 못해 발생합니다.

7. Incomplete (불완전한 답변)
- 문제: 질문이 복합적인 정보를 요구할 때, 일부 정보만 제공하고 나머지를 누락하는 경우입니다. (예: "A와 B의 차이점을 알려줘"라는 질문에 A만 설명하는 경우)