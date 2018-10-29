# Java

### 목차

* [JVM의 메모리 구조](#JVM의-메모리-구조)
* [리스트 정렬](#리스트-정렬)
* [버블 정렬 In Java](#버블-정렬-알고리즘)
* [삽입 정렬 In Java](#삽입-정렬-알고리즘)



---


## JVM의 메모리 구조
<br>

### JVM이란
- 자바가상머신은 자바로 작성된 프로그램을 실행해주는 플랫폼이다.
- 운영체제와 자바프로그램(어플리케이션) 사이에 위치하기 때문에 운영체제와 상관없이 어플리케이션을 실행하게 해주는 장점이 있다.  

### JVM의 메모리 구조
- 자바 버전에 따라 변화가 있지만, 크게 **메소드영역**, **스택영역**, **힙영역*으로 구분할 수 있다.*"  


#### 메소드 영역
- Class Area, Method Area, Static Area 라고도 불린다.
- 이름에서 알 수 있듯이 *.class 파일이 메모리에 올라가는 일과 관련되어 있다.
- 컴파일러에 의해 컴파일된 class 파일이 올라가기 때문에 메소드와 클래스 변수인 스테틱변수들이 올라간다.
- 즉, main 메소드가 있는 클래스 파일이 메모리에 저장되고 main메소드가 실행되면서 프로그램이 실행된다.
- **클래스 로딩** - 프로그램을 실행하다 메소드 호출이 있었는데 해당 메소드를 가지고 있는 클래스가 메모리 상에 없다면, 메소드 영역에 클래스를 올리게된다.  
[참고 - WANZARGEN블로그](http://wanzargen.tistory.com/16)  


#### 스택 영역
- 지역변수와 매개변수가 저장된다.
- 메소드가 호출되면 지역변수, 매개변수가 메모리에 쌓이고 메소드가 끝나면 소멸한다.
- 스택구조로 되어 있기 때문에, 1메소드안에서 2메소드가 호출되면 2메소드가 1메소드 위에 쌓이게 된다.
- 재귀호출을 잘 못 사용하게 된다면, 같은 지역변수들이 계속 쌓이게 되기 때문에 'StackOverFlow'오류가 발생하게 된다.  


### 힙 영역
- 쉽게 생각하면 new 연산자를 사용했을 때, 생성된 객체들이 저장되는 공간이다.
- `A a = new A()`라고 객체를 생성했다면 실제 객체는 힙영역에 참조변수인 a와 힙영역의 주소는 스택에 저장된다.
- **가비지 콜렉터** 더이상 힙영역의 객체가 참조되지 않는다면 힙영역에서 삭제해 주어야한다. 자바를 가비지콜렉터라는 기능으로 자동으로 실행해준다.
- 효율적인 힙관리를 위해 힙은 여러단개로 구성되어 있다.(가비지 콜렉터와 관련되어 있으므로 가비지 콜렉터에서 더 자세히 설명하도록 힌다.)  


## 리스트 정렬

#### Comparable과 Comparator 인터페이스의 차이는 무엇일까?

> **Comparable** 인터페이스는 일반적인 순서로 정렬할 때 사용한다 (EX. 사전순서) 
>
> **Comparator** 인터페이스는 사용자가 원하는 순서로 정렬할 때 기준으로 사용한다.

배열을 정렬할 때는 Array나 Collection 클래스에 내장된 라이브러리를 사용한다. 내장된 함수 중 sort에 해당하는 메소드가 오버로딩 된 것들이 있다. 배열만 매개변수로 받거나, 배열과 Comparator 객체를 매개변수로 받는 두 가지로 분류가 된다. Comparator 객체가 없는 sort는 Comparable하게 정렬한다.

```java
1. 원시 타입
int[] numbers = {3, 2, 1};

Arrays.sort(numbers);

2. 레퍼런스 타입
String[] alphabets = {"f","c","s"};

Arrays.sort(alphabets);
```

원시타입의 배열을 정렬한다. Comparable로 자연스럽게 정렬이 된다.

그리고 레퍼런스 타입인 String은 Comparable 인터페이스를 구현하기 때문에 자동 정렬이 된다.

정렬해야 하는 타입이 Comparable 인터페이스를 구현하지 않으면 ClassCastException 예외가 발생한다.

아래가 그 예시이다.

```java
List<Man> mans = new ArrayList<>();

for(int i = 0; i < 10; i++){
    mans.add(new Man(i));
}

try {
    Arrays.sort(mans.toArray());
} catch (Exception e){
    //Maybe ClassCastException..
}
```

컴파일러는 sort의 매개변수의 타입이 Comparable 인터페이스를 구현했을 것이라고 생각한다. 그래서 여기서는 sort 메소드를 사용할 수 없다.

```java
public static <T extends Comparable<? super T>> void sort(List<T> list)  --- 메소드 시그니처
```

원하는 대로 정렬하고 싶으면 Comparator를 구현하여 sort의 매개변수로 넘겨주어야한다. 



```java
public class ReverseNumber implements Comparator<Integer> {
    @Override
    public int compare(Integer o1, Integer o2){
        return o2 - o1;
    }
}
```

역순으로 정렬이 된다. (두번째 매개변수가 첫번째 매개변수 앞에 올 때) o1-o2면 평순

이걸 실제 정렬에 사용해보자

```java
List<Integer> numbers = Arrays.asList(4,3,1,2);

Collections.sort(numbers, new ReverseNumber());			
```

**정렬 완료**





---

#### 버블 정렬 알고리즘

```java
public void bubbleSort(int[] numbers){
    boolean numbersSwitched;
    do{
        numbersSwitched = false;
        for(int i = 0; i < numbers.length - 1; i++){
            if(numbers[i+1] < numbers[i]){
                int temp = numbers[i+1];
                numbers[i+1] = numbers[i];
                numbers[i] = temp;
                numbersSwitched = true;
            }
        }
    } while (numbersSwitched);
}
```

 가장 구현하기 간단한 알고리즘이다. 하지만 최악의 경우 O(n^2)의 성능을 보여준다. 바로 역순으로 정렬되어있을 때다. 하지만 모두 다 정렬이 되어있다면 O(n)이다.





---

#### 삽입 정렬 알고리즘

```java
public List<Integer> insertSort(List<Integer> numbers){
    List<Integer> sortedList = new LinkedList<>();
    
    originalList: for(Integer number : numbers){
        for(int i = 0; i < sortedList.size(); i++){
            if(number < sortedList.get(i)){
                sortedList.add(i, number);
                continue originalList;
            }
        }
        sortedList.add(sortedList.size(), number);
    }
    return sortedList;
}
```

 삽입 정렬은 새로운 리스트를 생성하고 반환한다. LinkedList를 사용한 이유는 리스트 중간에 삽입할 일이 생기기 때문에 이런 경우, ArrayList는 배열기반이기 때문에 자리를 모두 이동시켜주는 작업들이 내부적으로 이루어져서 속도가 느리다. 

originalList를 continue 하게 되면, 아래 sortedList를 실행시키지 않는다. break와의 차이점이다. 오랜만에 이 문법을 보게 되었다. 잘 기억해두면 이렇게 유용하게 쓰일 수 있을 것 같다.

