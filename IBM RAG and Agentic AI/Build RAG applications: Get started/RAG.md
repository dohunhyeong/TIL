# why RAG? 

## 기존 LLM의 문제점
1. 최신 정보가 답변에 반영되지 않는다.
2. LLM 모델별로 학습에 사용된 내용 이외의 내용에 대해서는 답변하지 못한다.

## RAG
### RAG란 무엇인가?
- RAG는 Retrieval Augmented Generation의 약자로, 검색 증강 생성을 의미한다. 즉, RAG는 기존 LLM 이 가진 문제를 해결하기 위해서 LLM을 Fine-tuning하지 않은 채, Domain-specific, Up-to-Date, External 한 컨텍스트들에 대한 답변이 가능하도록 만든 프레임워크이다.

### RAG 아키텍쳐
1. 벡터 스토어 구성
- LLM에 추가적으로 알려주고 싶은 내용들을 담고있는 문서들(pdf, md, hwp 등등)을 임베딩하여 벡터 스토어를 만든다.

2. Retrieval(검색)
- user의 query를 임베딩한 후, 이 벡터와 유사한 벡터를 벡터스토어에서 검색한다.
- 검색된 벡터의 내용은 user의 query와 결합되어 증강(Augmented)된다.

3. Model Generation
- user query + augmented vector's Content 되어 LLM 에게 전달되고, LLM은 이에 대한 답변을 생성한다.