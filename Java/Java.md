# Java

### 목차

* [리스트 정렬](#리스트-정렬)
* [버블 정렬 In Java](#버블-정렬-알고리즘)
* [삽입 정렬 In Java](#삽입-정렬-알고리즘)



---



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

