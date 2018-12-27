# Algorithm

### 목차

- [그래프](#그래프)
  - [다익스트라 최단거리 알고리즘](#다익스트라-최단거리-알고리즘)
  - [플루이드와샬 최단거리 알고리즘](#플루이드-와샬-최단거리-알고리즘)
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
<br>

### 다익스트라 최단거리 알고리즘

[geeksforgeeks - Dijkstras shortest path algorithm](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)를 번역한 자료입니다.



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

![dijkstra-1](https://www.geeksforgeeks.org/wp-content/uploads/Fig-11.jpg)

 sptSet은 비어있으며, 모든 정점에 무한대 값을 할당한다. {0, INF, INF, INF, INF, INF, INF, INF, INF}(정점 0은 시작점이고, INF는 무한대를 의미한다.) 다음으로 가장작은 거리값을 가진 정점을 선택한다. 정점 `0`이 선택되면 이를 sptSet에 넣는다. 이제 sptSet은 {0}이 된다. 점점 `0`을 sptSet에 포함 시킨 후, `0`에 인점한 정점들의 거리를 갱신한다. `0`에 인접한 정점은 `1`과 `7`이다. 각각의 정점의 거리는 '4'와 '8'로 갱신된다. 다음의 서브그래프는 거리가 결정된 정점과 그 거리 값을 보여준다. SPT에 포함된 정점은 초록색으로 보여진다.

![dijkstra-2](https://www.geeksforgeeks.org/wp-content/uploads/MST1.jpg)

 다음으로 아직 SPT에 포함되지 않은 정점중 거리가 가장 짧은 정점을 선택한다. 정점 `1`이 선택되고 sptSet에 포함한다. 이제 sptSet은 {0,1}이 된다. 다시 정점 `1`에 인접한 정점의 거리를 갱신한다. 정점 `2`의 거리 값이 12가 된다.

![dijkstra-3](https://www.geeksforgeeks.org/wp-content/uploads/DIJ2.jpg)

 다시 가장 짧은 거리값을 가진 정점을 선택한다. 정점 `7`이 선택된다. 이제 sptSet은 {0,1,7}이 된다. 다시 7과 인점한 정점의 거리를 갱신한다. 정점 `6`과 `8`이 갱신된다.

![dijkstra-4](https://www.geeksforgeeks.org/wp-content/uploads/DIJ3.jpg)

 아직 SPT에 포함되지 않은 정점을 선택한다. 정점 `6`이 선택된다. (sptSet{0,1,7,6}). 정점 `6`과 인접한 정점의 거리를 업데이트한다. 정점 `5`와 `8`이 갱신된다.

![dijkstra-5](https://www.geeksforgeeks.org/wp-content/uploads/DIJ4.jpg)

모든 정점이 sptSet에 포함될때 까지 위의 과정을 반복한다. 결과적으로 다음과 같은 SPT를 얻을 수 있다.

![dijkstra-6](https://www.geeksforgeeks.org/wp-content/uploads/DIJ5.jpg)
<br>

#### 특징

- 모든 정점을 서치해야하며, 모든 정점이 연결되어 있다면, O(V^2)의 시간이 든다.
- 구현할 때 우선순위 큐를 사용한다면 최단 거리인 정점을 쉽게 찾을 수 있다.
- 음의 가중치가 있다면 서클이 생기기때문에 값을 구할 수 없다.
- 그리디 알고리즘중 하나이다.  
  
  
------  
<br>
<br>

### 플루이드 와샬 최단거리 알고리즘  

GeeksforGeeks의 [Floyd Warshall Algorithm | DP-16](https://www.geeksforgeeks.org/floyd-warshall-algorithm-dp-16/)를 번역한 글입니다.

> 플루이드 와샬은 모든 쌍의 최단거리를 구하는 문제이다. 주어진 가중치가 있는 방향 간선에서 모든 정점 사이의 최단거리를 해결하는 문제이다.



첫번째로 그래프 메트릭스와 같은 솔루션 메트릭스를 초기화 한다. 그 다음 모든 정점을 중간 정점으로 고려하면서 솔루션 메트릭스를 갱신할 것이다. 이 알고리즘의 아이디어는 모든 정점을 하나하나 선택하여 모든 최단거리를 갱신하는 것인데, 선택된 정점을 중간 정점으로 포함하는 것이다. 정점 `K`를 중간 정점으로 선택한다면, 이미 {1,2,3, ... k-1}의 정점들은 중간 정점으로 구려된 후이다. 모든 정점의 쌍 (i, j)을 시작점과 끝점으로 여긴다면, 두가지 가능성이 있다.

1) `K`는 최단거리 (i, j)의 중간 정점이 아니기 때문에 dist'\[i][j]'를 그대로 유지한다. (dist 배열은 솔루션 메트릭스이다.)

2) `K`가 최단거리 (i, j)의 중간 정점에 포함된다. 때문에 만얃ㄱ dist\[i][j]의 값이 dist\[i][k] + dist\[k][j] 값보다 크다면 dist\[i][j]의 값을 dist\[i][k] + dist\[k][j] 로 갱신해야한다.

 다음의 그림은 위의 설명을 보여준다.

![플루이드 와샬](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/dpFloyd-Warshall-.jpg)



```java
class AllPairShortestPath 
{ 
    final static int INF = 99999, V = 4; 
  
    void floydWarshall(int graph[][]) 
    { 
        int dist[][] = new int[V][V]; 
        int i, j, k; 
  
        /* Initialize the solution matrix same as input graph matrix. 
           Or we can say the initial values of shortest distances 
           are based on shortest paths considering no intermediate 
           vertex. */
        for (i = 0; i < V; i++) 
            for (j = 0; j < V; j++) 
                dist[i][j] = graph[i][j]; 
  
        /* Add all vertices one by one to the set of intermediate 
           vertices. 
          ---> Before start of an iteration, we have shortest 
               distances between all pairs of vertices such that 
               the shortest distances consider only the vertices in 
               set {0, 1, 2, .. k-1} as intermediate vertices. 
          ----> After the end of an iteration, vertex no. k is added 
                to the set of intermediate vertices and the set 
                becomes {0, 1, 2, .. k} */
        for (k = 0; k < V; k++) 
        { 
            // Pick all vertices as source one by one 
            for (i = 0; i < V; i++) 
            { 
                // Pick all vertices as destination for the 
                // above picked source 
                for (j = 0; j < V; j++) 
                { 
                    // If vertex k is on the shortest path from 
                    // i to j, then update the value of dist[i][j] 
                    if (dist[i][k] + dist[k][j] < dist[i][j]) 
                        dist[i][j] = dist[i][k] + dist[k][j]; 
                } 
            } 
        } 
    } 
}
```



#### 특징

-  DP 문제 중 하나이다.
- 3중 포문으로 문제를 해결해야하기 때문에 시간복잡도는 O(V^3)이다. 때문에 정점의 개수가 많다면 다익스트라의 최단거리 알고리즘을 여러번 사용하여 문제를 해결하는 것이 좋다.
- 다익스트라보다 시간이 많이 걸리지만 한번에 모든 정점의 최단거리를 구할 수 있는 장점이 있다.
- 문제에 따라 무방향그래프를 활용할 수도 있으며, 초기값 설정, 자기 자신( i == j )의 초기값 등을 잘 생각해야한다.

 
---
<br>
<br>

### 벨만포드 알고리즘

이 글은 GeeksforGeeks의 [Bellman–Ford Algorithm | DP-23](https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/)를 번역한 글입니다.

 그래프와 그래프의 source 정점 src를 고려하여, src부터 모든 정점의 최단거리를 구하는 알고리즘이다. 다익스트라와 차이점은 그래프의 간선이 음의 값을 가질 수 있다는 점이다. 최단 거리문제는 다익스트라를 활용하여 해결할 수 있다. 다익스트라 알고리즘은 그리디 알고리즘 이며 피보나치 힙을 사용한다면 O(VlogV)의 시간 복잡도를 가졌다. 하지만 다익스트라는 음의 값을 가진 그래프에서는 사용할 수 없으며, 벨만포드를 사용하여야 한다. 벨만포드는 다익스트라보다 간단하며 분산 시스템에 잘 맞다. 하지만 시간 복잡도는 O(VE)로 다익스트라보다 복잡하다.



#### 알고리즘

Input : 그래프와 source 정점 src

Output : src로 부터 모든 정점의 최단거리. 만약 음의 사이클이 존재한다면 최단거리는 계산되지 않고, 음의 사이클을 찾아낸다.

```
1) 첫번째로 src로 부터 모든 정점의 거리를 무한대로 초기화 한다. 그리고 src의 거리는 0으로 초기화 한다.  정점의 개수만큼의 dist[] 배열을 만든다.

2) 다음으로 최단거리를 계산한다. |V|-1 번 만큼 아래 단계를 반복한다.

	a)  dist[v] > dist[u] + 간선 uv의 가중치 라면 dist[v]를 dist[u]+ 간선 uv의 가중치로 갱신한다.

3) 만약 음의 사이클이 존재한다면 다음 과 같은 상황이 발생한다.
```

 만약 ( dist[v] > dist[u] + 간선 uv의 가중치 )라면, 음의 가중치가 존재하는 것이다. step3의 아이디어는 step2가 음의 가중치를 포함하지 않으면 가장 짧다는 것을 보장한다. 만약 모든 간선에 대하여 한번더 반복하여 더 짧은 최단거리를 얻는다면, 음의 사이클이 존재한다는 것이다.

**어떻게 동작하는가?** 다른 다이나믹 프로그래밍 문제들 처럼, 이 알고리즘은 문제를 **바텀업(Bottom-up)의 방법**으로 해결한다.  첫번째 탐색에서 간선이 최대 하나 포함된 최단거리가 구해진다. 다음으로 최대 2개의 간선이 포함된 최단거리가 구해지는데 그래서 i q번째 반복 이후에 최대 i개의 간선이 포함된 최단 거리가 구해진다. 이 그래프에는 최대 |V|-1개의 단순 경로가 있을 수 있기 때문에 |V|-1번 반복된다. 이 아이디어는 음의 경로가 없음을 가정한다. 만약 i번 이상의 최단경로가 구해진다면 모든 경로는 최대 (i+1)개의 간선이 포함된 최단경로임을 보장하게 된다. 



#### 예제

다음의 예제와 함께 알고리즘을 이해해보자. 

모든 정점까지의 거리를 무한대로 초기화하고 시작 정점 src의 거리를 0으로 초기화 한다. 이 그래프에서 간선의 개수는 5개이며 모든 과정은 4번만 이루어 저야한다.

![벨만포드1](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/bellmanford1.png)

다음 순서로 진행한다. (B,E), (D,B), (B,D), (A,B), (A,C), (D,C), (B,C), (E,D). 위의 첫번째 과정을 거치고 나면 다음과 같은 거리값이 구해진다. 두번째 줄은 (B,E), (D,B), (B,D)와 (A,B)의 과정이 진행한 거리 값을 보여준다.

![벨만포드2](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/bellmanford2.png)

첫번째 반복은 최단거리가 1개이상의 간선을 포함함을 보장한다. 두번째 반복이 이루어지만 다음과 같은 거리가 구해진다. (마지막 줄이 2번째 반복의 최종결과 값이다.)

![벨만포드3](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/bellmanford3.png)

두번째 반복은 모든 최단거리가 최대 2개의 간선을 포함함을 보장한다. 모든 과정은 간선을 2번이상 처리한다. 거리는 두번째 반복 후에 최소화되므로 세번째 및 네번째 반복은 거리를 업데이트하지 않는다. 



#### 자바소스

```java
class Graph 
{ 
    // A class to represent a weighted edge in graph 
    class Edge { 
        int src, dest, weight; 
        Edge() { 
            src = dest = weight = 0; 
        } 
    }; 
  
    int V, E; 
    Edge edge[]; 
  
    // Creates a graph with V vertices and E edges 
    Graph(int v, int e) 
    { 
        V = v; 
        E = e; 
        edge = new Edge[e]; 
        for (int i=0; i<e; ++i) 
            edge[i] = new Edge(); 
    } 
  
    // The main function that finds shortest distances from src 
    // to all other vertices using Bellman-Ford algorithm.  The 
    // function also detects negative weight cycle 
    void BellmanFord(Graph graph,int src) 
    { 
        int V = graph.V, E = graph.E; 
        int dist[] = new int[V]; 
  
        // Step 1: Initialize distances from src to all other 
        // vertices as INFINITE 
        for (int i=0; i<V; ++i) 
            dist[i] = Integer.MAX_VALUE; 
        dist[src] = 0; 
  
        // Step 2: Relax all edges |V| - 1 times. A simple 
        // shortest path from src to any other vertex can 
        // have at-most |V| - 1 edges 
        for (int i=1; i<V; ++i) 
        { 
            for (int j=0; j<E; ++j) 
            { 
                int u = graph.edge[j].src; 
                int v = graph.edge[j].dest; 
                int weight = graph.edge[j].weight; 
                if (dist[u]!=Integer.MAX_VALUE && 
                    dist[u]+weight<dist[v]) 
                    dist[v]=dist[u]+weight; 
            } 
        } 
  
        // Step 3: check for negative-weight cycles.  The above 
        // step guarantees shortest distances if graph doesn't 
        // contain negative weight cycle. If we get a shorter 
        //  path, then there is a cycle. 
        for (int j=0; j<E; ++j) 
        { 
            int u = graph.edge[j].src; 
            int v = graph.edge[j].dest; 
            int weight = graph.edge[j].weight; 
            if (dist[u] != Integer.MAX_VALUE && 
                dist[u]+weight < dist[v]) 
              System.out.println("Graph contains negative weight cycle"); 
        } 
    }
}
```

 
 ---
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
<br>
<br>

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


