## 형태소 분석이란?
- **(형태소?)** 의미가 유지되는 최소 단위.
- **(형태소 분석?)** 어근, 접두/접미사 품사 등 다양한 언어적 속성의 구조를 파악하는 것.
- 예시
  - MMD: 지시관형사, NNG: 일반 명사, VA: 형용사, EF: 종결어미, JX: 보조, SF: 기타 접미사
  
  ![image](https://user-images.githubusercontent.com/126950833/234155908-664e3ed1-dd33-4c4f-8bd7-9356359f94f8.png)
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
  
## 형태소 태그(일부)
![image](https://user-images.githubusercontent.com/126950833/234161154-9f4dfadb-cde2-4dbb-be0f-eb4c2844c7c7.png)


## 대표적인 형태소 분석 알고리즘
## 참고
- [KoNLPy](https://konlpy-ko.readthedocs.io/ko/v0.4.3/morph/)
- [한국어 품사 태그 비교표](https://docs.google.com/spreadsheets/d/1OGAjUvalBuX-oZvZ_-9tEfYD2gQe7hTGsgUpiiBSXI8/edit#gid=0)
- [카카오의 딥러닝 기반 형태소 분석기 소개글](https://brunch.co.kr/@kakao-it/308)
- [khaii github](https://brunch.co.kr/@kakao-it/308)
- [김기현님 자연어처리](https://kh-kim.gitbook.io/natural-language-processing-with-pytorch/)
