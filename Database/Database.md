# Database

### 목차

* [1. 데이터베이스 시스템](#1.-데이터베이스-시스템)
  * [데이터베이스의 특징](#데이터베이스의-특징)
  * [1.1 데이터베이스 시스템 개요](#1.1-데이터베이스-시스템-개요)
    * [1.1.1 데이터베이스 스키마와 상태](#1.1.1-데이터베이스-스키마와-상태)
    * [1.1.2 데이터베이스 시스템의 구성요소](#1.1.2-데이터베이스-시스템의-구성요소)
    * [1.1.3 데이터베이스 시스템의 요구사항](#1.1.3-데이터베이스-시스템의-요구사항)
  * [파일 시스템 방식과 DBMS 방식의 비교](#파일-시스템-방식과-dbms-방식의-비교)
  * [1.2 DBMS 언어](1.2-dbms-언어)
  * [1.3 DBMS 사용자](#1.3-dbms-사용자)
  * [1.4 데이터베이스 시스템 아키텍쳐](#1.4-데이터베이스-시스템-아키텍쳐)
    * [클라이언트 - 서버 데이터베이스 시스템](#클라이언트---서버-데이터베이스-시스템)



---

## 1. 데이터베이스 시스템

> 데이터베이스는 조직체의 응용 시스템들이 공유해서 사용하는 운영 데이터들이 구조적으로 통합된 모임이다.

### 데이터베이스의 특징

* 데이터베이스는 데이터의 대규모 저장소로서, 여러 부서에 속하는 여러 사용자에 의해 동시에 사용된다. 더 이상 데이터를 한 사용자 또는 한 부서에서 소유하지 않는다. 데이터베이스는 이제 조직체의 모든 구성원이 공유하는 자원이다
* 중복된 데이터를 갖는 별도의 파일들로 유지되는 대신에 데이터베이스에서는 모든 데이터가 중복을 최소화하면서 통합된다.
* 데이터베이스는 한 조직체의 운영 데이터뿐만 아니라 그 데이터에 관한 설명까지 포함한다. 이런 설명을 데이터베이스 스키마 또는 메타데이터라고 한다. 메타데이터는 데이터에 관한 데이터라는 뜻이다.
* 데이터의 구조가 프로그램과 분리되어 데이터베이스에 저장되므로 프로그램과 데이터 간의 독립성이 제공된다.
* 데이터베이스는 효육적으로 접근이 가능하고 질의를 할 수 있다.

### 1.1 데이터베이스 시스템 개요

#### 1.1.1 데이터베이스 스키마와 상태

* **데이터베이스 스키마** : 전체적인 데이터베이스 구조를 뜻하며 자주 변경되지 않는다. 데이터베이스의 모든 가능한 상태를 미리 정의한다. 내포(intension)이라고 부르기도 한다.
* **데이터베이스 상태** : 특정 시점의 데이터베이스의 내용을 의미하며, 시간이 지남에 따라 계속해서 바뀐다. 데이터베이스 상태를 외연(extension)이라고 부르기도 한다.

#### 1.1.2 데이터베이스 시스템의 구성요소

> 데이터베이스 시스템(DBS : Database System)은 데이터베이스, 사용자(응용 프로그램), DBMS, 하드웨어로 구성된다. 

![ê´ë ¨ ì´ë¯¸ì§](data:image/jpeg;base64,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)

* **데이터베이스** : 데이터베이스는 조직체의 응용 시스템들이 공유해서 사용하는 운영 데이터들이 구조적으로 통합된 모임이다.
* **시스템 카탈로그** : 저장된 데이터베이스의 스키마 정보를 유지한다. 사용자가 새로운 테이블을 만들거나 기존의 테이블에 새로운 애트리뷰트를 추가하는 작업 등을 수행하면 시스템 카탈로그에 이를 반영하는 스키마 정보가 삽입된다.
* **DBMS** : 실세계는 동적이기 때문에 계속해서 엔티티가 생성, 수정, 삭제된다. 적은 수라면 수작업으로 관리 가능하지만, 수십개 이상의 엔티티가 연관되고 비즈니스의 규모가 매우 크다면 비즈니스의 상태를 유지하는 것이 더 이상 수작업으로는 불가능해진다. 그래서 DBMS는 사용자가 새로운 데이터베이스를 생성하고 데이터베이스 구조를 명시할 수 있게 하고, 사용자가 데이터를 효율적으로 질의하고 수정할 수 있도록 하며, 시스템의 고장이나 권한이 없는 사용자로부터 데이터를 안전하게 보호하며, 동시에 여러 사용자가 데이터베이스를 접근하는 것을 제어하는 소프트웨어 패키지이다.
* **SQL** : 여러 DBMS에서 제공되는 사실상의 표준 데이터베이스 언어이다.
* **하드웨어** : 데이터베이스는 디스크와 같은 보조 기억 장치에 저장되며, DBMS에서 원하는 정보를 찾기 위해서는 디스크의 블록들을 주기억 장치로 읽어들여야 한다. 또한 계산이나 비교 연산들을 수행하기 위해 중앙 처리 장치가 사용된다. DBMS 자체도 주기억 장치에 적재되어 실행되어야 하므로 하드웨어 자원들을 필요로 한다.

#### 1.1.3 데이터베이스 시스템의 요구사항

* **데이터의 독립성** : 응용 프로그램이 데이터 표현의 상세한 내역과 데이터 저장으로부터 독립적이다 (파일 시스템과는 반대)
* **융통성** : 기존의 응용 프로그램에 영향을 주지 않으면서 데이터베이스 구조를 변경할 수 있어야한다.
* **효율적인 데이터 접근** : 방대한 데이터베이스를 효율적으로 저장하고 접근하기 위해서 다수의 정교한 기법을 제공해야한다. 일반적으로 인덱스 구조가 이런 목적으로 사용된다.
* **데이터에 대한 동시 접근** : 여러 사용자가 동일한 데이터베이스를 동시에 접근하는 경우가 많다. 각 사용자가 혼자서 데이터베이스를 접근하는 것처럼 인식하도록 데이터베이스에 대한 동시 접근을 동기화하기 위한 동시성 제어를 제공해야 한다.
* **백업과 회복** : 시스템 에러 등으로부터 데이터베이스를 회복하며, 디스크 등이 손상을 입는 경우를 대비해서 백업을 수행한다.
* **중복을 줄이거나 제어하여 일관성 유지** : 데이터를 통합함으로써 동일한 데이터가 여러 개의 사본으로 존재하는 것을 피한다. 성능을 향상시키기 위해 중복을 일부 허용하고 제어할 수 있다.
* **데이터 무결성** : 데이터 무결성은 의미적인 측면에서 데이터가 정확하고 완전함을 의미한다. 사용자가 무결성 제약조건을 정의하면 DBMS는 데이터를 삽입, 삭제, 수정할 때 마다 제약조건을 자동적으로 검사한다. 
* **데이터 보안** : 권한이 없는 접근으로부터 데이터베이스를 보호한다.
* **쉬운 질의어**
* **다양한 사용자 인터페이스의 제공**

*파일 시스템은 이 모든 것들의 반대이다.*

###파일 시스템 방식과 DBMS 방식의 비교

|                       파일 시스템 방식                       |                          DBMS 방식                           |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|             데이터에 대한 물리적 접근만 조정한다             |  데이터에 대한 물리적 접근과 논리적인 접근을 모두 조정한다.  |
| 동일한 파일을 두 개 이상의 프로그램이 동시에 접근할 수 없다. |     동일한 데이터를 다수 사용자가 동시에 접근할 수 있다      |
|    데이터가 비구조적이며, 중복성과 유지보수 비용이 높다.     |  데이터가 구조화되어 있으며, 중복성과 유지보수 비용이 낮다.  |
| 어떤 프로그램이 기록한 데이터는 다른 프로그램에서 읽을 수 없는 경우가 많다. |     접근 권한이 있는 모든 프로그램이 데이터를 공유한다.      |
| 데이터에 대한 접근은 미리 작성된 프로그램을 통해서만 가능하다. | 질의어를 사용하여 데이터에 대한 융통성 있는 접근이 가능하다. |
| 각 응용 프로그램마다 파일이 따로 있으므로 데이터가 통합되어 있지 않다. |          데이터가 중복을 배제하면서 통합되어 있다.           |

---

### 1.2 DBMS 언어

* **데이터 정의어(DDL : Data Definition Language)** : 사용자는 데이터 정의어를 사용하여 데이터베이스 스키마를 정의한다. DBMS는 사용자가 정의한 스키마에 대한 명세를 시스템 카탈로그 또는 데이터 사전에 저장한다. 시스템 카탈로그는 메타데이터를 저장한다. 메타데이터는 데이터베이스에 저장된 데이터에 관한 데이터를 말한다. 
  * EX > CREATE, ALTER, DROP
* **데이터 조작어(DML : Data Manipulation Language)** : 사용자는 데이터 조작어를 사용하여 데이터베이스 내의 원하는 데이터를 검색하고 수정하고 삽입하고 삭제한다. 그리고 대부분의 데이터 조작어에는 SUM, COUNT, AVG와 같은 내장 함수들이 있는데, 이것들은 C, COBOL과 같은 호스트 언어들을 사용하여 제작된 프로그램에 내포되어 사용된다. 그 이유는 데이터 조작어에는 조건문, 반복문, 입력문 등이 없기 때문이다
  * EX > SELECT, UPDATE, DELETE, INSERT
* **데이터 제어어(DCL : Data Control Language)** : 사용자는 데이터 제어어를 사용하여 데이터베이스 트랜잭션을 명시하고 권한을 부여하거나 취소한다. 해당 개념은 후에 트랜잭션을 다루면서 추가적으로 설명하겠다.

---

### 1.3 DBMS 사용자

* **데이터베이스 관리자 (DBA : Database Administrator)** : 조직의 여러 부분의 상이한 요구를 만족시키기 위해서 일관성 있는 데이터베이스 스키마를 생성하고 유지하는 사람을 말한다. 하는 일은 다음과 같다.
  * 데이터베이스 스키마의 생성과 변경
  * 한꺼번에 적재(bulk loading)
  * 무결성 제약조건을 명시
  * 사용자의 권한을 허용하거나 취소하고, 사용자의 역할을 관리
  * 저장 구조와 접근 방법(물리적 스키마) 정의
  * 백업과 회복
  * 표준화 시행
* **응용 프로그래머** : 데이터베이스 위에서 특정 응용 프로그램이나 인터페이스를 구현하는 사람으로서 `DML`의 주요 사용자다. 이들이 작성한 프로그램은 최종 사용자들이 반복해서 수행하므로 **'기작성 트랜잭션(Canned Transaction)'**이라고 부른다.
* **End User(최종 사용자)** : 최종 사용자는 질의하거나 갱신하거나 보고서를 생성하기 위해서 데이터베이스를 사용하는 사람으로서 데이터 정의어나 데이터 조작어를 직접 사용하는 경우는 비교적 많지 않다.
* **데이터베이스 설계자** : ERWin, CASE 도구들을 이용해서 데이터베이스 설계를 책임진다. 데이터베이스의 일관성을 유지하기 위해서 정규화를 수행한다. 데이터베이스를 효율적으로 접근할 수 있도록 인덱스 등을 정의한다. 설계에 관한 문서화 작업도 한다

---

### 1.4 데이터베이스 시스템 아키텍쳐

![ë°ì´í°ë² ì´ì¤ ìì¤í ìí¤íì²ì ëí ì´ë¯¸ì§ ê²ìê²°ê³¼](https://t1.daumcdn.net/cfile/tistory/2434CC5055F2A8942E)

* 데이터베이스 관리자가 **데이터 정의어**를 사용하여 테이블 생성을 요청
* **데이터 정의어 컴파일러**가 이를 번역하여 테이블이 파일 형태로 데이터베이스에 만들어진다
* 이 테이블에 대한 명세가 **시스템 카탈로그에 저장**된다.
* 최종 사용자나 응용 프로그래머가 데이터 조작어를 사용하여 데이터베이스를 접근하려 하면 DBMS의 **질의 처리기**를 통해서 기계어 코드로 번역된다.
* DBMS의 **런타임 데이터베이스 관리기**에 의해 데이터베이스가 접근된다.
* 이 과정에서 사용자가 원하는 테이블이 데이터베이스에 존재하는가, 데이터 조작어를 입력한 사용자가 해당 테이블을 접근할 수 잇는 권한이 있는가, 테이블에 어떤 접근 경로들이 존재하는가 등을 **시스템 카탈로그를 접근하여 확인**한다.
* 여러 사용자가 공용 데이터베이스를 접근할 때 생길 수 있는 데이터 불일치를 해결하기 위해서 **동시성 제어 모듈이 사용**된다.
* 데이터베이스를 접근하는 도중에 시스템이 다운되면, 다운되기 직전의 일관된 데이터베이스 상태를 복구하기 위해서 **회복 모듈**이 사용된다.
* 동시성 제어 모듈과 회복 모듈을 합쳐서 **트랜잭션 관리 모듈**이라 부른다.

#### 클라이언트 - 서버 데이터베이스 시스템

> 클라이언트-서버 아키텍처는 클라이언트와 데이터베이스 서버가 직접 연결되는 **2-tier Model**과, 클라이언트와 데이터베이스 서버 사이에 **응용 서버**(Application Server)가 추가된 **3-tier Model**로 구분한다.

* **2-Tier Model** : 어플리케이션의 논리(DB관련 로직)가 클라이언트와 서버에 흩어져 있다.
* **3-Tier Model** : 어플리케이션의 논리가 어플리케이션 서버에만 포함되어 있다. 서비스 요청과 응답이 클라이언트와 어플리케이션 서버 간에만 전송되기 때문에 성능이 향상된다. 또한 응용 소프트웨어를 다수의 클라이언트 대신에 소수의 어플리케이션 서버에 설치하게 되므로 구현 및 유지보수가 용이하다.

클라이언트-서버 데이터베이스 시스템의 장점은 기존의 데이터베이스를 보다 넓은 지역에서 접근할 수 있고, 성능이 향상되며, 하드웨어 비용이 절감된다는 것이다. 또한 다양한 컴퓨터 시스템을 사용할 수 있다. 예를 들어, 클라이언트는 PC에서 윈도우 운영 체제를 사용하고, 서버는 워크스테이션이나 메인프레임에서 UNIX 운영 체제를 사용할 수 있다. 보안이 다소 취약할 수 잇따는 것은 클라이언트-서버 데이터베이스 시스템의 단점이다.