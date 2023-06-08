## 요약
- 한국어 형태소 분석기에서 많이 사용하는 검색 알고리즘. 아호, 코라식 각각 사람 이름임.
- 사전에 포함되어 있는 모든 접두사를 검색할 수 있음. 자동완성 같은거 구현할 때 쓰임(그림). 바이오인포매틱스에서는 특정 패턴의 염기서열 검색 등에 사용 가능.
- 시간 복잡도: O(N+p1+p2+..+pn)

  ![image](https://github.com/3billionAIstudy/NLP/assets/126950833/89e4ef56-684c-4c2c-a3dc-a2b4c550c42f)

## 미리 알고 있으면 좋은 것들 & 참고 자료
- [KMP algorithm](https://en.wikipedia.org/wiki/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm)
- [trie structure](https://en.wikipedia.org/wiki/Trie)
- [BFS](https://en.wikipedia.org/wiki/Breadth-first_search)
- [인도형님 유투브](https://www.youtube.com/watch?v=OFKxWFew_L0)
## Algorithm overview
### 크게보면 3단계
- 입력 패턴(=형태소)에 대해 트라이 사전 구축
- **failure link(=suffix link)**, **output link** 구성
- matching
### key idea
- 검색하려고 하는 패턴을 하나하나 전부 탐색하지 않고, **부분 매치** 가 일어난 지점을 기억했다가 거기부터 이어서 탐색
- 이게 무슨 말이냐하면(KMP의 failure function)..
  - 패턴 p를 스트링 s에서 찾는 KMP의 경우를 보자. *s=wacandaforever*, *p=candacan* 스트링 s의 인덱스=i, 패턴 p의 인덱스=j라 하면
  - 가장 단순한 완전 탐색에서는 **i=0, j=0** 에서 *miss*, **i=1, j=1** 에서 *miss*, **i=2, j=0** 에서 *sub match* .. 이후 *miss*가 한 번 더 발생하면? **패턴 p의 처음부터(j=0)부터** 다시 탐색해야 함..
  - 근데 사실 우리는 패턴 p를 처음부터 탐색할 필요가 없음. 왜냐하면, p의 접두/접미(prefix, suffix)사를 알고 있으면 p의 부분 매치가 성공하는 인덱스 j를 미리 계산할 수 있기 때문에.
  - KMP는 이런 동기에서 출발한 알고리즘이고, aho-corasick은 KMP의 일반화(=automaton) 버전으로 볼 수 있음. 
## Trie structure
### 그림
![image](https://github.com/3billionAIstudy/NLP/assets/126950833/2ab7d7e3-3740-4b27-8c64-891b55243f04)
### 코드
```
    def insert(self, word):
        """Insert a word into the trie"""
        node = self.root
        
        # Loop through each character in the word
        # Check if there is no child containing the character, create a new child for the current node
        for char in word:
            if char in node.children:
                node = node.children[char]
            else:
                # If a character is not found,
                # create a new node in the trie
                new_node = TrieNode(char)
                node.children[char] = new_node
                node = new_node
        
        # Mark the end of a word
        node.is_end = True

        # Increment the counter to indicate that we see this word once more
        node.counter += 1
```
## Failure link(suffix link)

### 그림

![image](https://github.com/3billionAIstudy/NLP/assets/126950833/4b82f859-39dc-438b-aaaf-d2243d9c4922)


### 코드
```
1. Trie의 루트로부터 BFS를 수행하면서 Failure Link를 만든다.
2. 현재 위치(p)와 가리키는 노드(q)에 대해서
  (1) p가 루트라면, q의 Failure Link는 루트이다.
  (2) p가 루트가 아니면, p의 실패 링크(pf)에서 q와 같은 문자로 이어지는 노드(r)가 있는지 확인한다.
    1) 그런 r이 존재한다면 qf는 r을 가리킨다.
    2) 그런 r이 존재하지 않는다면, p에 pf를 대입하고 (1)로 돌아가 과정을 반복한다.

############################################################################################
    def constructfail(self):
        queue = Queue()
        self.head.fail = self.head
        queue.put(self.head)
        while not queue.empty():
            crr = queue.get()
            for nextc in crr:
                child = crr[nextc]
                
                if crr is self.head:
                    child.fail = self.head
                else :
                    f = crr.fail
                    while f is not self.head and nextc not in f:
                        f = f.fail
                    if nextc in f:
                        f = f[nextc]
                    child.fail = f
                
                child.addout(child.fail.out)
                child.final |= child.fail.final
                
                queue.put(child)
``` 

## Search Example
사실 failure link 말고 다른 종류의 link가 하나 더 필요함ㅎ
output link라고..인도 형님 유투브에서는 dictionary link로 표시 하던데 똑같은 거임.
암튼 output link + failure link를 따라가면서 substring matching 을 하는건데 이건 복잡하니까 다음 기회에... ~~는 그짓말이고 사실 이거 그림 찾다가 못찾았읍니다 ㅈㅅ~~
### 그림
### 코드







