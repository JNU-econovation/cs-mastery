# Spring

### 목차

* [ORM, JPA, Hibernate의 차이점](orm,-jpa,-hiberbate의-차이점)

- [스프링 개요](#스프링-개요)
  - [스프링 프레임워크](#스프링-프레임워크)
  - [스프링 프레임워크 모듈](#스프링-프레임워크-모듈)
  - [스프링 컨테이너](#스프링-컨테이너)
- [DI](#di)
  - [About DI](#about-di)
  - [스프링 DI 설정 방법](#spring-di-setting)
- [다양한 의존 객체 주입](#다양한-의존-객체-주입)
  - [생성자를 이용한 의존 객체 주입](#생성자를-이용한-의존-객체-주입)
  - [Setter를 이용한 의존 객체 주입](#setter를-이용한-의존-객체-주입)



---

# ORM, JPA, Hibernate의 차이점

> 모 기업에서 기술면접을 보고 왔는데 위와 같은 질문이 나왔다. JPA를 그저 사용만 해봤지 저들의 관계에 대해서는 알지 못하여 아무도 대답하지 못했다. 이참에 공부해보려 한다.



### ORM이란 무엇인가?

- Object Relational Mapping의 약자이다. 즉 객체 관계를 DB에 매핑 시키는 기술이다.
- 기존의 RDB를 객체지향적으로 사용하기 위하여 탄생하였다. 기존에는 객체지향적으로 접근하기 쉽지 않았다.
- ORM을 통해 객체와 RDB 사이를 객체지향적으로 다룰 수 있다.



### JPA란 무엇인가?

- Java Persistence API의 약자다. 
- JavaSE, JavaEE를 위한 영속성(persistence) 관리와 ORM을 위한 표준 기술이다.
- JPA는 ORM 표준 인터페이스이라고 할 수 있다.
- JPA의 구현체는 Hibernate, OpenJPA, EclipseLink 등이 있다.



### Hibernate란 무엇인가?

- Boss에서 개발한 ORM 프레임워크 입니다.
- 특정 클래스에 매핑되어야 하는 데이터베이스의 테이블에 대한 관계 정의가 되어 있는 XML 파일의 메타데이터로 객체 관계 매핑을 간단하게 수행시킨다.
- Hibernate를 사용하면 데이터베이스가 변경되더라도 SQL 스크립트를 수정하는 등의 작업을 할 필요가 없다.
- 애플리케이션에서 사용되는 데이터베이스를 변경시키고자 한다면 설정파일의 dialect 프로퍼티를 수정함으로서 쉽게 처리할 수 있다.
- Hibernate는 MySQL, Oracle, Sybase, Derby, PostgreSQL를 포함한 많은 데이터베이스를 지원하며 POJO 기반의 모델과도 원활하게 동작한다.



### 왜 JPA를 쓸까?

- SQL 중심적인 개발 불편
  - 쿼리가 변경되면 이에 따른 DTO 객체의 변경도 불가피하게 일어난다
  - 데이터를 가져와 객체지향적으로 관계를 Mapping하는 일이 매번 일어난다.
  - SQL 의존적 개발이 이루어진다.
- 객체-관계 간에 모델 불일치
  - RDB에는 Row, column의 2차원 형태로 데이터가 저장된다.
  - 데이터 관계는 외래키 형태로 표현된다.
  - 문제는 도메인 객체를 관계형 데이터 베이스로 저장할 때 발생한다.
  - 애플리케이션의 객체는 row column 형태가 아니다.
  - 도메인의 객체는 객체의 상태를 변수로 가지고 있다. 그래서 도메인 객체 그대로 관계형 데이터베이스에 저장할 수가 없다.
  - 이러한 불일치를 객체-관계 간 임피던스 불일치라고 한다.
- 상속 불일치
  - 상속은 객체 세계에서는 지원하지만, 관계형 스키마에서는 지원하지 않는다.
  - 상속은 모든 객체지향 언어, 특히 자바에서 바늘과 실처럼 뗄 수 없는 특징이다.
  - 관계형 스키마에는 상속 개념이 없다.
  - 임원과 직원을 예로 들어보면 이 관계를 RDB에서 표현하는 것은 쉽지 않다. 상속 없이 현실 세계의 문제 상황을 표현하는 것은 매우 복잡한 일이다.
  - class to table 전략을 사용한다.
- 관계와 연관 관계의 불일치
  - SQL 중심적인 개발의 문제점
    - field 하나 추가할 때 마다 쿼리도 바꿔야하고, VO도 바꿔야한다
    - 객체답게 모델링 할수록 매핑 작업만 늘어난다.



### 장점

- 객체지향적으로 데이터를 관리할 수 있기 때문에 비즈니스 로직에 집중할 수 있으며, 객체지향 개발이 가능하다.
- 테이블 생성, 변경, 관리가 쉽다. 로직을 쿼리에 집중하기 보다는 객체자체에 집중할 수 있다.
- 빠른 개발이 가능하다.





### 단점

- 어렵다. 장점을 누리기 위해서는 알아야 할 것이 많다.
- 잘 이해하고 사용하지 않으면 독이 된다.
- 성능상 문제가 있을 수 있다.



**출처** : http://www.libqa.com/wiki/769





---

# 스프링 개요

### 스프링 프레임워크

스프링 프레임워크는 주요기능으로 **DI, AOP, MVC, JDBC** 등을 제공한다. 처음하는 사람들에게는 낯설 수 있다. 

- 자바로 처음 웹 개발을 하는 사람들은 **JSP**를 많이 접해봤을거다. **Spring** 하기 전에 **JSP** 먼저 해보는게 낫다.
- **MVC**는 **모델, 뷰, 컨트롤러**로 **구조화하는 것**이고, **JDBC**는 **디비 관련**이다. **DI**는 **주입기능**이다. 어떤 기능을 만들어서 필요할때마다 주입해서 사용하는 것. **AOP**는 **관점지향 프로그래밍**이라고 하는데, 스프링에서 공통 부분을 떼어내서 주요부분에 붙였다가 뗏다가 하면서 사용하는 것이다.
- 프레임워크의 유무를 **네비게이션 유무**에 **비유**. 운전자(프로그래머)는 네비게이션이 있으면 운전만 하면 된다. 프레임워크는 **수많은 기능들을 추상화 시켜놓고 틀로 만든다**. 그리고 그걸 이용할 수 있게 하는 것이다. **추상적인 틀을 곧 프레임워크**라고 한다.

### 스프링 프레임워크 모듈

앞에서 말한 틀의 하나하나를 모듈이라고 한다. 스프링에는 `Spring-core`, `Spring-aop`, `Spring-jdbc`, `Spring-tx`, `Spring-webmvc` 모듈을 제공하고 있다.

- **Spring core** : 스프링의 핵심인 DI와 IoC를 제공
- **Spring aop** : AOP구현 기능 제공
- **Spring jdbc** : 데이터베이스를 쉽게(적은 양의 코드) 다룰 수 있는 기능 제공
- **Spring tx** : 스프링에서 제공하는 트랜잭션 관련 기능 제공
- **Spring webmvc** : 스프링에서 제공하는 컨트롤러와 뷰를 이용한 스프링MVC 구현 기능 제공
- 스프링을 사용하기 위해서는 가장 핵심인 core를 사용해야하고, 데이터베이스 연동하면 jdbc 사용해야하고, 웹 구현하려면 mvc도 사용해야한다. 

스프링 프레임워크에서 제공하고 있는 모듈을 사용하려면 모듈에 대한 의존설정을 개발 프로젝트에 XML 파일 등을 이용해서 개발자가 직접하면 된다.

라이브러리를 주입해서 사용하는 것과 비슷하다. 하지만 개발자가 직접 다운받을 필요는 없고 명시만 해주면 자동으로 import 시켜준다.

### 스프링 컨테이너

스프링에서 객체를 생성하고 조립하는 컨테이너로, 컨테이너를 통해 생성된 객체를 **Bean**이라고 부른다.

- 자바를 보통 OOP 언어라고 한다. 객체에는 속성과 기능이 들어있다. 외부에서 사용만하면 된다. 스프링도 마찬가지다. 
- 스프링도 객체를 만든다. 필요할 때 마다 객체가 가지고 있는 속성과 기능을 사용하면 된다. 
- XML 문서를 통해 객체가 만들어진다. Spring 컨테이너는 XML 문서를 이용해서 만들어진 객체를 담고 있다. 
- Spring에서는 이걸 Object라고 하지 않고 Bean이라고 한다. 그것을 개발문서로 꺼내서 사용하는 구조다.
- Spring에서는 IoC를 컨테이너라고 한다.



> **스프링 컨테이너에 대하여 좀 더 자세히 알아보자**

 보통 스프링 프로젝트에서 resources는 프로젝트에 필요한 자원들이 담기는 곳이다. 거기에는 **applicationContext.xml** 이 있는데 이것이 컨테이너 역할을 한다. 그리고 스프링은 이 컨테이너 안에 객체(Bean)를 모아둔다. 스프링이 객체를 갖다가 메모리에 로딩을 하긴 하는데, 스프링 컨테이너를 IoC하는 큰 그릇을 만들어두어야 한다. 내가 필요한 객체를 그 그릇에 다 구현해놓고 필요할 때마다 그 그릇에서 해당 객체를 꺼내와서 사용한다. 이 객체를 Bean이라고 한다. Bean에는 id가 있고 class의 풀네임이 있다. 이렇게 사용하면 new를 사용하지 않고 객체를 불러올 수 있게 된다. applicationContext라는 파일에 의해서 객체가 생성이 되고 메모리에 로딩이 된다는 말이다. 그리고 이것은 메모리에서 특별히 관리되는 스프링 컨테이너 부분에 로딩이 된다.

 객체를 가져오기 위해서는 스프링 컨테이너에 먼저 접근을 해야한다. GenericXmlApplicationContext 의 파라미터로 classpath:applicationContext.xml 이라고 적어주고 객체를 생성한다. 그리고 bean id를 매개변수로 넣어 getBean() 함수를 호출한다.  데이터타입은 클래스를 적어주면 된다. 그리고 객체를 반환받아서 사용하면 된다. 

 스프링에서는 좀 더 효율적이고 다른 업무에 집중할 수 있도록, xml을 통해서 bean을 만들어 접근할 수 있게 해놓았다. 이게 일반 자바와의 가장 큰 차이점이다. 요즘은 xml 말고 어노테이션 기능을 이용해서 주로 사용한다. 

pom.xml은 스프링 모듈들을 가져오는 곳이다.





# DI

> **스프링은 DI를 효율적으로 사용하게 한다. 다른 언어에서도 DI는 사용한다. 알게모르게 이미 사용해본 경험이 있을 것이다.**

### About DI

- **배터리 일체형** : 배터리가 떨어지면 장난감을 새로 구입해야 한다.
- **배터리 분리형** : 배터리가 떨어지면 배터리만 교체하면 된다.

효과적인 것은 **배터리 분리형**이다. 이것을 프로그래밍적으로 관점을 바꿔서 객체를 이용해서 수많은 기능을 구현했다고 생각해보자. 객체 하나가 모든 프로젝트에 엮여있다고 생각하면 그 객체를 수정할 때 프로젝트 전체를 바꿔야할 것이다. 하지만 배터리 분리형처럼 객체가 분리되어있다면 객체만 수정하면 된다. 이러한 내용은 객체지향 프로그래밍을 하다보면 흔히 경험할 수 있는 내용이다. 여기서 좀 더 깊이 진입하면 DI라는 개념이 나오는데, 배터리가 장난감에 의존해서 만들어진다고 해서 의존 주입이라고 한다. **좀 더 효과적인 DI 방법은 분리형**이라고 할 수 있다. DI는 생각보다 별게 아니다. 흔히 봐왔던 프로그래밍 기법 중 하나다. 

```java
public class ElectronicCarToy {
    private Battery battery;
    
    public ElectronicCarToy() {
        battery = new NormalBattery();
    }
}
```

- **배터리 일체형** : **생성자를 통해 배터리를 생성**하므로 배터리가 떨어지면 장난감을 새로 만들어야한다.

```java
public class ElectronicRobotToy {
    private Battery battery;
    
    public ElectronicRobotToy() {
        this.battery = battery
    }
    
    public void setBattery(Battery battery) {
        this.battery = battery;
    }
}
```

- **배터리 분리형** : 장난감을 생성하고 나서 **배터리를 수동으로 세팅**할 수 있기 때문에 배터리 교체가 가능하다.

**어떤 객체에 의존한다 -> 의존성 주입**

### Spring DI Setting

**스프링 컨테이너 생성 및 Bean 객체 호출 과정**

스프링 설정파일`Application.xml`로부터 `GenericXmlApplicationContext` 클래스를 통해 `Spring Container`에 `getBean()`으로 Bean들을 만들어 놓는다. Bean 객체를 필요로 하는 로직에 자유롭게 갖다가 사용하면 된다. new로 동적 객체 생성이 필요없다. 그러므로 Bean 객체는 상태값이 없고 비즈니스 로직만 처리할 때에 사용하는 것이 좋다.

- DI는 Bean 내부에 또 다른 객체들이 의존성 주입이 된 것을 말한다. **객체 속에 객체를 가지고 있는 구조를 보고 DI**라고 한다.
- 생성자로 객체를 주입하는 방법과 Setter를 통해 객체를 주입하는 방법이 있다. 생성장로 주입하는 방법은 applicationContext.xml에서 **bean 내부에  Constructor-arg 를 선언**하여 사용하는 방법이 있다.
- **클래스 구조** : MainClass -> 조립(applicationContext.xml, assembler) -> service 클래스 -> DAO 클래스





## 다양한 의존 객체 주입

### 생성자를 이용한 의존 객체 주입

```java
public StudentRegisterService(StudentDao studentDao) {
    this.studentDao = studentDao;		
}
...// 위의 코드를 applicationContext.xml에 구현하면 아래와 같다.
<bean id ="studentDao" class="ems.member.dao.StudentDao"></bean>
<bean id = "registerService" class"ems.member.service.StudentRegisterService">
	<constructor-arg ref="studentDao"></constructor-arg>
</bean>
```

* 객체가 스프링 컨테이너에서 생성이 될 때 argument로 주입이 되면서 생성될 수 있다.



### Setter를 이용한 의존 객체 주입

```java
public void setJdbcUrl(String jdbcUrl){
    this.jdbcUrl = jdbcUrl;
}
...// 위의 코드를 applicationContext.xml에 구현하면 아래와 같다.
<bean id = "dataBaseConnectionInfoDev" class="ems.member.DatabaseConnectionInfo">
	<property name"jdbcUrl" value="jdbc:oracle:thin:@localhost:1521:xe" />
</bean>
```

* 파라미터가 List 타입이면?

  ```xml
  <property name="developers">
  	<list>
  		<value>Cheney.</value>
  		<value>Eloy.</value>
  		<value>Jasper.</value>
  	</list>
  <property>
  ```

하나의 클래스를 가지는 여러가지 Bean이 있을 수 있다. 보통 Dev(개발)용 Real(배포)용으로 두가지 경우가 있을 수 있는데, 이 경우 property를 이용하여 경우를 나눠서 개발할 수 있다.

* 파라미터가 Map 타입이면?

  ```xml
  <property name="developers">
  	<map>
  		<entry>
  			<key>
  				<value>cheney</value>
  			</key>
  		</entry>
  	</map>
  <property>
  ```










참고강의 : https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC_renew/
