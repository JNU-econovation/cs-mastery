# Algorithm

### 목차

- [그래프](#그래프)
  - [다익스트라 최단거리 알고리즘](#다익스트라_최단거리_알고리즘)
- [Brian Kernighan's Algorithm](#brian-kernighan's-algorithm)
  - [Kernighan은 누구인가](#brian-kernighan's-algorithm은-누구인가?)
  - [알고리즘 설명](#brian-kernighan's-알고리즘이란?)
- [Huffman coding(허프만 부호화)](#huffman_coding(허프만_부호화))  
  
  
------
<br>
<br>


## 그래프
> 최단 거리 알고리즘
> - 하나의 정점에서 모든 정점까지의 최단거리 - 다익스트라
> - 음의 값이 있을때 하나의 정점에서 모든 정점까지의 최단거리 - 벨만포드
> - 모든 정점간의 최단거리 - 플루이드


### 다익스트라 최단거리 알고리즘

[geeksforgeeks - Dijkstras shortest path algorithm](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)



> 그래프와 그래프 속에 시작점(source vertex)이 주어진다면, 그래프안에서 시작 정점으로부터 모든 정점까지의 가장 짧은 거리를 찾는 알고리즘

 다익스트라의 알고리즘은 프림의 최단 신장트리 알고리즘과 닮았다. 프림의 최단 스패닝트리(Minimum spanning tree - MST)처럼, 주어진 시작점을 루투로 하여 최단 길이 트리(Shortest path tree-SPT)를 만들 것이다. 알고리즘의 모든 스탭에서 소스로부터 가장짧으면서 아직 포함되지 않은 set에 있는 정점을 찾을 것이다.

 다음은 다익스트라 알고리즘에서 가장 짧은 길을 찾기위한 자세한 step이다. 



#### 알고리즘

1) SPT에 포함되는 정점을 추적하기 위한 sptSet을 만든다. 즉 그 정점의 최단거리는 계산되어 결정되었다. 처음에 이 set은 비었다.

2) 그래프의 모든 정점에 거리(가중치) 값을 준다. 모든 거리는 처음에 무한대로 설정한다. 그리고 source 정점에는 0 값을 주어 처음에 선택되도록 한다.

3) 모든 정점이 sptSet에 포함될 때 까지 반복한다.

​	a) 아직 sptSet에 포함되지 않았고 가장 짧은 길이를 갖진 정점 u를 선택한다.

​	b) 이를 sptSet에 포함한다.

​	c) 정점 u에 인접한 모든 정점의 거리를 업데이트한다. 정점의 거리를 업데이트하기 위해, 모든 정점을 반복한다. 모든 정점 v에 대해서, 정점 u의 값과 u-v 간선의 가중치의 합이 정점 v의 값보다 작다면 정점 v의 거리 값을 갱신한다.



다음 예제를 이해해 보자.

