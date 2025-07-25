---
title: "알고리즘 잘하는 법 (삼성역량테스트 B형 취득)"
date: 2025-07-15 12:30:00 +0900
categories: [Algorithm]
tags: [알고리즘, 자료구조, 백준, SWEA, 코딩테스트, 자바, JAVA, CPP, C, C++, Python, B형]
math: true
---

## 알고리즘 고수 되는 법?

같은 것은 없습니다. 진부한 말이지만, 꾸준히 열심히 해야합니다. 저는 올해 1월에 싸피에 들어와서 반년의 시간동안 실력이 정말 많이 늘었습니다. 그 과정에서 백준 골드4->플래티넘2로 올렸고, 삼성 역량테스트 B형도 취득했습니다.

저의 공부 철학이 정답은 아니겠지만, 꽤나 괜찮은 방법이라고 자부합니다. 사실 알고리즘 뿐만 아니라 어떤 공부에도 적용할 수 있는(특히 공학적 분야애서는) 방법이겠죠. 오늘 글을 통해 조금이나마 도움이 되길 바라며 글을 시작하겠습니다.

***

### 1. 자료구조, '사용법'이 아닌 '원리'에 집착하기

자료구조의 중요성은 아무리 강조해도 지나치지 않습니다. 하지만 저는 단순히 '자료구조를 유연하게 사용하는 수준'으로는 부족하다고 생각합니다. **특정 자료구조가 내부적으로 어떻게 동작하는지** 명확히 이해하고 설명할 수 있어야 합니다.

예시는 Java를 기준으로 말씀드리겠습니다.(하지만, 대부분의 언어에 적용되는 이야기일 것 같습니다.)

"예를 들어, int[] 배열과 HashMap<Integer, Integer>는 특정 원소를 조회하는 시간 복잡도가 평균 $O(1)$로 같다고 알려져 있습니다. 그렇다면 왜 특정 상황에서는 배열이 해시맵보다 압도적으로 빠를까요?

답은 메모리와 오버헤드에 있습니다. int[]는 연속된 메모리 공간에 순수한 정수 값들만 담습니다. CPU는 arr[i]에 접근한 뒤, 곧이어 arr[i+1]에 접근할 것을 예측하고 관련 데이터를 **캐시(Cache)**에 올려둡니다. 덕분에 다음 데이터 접근은 메모리가 아닌 훨씬 빠른 캐시에서 이루어져 눈에 보이지 않는 속도 향상을 얻습니다.

반면 HashMap은 다릅니다. 각 데이터는 Entry라는 객체로 포장되어 힙 메모리 곳곳에 흩어져 저장됩니다. 특정 값에 접근하려면 먼저 키의 hashCode()를 계산하고, 해시 충돌이 있다면 연결된 리스트나 트리를 순회해야 합니다. 또한, int가 아닌 Integer라는 **래퍼 클래스(Wrapper Class)**를 사용하므로, 값을 사용할 때마다 포장을 뜯는 과정(Unboxing)에서 보이지 않는 비용이 발생합니다.

이처럼 '동작 원리'에 대한 이해는, 같은 $O(1)$이라도 그 무게가 다름을 알게 해줍니다. 이러한 이해를 바탕으로 저는 대부분의 상황에서 배열로 풀 방법을 먼저 고민합니다.

트리나 해시 같은 고급 자료구조는 분명 강력합니다. 하지만, 기본적인 자료구조를 완벽히 이해하고 있다면, 정말 필요할 때만 칼을 뽑아 들 수 있습니다. 이는 결국 더 가볍고 효율적인 코드로 이어집니다.

***

### 2. 정렬, `Arrays.sort()` 너머의 세상

"정렬은 그냥 라이브러리 쓰면 되는 거 아닌가?"라고 생각할 수도 있습니다. 물론 코딩테스트나 실무에서는 그래도 됩니다. 하지만 '공부'의 과정에서는 다릅니다.

저는 버블, 삽입, 선택, 퀵, 병합 정렬 같은 고전적인 정렬 알고리즘들을 직접 구현해보는 경험이 필수라고 생각합니다. 이 과정을 통해 우리는 **데이터를 어떻게 비교하고, 교환하고, 이동시키는지**에 대한 근본적인 감각을 익힐 수 있습니다. `Arrays.sort()` 뒤에 숨겨진 복잡한 세상을 직접 마주하는 경험은 데이터를 다루는 시야를 넓혀주고, 더 나아가 문제 해결의 기반이 되는 탄탄한 근육을 길러줍니다.

