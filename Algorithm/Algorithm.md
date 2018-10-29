# Algorithm

### 목차

- [Brian Kernighan's Algorithm](#brian-kernighan's-algorithm)
  - [Kernighan은 누구인가](#brian-kernighan's-algorithm은-누구인가?)
  - [알고리즘 설명](#brian-kernighan's-알고리즘이란?)



---

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