# Prompt Engineering

## Prompt
- Instruction 과 Context로 구분지을 수 있음.
- Instruction은 모델에 대한 지시사항을 나타냄.
- Context는 모델이 지시사항을 이행하는데에 도움이 될만한 백그라운드 정보들을 나타냄.

## PromptEngineering이란?
- 단순히 질문을 하기 위한 것이 아니라, 얼마나 잘 질문을 할 것인가를 목표로 하는 Engineering
- 즉, LLM으로부터 보다 정확한 답변을 얻기 위해서 LLM이 잘 이해할 수 있도록 질문을 하는 전과정을 의미함.

# Advanced Method of PromptEngineering
## Zero-shot Prompt
- LLM에 아무런 학습과 예시 없이, Task를 수행하도록 하는 프롬프팅 기법
- 예시:  
```markdown
Classify the following statement as True or False:   
The Eiffel Tower is located in Berlin   
```

## Few-Shot Prompt
- LLM에게 몇 개의 예시를 컨텍스트로 주고, 그와 유사한 Task를 수행하도록 하는 프롬프팅 기법.


## CoT (Chain-Of-Thought)
- LLM이 복잡한 추론 과정을 **단계적으로** 수행하도록 하는 프롬프팅 기법.
- 예시:   
```markdown   
Consider the problem : A store had 22 apples. They sold 15 apples today and got a new delivery of 8 apples. How many apples are there now?
**Break down** eack step of your calculation
```

## Self-Consistency (자기 일관성)
- 모델 출력의 신뢰성과 정확성을 향상시키는 기법.
- 동일한 질문에 대한 독립적인 답변을 여러 개 생성한 다음 이를 평가하여 가장 일관된 결과를 결정하는 작업이 포함됨.
- 예시:   
```markdown
when I was 6, my sister was half of my age. Now I am 70, what age is my sister?   
Provide **three independent calculations and explanations**, then determine the most consistent result
```