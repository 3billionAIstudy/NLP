## 요약
- colbert is a new paradigm for IR;InformationRetrieval
- speed up vector search(170x faster, 14,000x fwer FLOPs/query)
## IR;InformationRetrieval
- basic schema: colbert

  ![image](https://github.com/3billionAIstudy/NLP/assets/126950833/d243e4b1-ed82-456c-aa29-234c19855d44)
  
- how to deal with long texts?
  - passaging: split into smaller texts
  - 학습 단계에서는 긴 문서(long doc)가 관련성 있다고 판단되면 각각의 패시지도 관련성 있는 것으로 취급됨
  - 이 경우에 aggregation function을 정의하는 방법은 여러가지가 있음: FirstP(첫 번째 패시지의 스코어를 문서 전체의 스코어로 보는 방법), MaxP(패시지 스코어 최댓값), SumP(ㅎㅎ)
## Vector search
- typical IR system schema
  ![image](https://github.com/3billionAIstudy/NLP/assets/126950833/78f68bf1-9201-4980-80fa-d89583a6b80b)
- how to find the top-1 similar?
  - ANN;ApproximateNearestNeighbor algorithm
  - special index: IVFPQ, etc.
  - HNSW: Hierarchical Navigable Small World Graphs
## ColBERT: Contextualized Late Interaction over BERT
- 기존 방법론(위 그림 2-c)에서는 `query`와 `document`의 유사도 계산을 하기 위해 필요한 계산복잡도가 너무 컸음
  - `query` 자신의 interaction(***within q***)과 `query-document` interaction을 모두 계산해야 함.
  - (Q) 않이 근데 document가 엄청 많은데 이걸 쿼리 들어올 때마다?!
## Refs
- [Lecture Notes on Neural Information Retrieval](https://arxiv.org/pdf/2207.13443.pdf)
- [Efficient and Effective Passage Search via Contextualized Late Interaction over BERT](https://arxiv.org/pdf/2004.12832.pdf)
- [A White Box Analysis of ColBERT](https://arxiv.org/pdf/2012.09650.pdf)
- [Neural Information Retrieval: article](https://medium.com/@blogsupport/neural-information-retrieval-google-bert-6ce3cbabf7ff)
- [네이버 DEVIEW2021 발표 영상](https://tv.naver.com/v/23650668)



