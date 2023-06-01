## 요약
- colbert is a BERT based ranking model for IR;InformationRetrieval
- speed up vector search(170x faster, 14,000x fwer FLOPs/query)
## IR;InformationRetrieval
- basic schema

- how to deal with logn texts?
  - passaging: split into smaller texts
  - 학습 단계에서는 긴 문서(long doc)가 관련성 있다고 판단되면 각각의 패시지도 관련성 있는 것으로 취급됨
  - 이 경우에 aggregation function을 정의하는 방법은 여러가지가 있음: FirstP(첫 번째 패시지의 스코어를 문서 전체의 스코어로 보는 방법), MaxP(패시지 스코어 최댓값), SumP(ㅎㅎ)
## ColBERT: Contextualized Late Interaction over BERT
- 
## Refs
- [Lecture Notes on Neural Information Retrieval](https://arxiv.org/pdf/2207.13443.pdf)
- [Efficient and Effective Passage Search via Contextualized Late Interaction over BERT](https://arxiv.org/pdf/2004.12832.pdf)
- [A White Box Analysis of ColBERT](https://arxiv.org/pdf/2012.09650.pdf)
- [Neural Information Retrieval: article](https://medium.com/@blogsupport/neural-information-retrieval-google-bert-6ce3cbabf7ff)