![](https://www.geeksforgeeks.org/wp-content/uploads/Fig-11.jpg)

 sptSet은 비어있으며, 모든 정점에 무한대 값을 할당한다. {0, INF, INF, INF, INF, INF, INF, INF, INF}(정점 0은 시작점이고, INF는 무한대를 의미한다.) 다음으로 가장작은 거리값을 가진 정점을 선택한다. 정점 `0`이 선택되면 이를 sptSet에 넣는다. 이제 sptSet은 {0}이 된다. 점점 `0`을 sptSet에 포함 시킨 후, `0`에 인점한 정점들의 거리를 갱신한다. `0`에 인접한 정점은 `1`과 `7`이다. 각각의 정점의 거리는 '4'와 '8'로 갱신된다. 다음의 서브그래프는 거리가 결정된 정점과 그 거리 값을 보여준다. SPT에 포함된 정점은 초록색으로 보여진다.

![](https://www.geeksforgeeks.org/wp-content/uploads/MST1.jpg)

다음으로 아직 SPT에 포함되지 않은 정점중 거리가 가장 짧은 정점을 선택한다. 정점 `1`이 선택되고 sptSet에 포함한다. 이제 sptSet은 {0,1}이 된다. 다시 정점 `1`에 인접한 정점의 거리를 갱신한다. 정점 `2`의 거리 값이 12가 된다.

![img](https://www.geeksforgeeks.org/wp-content/uploads/DIJ2.jpg)



 다시 가장 짧은 거리값을 가진 정점을 선택한다. 정점 `7`이 선택된다. 이제 sptSet은 {0,1,7}이 된다. 다시 7과 인점한 정점의 거리를 갱신한다. 정점 `6`과 `8`이 갱신된다.

![](https://www.geeksforgeeks.org/wp-content/uploads/DIJ3.jpg)

 아직 SPT에 포함되지 않은 정점을 선택한다. 정점 `6`이 선택된다. (sptSet{0,1,7,6}). 정점 `6`과 인접한 정점의 거리를 업데이트한다. 정점 `5`와 `8`이 갱신된다.

![](E:\AndroidStudioProjects\mustardcoupon\DIJ4.jpg)

모든 정점이 sptSet에 포함될때 까지 위의 과정을 반복한다. 결과적으로 다음과 같은 SPT를 얻을 수 있다.

![img](https://www.geeksforgeeks.org/wp-content/uploads/DIJ5.jpg)



#### 특징

- 모든 정점을 서치해야하며, 모든 정점이 연결되어 있다면, O(V^2)의 시간이 든다.
- 구현할 때 우선순위 큐를 사용한다면 최단 거리인 정점을 쉽게 찾을 수 있다.
- 음의 가중치가 있다면 서클이 생기기때문에 값을 구할 수 없다.
- 그리디 알고리즘중 하나이다.  
  
  
------  
<br>
<br>

## Brian Kernighan's Algorithm

2진법 수에서 1의 개수를 리턴하는 로직을 짜야할 때가 있다. 예전에 Codility 단계별 문제 중에 그러한 문제가 있었던 게 기억이 난다. 그때는 매우 비효율적으로 문제를 해결했던 것 같은데, 오늘 O(logN)으로 이 문제를 해결하는 방법을 알게되어서 공유하고자 한다. 

### Brian Kernighan은 누구인가?

**브라이언 윌슨 커니핸** ([영어](https://ko.wikipedia.org/wiki/%EC%98%81%EC%96%B4): Brian Wilson Kernighan, [1942년](https://ko.wikipedia.org/wiki/1942%EB%85%84) [1월 1일](https://ko.wikipedia.org/wiki/1%EC%9B%94_1%EC%9D%BC) ~ ) 은 [벨 연구소](https://ko.wikipedia.org/wiki/%EB%B2%A8_%EC%97%B0%EA%B5%AC%EC%86%8C)에서 일하면서 선구적인 스크립트 언어인 [AWK](https://ko.wikipedia.org/wiki/AWK)와 [AMPL](https://ko.wikipedia.org/w/index.php?title=AMPL&action=edit&redlink=1)의 디자인에 기여한 컴퓨터 과학자이다. 그의 성에서 'g'는 발음되지 않으나 **커니건** 등으로도 자주 오기된다.

[C](https://ko.wikipedia.org/wiki/C_(%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D_%EC%96%B8%EC%96%B4))를 만든 [데니스 리치](https://ko.wikipedia.org/wiki/%EB%8D%B0%EB%8B%88%EC%8A%A4_%EB%A6%AC%EC%B9%98)와 함께 최초의 C언어 해설서인 〈[C 언어 프로그래밍](https://ko.wikipedia.org/w/index.php?title=C_(%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D_%EC%96%B8%EC%96%B4)_(%EC%B1%85)&action=edit&redlink=1)〉를 써서 널리 알려져 있다. 커니핸은 자신은 C 언어의 탄생에 전혀 기여하지 않았다고 밝혔다. 그는 [dirtroff](https://ko.wikipedia.org/w/index.php?title=Dirtroff&action=edit&redlink=1)를 비롯한 수많은 유닉스 프로그램을 작성했다.

선 린과 함께 [그래프 분할](https://ko.wikipedia.org/wiki/%EA%B7%B8%EB%9E%98%ED%94%84_%EB%B6%84%ED%95%A0)과 [외판원 문제](https://ko.wikipedia.org/wiki/%EC%99%B8%ED%8C%90%EC%9B%90_%EB%AC%B8%EC%A0%9C)를 푸는 유명한 휴리스틱을 개발하였다. 전자는 [커니핸-린 알고리즘](https://ko.wikipedia.org/w/index.php?title=%EC%BB%A4%EB%8B%88%ED%95%B8-%EB%A6%B0_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98&action=edit&redlink=1) (줄여서 KL), 후자는 [린-커니핸 알고리즘](https://ko.wikipedia.org/w/index.php?title=%EB%A6%B0-%EC%BB%A4%EB%8B%88%ED%95%B8_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98&action=edit&redlink=1) (줄여서 LK)이라고 부른다.

**K&R C**의 "K"에 해당하며, [AWK](https://ko.wikipedia.org/wiki/AWK)의 마지막 "K"도 그의 이름의 **K**ernighan을 나타낸다.

[캐나다](https://ko.wikipedia.org/wiki/%EC%BA%90%EB%82%98%EB%8B%A4) [온타리오](https://ko.wikipedia.org/wiki/%EC%98%A8%ED%83%80%EB%A6%AC%EC%98%A4) 주 [토론토](https://ko.wikipedia.org/wiki/%ED%86%A0%EB%A1%A0%ED%86%A0)에서 태어났으며, [토론토 대학](https://ko.wikipedia.org/wiki/%ED%86%A0%EB%A1%A0%ED%86%A0_%EB%8C%80%ED%95%99)에서 [공학](https://ko.wikipedia.org/wiki/%EA%B3%B5%ED%95%99) [물리학](https://ko.wikipedia.org/wiki/%EB%AC%BC%EB%A6%AC%ED%95%99) 학사학위를 얻었다. [프린스턴 대학](https://ko.wikipedia.org/wiki/%ED%94%84%EB%A6%B0%EC%8A%A4%ED%84%B4_%EB%8C%80%ED%95%99)에서 전기공학 박사학위를 받았으며, [2004년](https://ko.wikipedia.org/wiki/2004%EB%85%84)부터 현재까지 이 대학의 전산학과 교수로 재직중이다.



**출처** : 위키백과



### Brian Kernighan's 알고리즘이란?

```java
public int countSetBits (int n) {
    int count = 0;
    while(n){
        n = n & (n-1);  //  n의 가장 오른쪽 1비트 제거
        count ++;
    }
    return count;
}
```

이진수 비트 중 가장 오른쪽에 위치한 1을 제거하기 위해서는 n = n & (n-1)을 사용한다. 이렇게 while 문을 돌게 되면 모든 1이 제거된 후 n이 0이 되었을 때 while문이 끝나게 되고, count 값은 1이 제거될 때마다 1씩 추가되어서 결과값이 된다.

***결과적으로 2진수로 표현된 숫자의 1 갯수를 쉽게 반환할 수 있다.***



---





# Huffman coding(허프만 부호화)

 허프만 부호화는 글이나 사진 압축에 사용되는 알고리즘이다. 글자의 빈도수에 따라 치환되는 코드가 달라진다. 알고리즘 분류상 그리디 알고리즘(탐욕)에 포함된다.



## 1. 특징

그리디 알고리즘은 다음과 같은 특징을 가지고 있다.

- 빈도수가 높을 수록 짧은 코드로 치환된다.
- 치환된 코드는 다른 글자의 접두코드로 사용될 수 없다.( 접두 부호 - prefix )  

문자의 빈도수에 따라 코드를 치환하기 위해서 허프만 부호화는 리프노드를 제외한 모든 노드가 두개의 자식을 가지는 정이진 트리를 생성한다. 정이진트리에서 리프노드가 나올때까지 왼쪽은 `0` 오른쪽은 `1`을 추가하며 노드를 따라 내려간다. 허프만 코드의 알고리즘은 해당하는 정이진트리를 찾는 과정이다.



## 2. 알고리즘

 모든 문자에 대해서 사용된 빈도수를 구합니다.  빈도수로 정렬되는 최소힙에 문자를 정렬합니다.

1. 푀소힙에서 두개의 문자를 꺼내 두 문자의 빈도수의 합을 루트로 화고 좌우 자식 노드가 해당 문자인 트리를 생성하여 최소힙에 다시 넣는다.
2. 이 과정을 최소힙에 1개의 노드만 있을 때까지 반복한다.
3. 마지막에 만들어진 트리를 허프만 트리라 한다.
4. 허프만 트리에서 좌측 자식으로 내려갈때는 0을 우측 자식으로 내려갈때는 1을 더해 나간다.

이렇게 완성된 코드를 허프만 코드라 합니다.



---

