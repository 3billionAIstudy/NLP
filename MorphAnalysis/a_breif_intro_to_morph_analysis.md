## 형태소 분석이란?
- **(형태소?)** 의미가 유지되는 최소 단위.
- **(형태소 분석?)** 어근, 접두/접미사 품사 등 다양한 언어적 속성의 구조를 파악하는 것.
  - 구체적으로, 문장을 형태소로 분리, 불규칙 용언/탈락/축약 등으로 변형된 단어의 원형 복원, 각 형태소의 품사 인식 
  - **형태소 사전**과 **결합제약** 규칙에 의해
- 예시
![image](https://user-images.githubusercontent.com/126950833/234180945-28fb72f7-1357-46e1-b8b0-82e106b733c3.png)

## 형태소 분석이 왜 필요한가(한국어 자연어 처리가 특히 어려운 이유)?
- 우리말은 **교착어**임.
  - [교착어?](https://namu.wiki/w/%EA%B5%90%EC%B0%A9%EC%96%B4): 어근에 접사가 붙어서 의미가 변하는 언어. **단어의 위치는 덜 중요**함. 
  - 그럼 영어는? 굴절어(단어의 **형태**에 따라 의미가 변화)에서 고립어(**어순**에 따라 의미가 변화)로 진화. 양자의 특성을 모두 갖고 있음. ~~핵노근본ㅎ..~~
  - 아래 예시에서 한국어가 얼마나 고오오급 언어임과 동시에 처리하기 어려운 언어인지 알 수 있음. 단어 4개 조합에서 나오는 문장 12개가 같은 의미
  ![image](https://user-images.githubusercontent.com/126950833/234159602-0ead4883-744e-4809-9b81-927a83843567.png)

- **데이터 전처리** 관점에서 형태소 분석
  - 가령 어떤 문장에서 **유전자**를 추출하는 개체명 인식기가 있다고 할 때: **유전자**는 **명사**이므로, 어떤 문장 성분이 명사가 아닌 경우에는 유전자가 아닐 가능성이 높음.
  - 다음 단어가 등장할 확률을 가지고 현재 단어로부터 문장을 생성하는 **히든마코프모델**을 예로들면, 전이 확률 P(유전자|(명사 외의 품사) ~=0
  - 영어 문장이라면 품사 태깅(POS tagging: Part of Speech tagging)만 해도 큰 도움이 될 것. 
  - 한국어라면? 마치 프리미티브 타입(Primitive type)이 없고 런타임에 오브젝트-값이 바인딩 되는 파이썬처럼, **접사**에 의해 의미가 바뀜. -> 근데 이제 이게 엄청 다양한 조합으로...
  - 어근을 찾아서 사전을 구축하는 방법이 가장 쉽게 떠올릴 수 있는 방법이지만(...)
  ![image](https://user-images.githubusercontent.com/126950833/234161882-6499981d-e46a-4b59-84e1-d085f509d263.png)
  - **모호성 문제**
    - 형태소 분석은 문장을 **형태소열**로 나누고 각각의 형태소를 부여하는 과정임: 시퀀스 라벨링(sequence labeling) 문제로 볼 수 있음. 근데 시퀀스 라벨링을 하려면 일단 시퀀스가 적당히 쪼개져(=단어 또는 형태소 기준으로) 있어야 할텐데?!
    - "서울대공원"을 예로들면: 서울대+공원 또는 서울+대공원 모두 가능. 즉, 영어처럼 띄어쓰기 기준으로  나누는게 좋은 선택이 아님.
    - "나누는" 문제를 시퀀스 세그맨테이션(sequence segmentation), 나누고 나서 무슨 형태소인지 맞추는 문제를 시퀀스 라벨링(sequential labeling)이라고 한다면, 한국어 자연어처리는 두가지 문제가 섞여서 더 어려워 짐.
    - 여기에 띄어쓰기 오류, 신조어(맨 위에 예시에서 "존맛탱구리", "우주대존맛" 이런것들) 문제까지 겹치면 혼돈의 카오스임.
  
## 형태소 태그(일부)
![image](https://user-images.githubusercontent.com/126950833/234436988-21255045-add1-449d-9c8c-17406b385819.png)

![image](https://user-images.githubusercontent.com/126950833/234161154-9f4dfadb-cde2-4dbb-be0f-eb4c2844c7c7.png)

## 형태소 분석 방법론의 간략한 역사
### 알아두면 좋을 것들
- **트라이(Trie) 구조**
  - 트라이는 문자열 저장 및 탐색을 위한 자료구조(DS시간에 prefix tree라는게 있다...고 넘어가놓고 기말고사에 냈던 교수님이 생각나네요 ~~시불탱~~). 트리(Tree)랑 비슷하게 생김. re**trie**val tree 에서 trie가 됨ㅎ.. 
  - [어떤 블로거의 친절한 설명](https://yabmoons.tistory.com/379): 별표시는 탐색 종료 가능 지점. 존재하는 문자열은 ABC, ABCD, BCG, BDE, ZYX 임을 알 수 있음.
  
  ![image](https://user-images.githubusercontent.com/126950833/234204904-c81d40e9-7c71-4580-9bca-1b840cb0b00a.png)
  - 한글 형태소 사전으로 만들면:
  
  ![image](https://user-images.githubusercontent.com/126950833/234210147-f140366c-6cb4-426b-b5c4-351c790def94.png)
- ****

## 뇌피셜
### 합성가능성!?
- SMILES 또는 fingerprint를 가지고 트라이를 구성해놓으면(!?): rdkit의 has substructure match 보다 빠르지 않을까...?(이게 이미 trie라면 ㅈㅅ;;)
### substructure 검색
- 아호-코라식 알고리즘이 KMP 보다 빠르니까.. 특정 구조가 포함된 모든 SMILES 검색해줘~ 이런거 샵가능하지 않을까
## 다음에는?
- 형태소 간의 결합과 불규칙 활용은 어떻게 구현하나?
- 딥러닝 기반 형태소 분석기(LSTM, transformer based etc.)
## 참고
- [KoNLPy](https://konlpy-ko.readthedocs.io/ko/v0.4.3/morph/)
- [한국어 품사 태그 비교표](https://docs.google.com/spreadsheets/d/1OGAjUvalBuX-oZvZ_-9tEfYD2gQe7hTGsgUpiiBSXI8/edit#gid=0)
- [카카오의 딥러닝 기반 형태소 분석기 소개글](https://brunch.co.kr/@kakao-it/308)
- [khaii github](https://brunch.co.kr/@kakao-it/308)
- [김기현님 자연어처리](https://kh-kim.gitbook.io/natural-language-processing-with-pytorch/)
- [KOMORAN menual](https://t1.daumcdn.net/cfile/tistory/24582942542946E206?download)
- [HMM based pos tagger](https://lovit.github.io/nlp/2018/09/11/hmm_based_tagger/)
- [자연어처리, 컴파일러 샵고인물 교수님(강승식 교수, HAM 개발하신분)](https://www.youtube.com/@user-fl2op3hz6g/videos)