예를 들어, **안정 정렬(Stable Sort)**이라는 개념을 생각해 봅시다. 병합 정렬은 안정 정렬이지만, 일반적인 퀵 정렬은 그렇지 않습니다. 이 차이가 왜 발생하는지, 그리고 어떤 문제에서 이 '안정성'이 결정적인 역할을 하는지 직접 구현하며 고민해보는 경험은, 단순히 Arrays.sort()를 호출하는 것만으로는 절대 얻을 수 없는 통찰을 줍니다. 이것이 바로 라이브러리 너머의 세상입니다."

***

### 3. '일단 틀리는' 문제 풀이의 역설

저는 문제를 풀 때 정답률이 굉장히 낮은 편입니다. 문제를 읽고 나면, 가장 먼저 떠오른 '날것의 아이디어'로 일단 구현부터 해봅니다. 설령 이 방법이 시간 초과가 날 것 같고, 비효율적으로 보여도 개의치 않습니다.

그리고 보기 좋게 틀립니다.

어떤 이는 이런 방식이 비효율적이라고 말할지도 모릅니다. 하지만 저는 이 **'일단 틀리는' 과정**이 가장 효율적인 학습법이라고 확신합니다. 왜 시간 초과가 발생했는지, 어떤 예외 케이스를 놓쳤는지 몸으로 부딪히며 배우는 것만큼 확실한 공부는 없습니다.

* 첫 번째 시도 (시간 초과) → "아, 이 로직은 $O(N^2)$이라 데이터가 많아지면 시간초과가 발생하는구나."
* 두 번째 시도 (메모리 초과) → "불필요한 객체를 너무 많이 생성했구나. 배열로 최적화할 수 있겠다."
* 세 번째 시도 (오답) → "경계값이나 예외 케이스 처리를 놓쳤네."

이 실패의 과정 속에서 구현 능력과 디버깅 능력은 폭발적으로 성장합니다. 완벽한 설계를 고민하느라 시간을 보내는 것보다, 일단 부딪치고 깨지면서 얻는 경험이 훨씬 더 값지다고 생각합니다.

***

### 결론: 어려운 문제도 언제나 기본기

많은 분들이 다익스트라, 세그먼트 트리 같은 고급 알고리즘를 공부해야 한다는 압박을 느낍니다. 하지만 저는 그보다 브루트포스(완전 탐색)와 이분 탐색 같은 기본기를 먼저 완벽하게 다지는 것이 훨씬 중요하다고 생각합니다. 

어떤 문제를 만났을 때, '이건 세그먼트 트리 문제네!'라고 바로 떠올리는 것보다, '일단 모든 경우를 다 탐색하면 어떻게 될까?'라는 브루트포스 접근부터 시작하는 것이 훨씬 더 단단한 풀이입니다. 그 과정에서 '아, 특정 구간의 합을 반복적으로 구해야 하네? 이걸 어떻게 최적화하지?'라는 필요성을 느껴야 세그먼트 트리의 진정한 가치를 이해할 수 있습니다. 대부분의 심화 알고리즘은 결국 이 기본기에서 파생된 최적화 기법일 뿐입니다.

저는 B형 시험장에서 제가 가장 자신 있는 기본기만으로 문제를 해결하고자 했습니다. LinkedList 대신 배열을, Union-Find 대신 DFS를 사용해서 문제를 풀었고 합격을 할 수 있었습니다.

알고리즘 공부는 자격증 취득처럼 단기간에 끝내는 것이 아닙니다. 자료구조의 동작 원리를 파고들고, 간단한 정렬을 구현해보며, 수없이 틀려보는 과정을 통해 다져진 단단한 기본기를 쌓는 것이 알고리즘 공부라고 생각합니다.

제가 오늘 캐싱/오버헤드/객체/세그먼트트리/래퍼클래스/안정정렬 등 다소 이해하기 어려운 개념들을 꺼내서 막막하실 수도 있을 것 같습니다. 하지만, 핵심은 한가지 입니다. **원리를 생각하며 문제를 해결하려는 태도**가 가장 중요합니다. 이에 대한 개념들은 앞으로 하나씩 설명을 드리도록 하겠습니다.

궁금한 내용 있으신 분들은 댓글 주세요. 감사합니다.