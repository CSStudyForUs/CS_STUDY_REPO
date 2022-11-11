# 데이터베이스

---

> 데이터를 각각의 파일 단위로 저장할 때 생기는 데이터 종속성, 중복성, 무결성 문제를 해결하기 위해 사용한다.
> 

- **데이터베이스 특징**
    1. 독립성: DB 사이즈를 늘리거나 성능 향상을 위해 데이터 파일을 늘리거나 추가하더라도 관련 응용 프로그램은 수정할 필요가 없다.
        
        → 물리적 독립성: DB 사이즈를 늘리거나 추가해도 관련 응용 프로그램은 수정할 필요가 없다.
        
        → 논리적 독립성: DB는 다양한 응용 프로그램의 논리적 요구를 만족시켜줄 수 있다.
        
    2. 무결성: 데이터 유효성 검사를 통해 데이터 무결성을 유지한다.
    3. 보안성: 인가된 사용자만 DB에 접근할 수 있도록 권한을 설정한다.
    4. 일관성: 연관된 정보를 논리적 구조로 관리해 하나의 데이터 변경 시 불일치성을 배제할 수 있다.
    5. 데이터 중복 최소화: 데이터를 통합해서 관리할 수 있다.

- **데이터베이스 성능에 영향을 미치는 요인**
    
    → 디스크 I/O : 디스크 드라이브의 플래터를 돌려서 읽어야 할 데이터가 저장된 위치로 디스크 헤더를 이동시킨 후 다음 데이터를 읽는 것.
    
    메모리는 물리적으로 한정된 자원이므로, 디스크 I/O를 최소화하고 버퍼 캐시 효율을 높일 때 효율적인 데이터베이스 I/O 튜닝이 된다.
    
    - **버퍼 캐시 효율 향상 → 버퍼 캐시 히트율 (BCHR)**
        
        물리적인 디스크 읽기 없이 메모리에서 데이터 블록을 찾은 비율.
        
        = (1 - (물리적 I/O) / (논리적 I/O)) * 100
        
        ⇒ 물리적 I/O가 수행되면 DB 버퍼 캐시에 해당 테이블 블록이 생기기 때문에, 물리적 I/O는 같은 SQL을 여러 번 수행할수록 줄어든다.
        
    
    - **Sequential I/O vs Random I/O**
        
        Sequential Access: 레코드 간 논리적, 물리적 순서를 따라 차례로 데이터를 읽는 방식
        
        Random Access: 레코드의 논리적, 물리적 순서를 따르지 않고 한 건을 읽을 때 한 블록 씩 접근하는 방식
        
        ⇒ Sequential Access에 의한 선택 비중을 늘린다.
        

# Key

---

검색, 정렬 시 Tuple을 구분할 수 있는 기준이 되는 Attribute

1. **Candidate Key (후보키)**
    
    유일성 (Key로 하나의 Tuple을 식별할 수 있음) 과 최소성 (꼭 필요한 속성으로만 구성) 을 모두 만족하는 키
    
2. **Primary Key (기본키)**
    
    후보키 중 선택된 키. Null 값과 중복 값 허용 안 됨.
    
3. **Alternate Key (대체키)**
    
    후보키 중 기본키를 제외한 키
    
4. **Super Key (슈퍼키)**
    
    유일성은 만족하지만 최소성은 만족하지 못하는 키
    
5. **Foriegn Key (외래키)**
    
    다른 릴레이션의 기본키를 참조하는 속성의 집합
    
6. **Foriegn Key (외래키)**
    
    다른 릴레이션의 기본키를 참조하는 속성의 집합
    

# Join

---

> 두 개 이상의 테이블이나 DB를 연결하여 데이터를 검색하는 방법
> 

- **INNER JOIN**
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b57d8f2b-8959-4f2a-8519-0e7b810c42ec/Untitled.png)
    
    ```abap
    SELECT
    A.NAME, B.AGE
    FROM EX_TABLE A
    INNER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
    ```
    

- **LEFT OUTER JOIN**
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/29786535-2f29-4943-83e7-39753b48d9b1/Untitled.png)
    
    ```abap
    SELECT
    A.NAME, B.AGE
    FROM EX_TABLE A
    LEFT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
    ```
    

- **RIGHT OUTER JOIN**
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/230bf0a5-6fd5-4d92-95e6-2b741ed69b88/Untitled.png)
    
    ```abap
    SELECT
    A.NAME, B.AGE
    FROM EX_TABLE A
    RIGHT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
    ```
    
- **FULL OUTER JOIN**
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/32f9abaa-b963-4794-af1d-c535bba13be6/Untitled.png)
    
    ```abap
    SELECT
    A.NAME, B.AGE
    FROM EX_TABLE A
    FULL OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
    ```
    

- **CROSS JOIN**
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/802485de-1cbf-41fa-a7af-1c87dd649344/Untitled.png)
    
    ```abap
    SELECT
    A.NAME, B.AGE
    FROM EX_TABLE A
    CROSS JOIN JOIN_TABLE B
    ```
    

- **SELF JOIN**
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ba6b3808-fe11-4070-a0b0-8977a961f1b9/Untitled.png)
    
    ```abap
    SELECT
    A.NAME, B.AGE
    FROM EX_TABLE A, EX_TABLE B
    ```
    

# Index

---

> 데이터베이스 테이블 내 모든 데이터를 검색해 원하는 결과를 가져올 경우 시간이 오래 걸리기 때문에, 컬럼의 값과 레코드가 저장된 주소를 키와 값의 쌍으로 인덱스를 만들어 두는 것
> 

인덱스를 사용하면 원하는 값을 탐색하는데는 빠르지만, 새로운 값을 추가하거나 삭제, 수정하는 경우 쿼리문 실행 속도가 느려진다. 따라서 데이터의 저장 성능을 희생하고, 데이터의 읽기 속도를 높이기 위해 사용한다. 인덱스의 크기가 비대해지지 않게 적당한 값을 선택해 인덱스를 생성하는 것이 중요!

- 인덱스 관리 알고리즘
    1. B+Tree 인덱스 일고리즘
        
        칼럼의 값을 변형하지 않고 원래의 값을 이용해 인덱싱하는 알고리즘.
        
    2. Hash 인덱스 알고리즘
        
        칼럼의 값으로 해시 값을 계산해 인덱싱하는 알고리즘.
        
        칼럼의 값을 해싱해 인덱스하기 때문에 특정 문자로 시작하는 값으로 검색할 때는 사용 불가하다. 따라서 동등 연산 (=) 에 특화되어 있다.
        

## Primary Index vs Secondary Index

---

- **Primary Index (Clustered Index)**
    
    데이터 블록 안 행들의 조직과 저장소에 영향을 미친다.
    
    테이블 당 하나만 가질 수 있다.
    
    Insert 시 데이터가 정렬되고, index는 data block의 첫 번째 레코드 주소값을 갖게 된다.
    
    데이터가 정렬되어 저장되므로, 범위를 이용해 질의 하는 것에 유리하다.
    
    ![[https://gwang920.github.io/database/clusterednonclustered/](https://gwang920.github.io/database/clusterednonclustered/)](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a05f2a72-2c07-4ac2-b7c1-8c17f364a4df/Untitled.png)
    
    [https://gwang920.github.io/database/clusterednonclustered/](https://gwang920.github.io/database/clusterednonclustered/)
    

1. 행 데이터를 정렬한 후에 루트 페이지를 생성한다.
2. Root 페이지는 Leaf 페이지의 주소로 구성하고, Leaf 페이지는 실제 데이터 페이지로 구성된다.
3. 클러스터드 인덱스 순서로 레코드가 하드디스크에 저장된다. 클러스터드 인덱스를 따로 지정하지 않으면 기본 키가 클러스터드 인덱스가 된다.

- 사용
    
    테이블 데이터가 자주 업데이트 되지 않는 경우
    
    범위의 조회, Group By 조회, 읽기 작업이 많은 경우
    
- **Secondary Index (NonClustered Index)**
    
    Primary Key 이외의 정렬 기준이 있을 경우 사용하며, 테이블 당 여러 개 가질 수 있다.
    
    index가 data record의 모든 주소값을 가지고 있어야 하며, 정렬되어 있지 않기 때문에 범위 조건으로 검색하면 많은 I/O가 발생한다.
    
    index는 모든 레코드에 대한 색인 데이터를 가지고 있어야 하기 때문에 update, delete, insert 시 오래 걸릴 수 있고 clustered index에 비해 더 많은 공간을 차지하게 된다.
    
    ![[https://gwang920.github.io/database/clusterednonclustered/](https://gwang920.github.io/database/clusterednonclustered/)](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cc33f5c2-1935-48a3-bbe0-b4e1222488de/Untitled.png)
    
    [https://gwang920.github.io/database/clusterednonclustered/](https://gwang920.github.io/database/clusterednonclustered/)
    
    1. Index로 구성한 열을 정렬한 후 위치 포인터를 생성한다. (키값 - 데이터)
    2. 데이터 페이지는 그냥 둔 상태에서 별도의 인덱스 페이지를 따로 만든다.
    3. 루트 페이지 → 리프 페이지 → 데이터 페이지
    4. 검색 속도는 느리지만 페이지 분할이 적게 일어나 입력, 수정, 삭제가 빠르다.

- **장단점 비교**
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8916a44b-0624-40eb-bc8e-b18736a979a7/Untitled.png)
    
    [https://velog.io/@sweet_sumin/클러스터드-인덱스-Clustered-Index-넌-클러스터드-인덱스-Non-Clustered-Index](https://velog.io/@sweet_sumin/%ED%81%B4%EB%9F%AC%EC%8A%A4%ED%84%B0%EB%93%9C-%EC%9D%B8%EB%8D%B1%EC%8A%A4-Clustered-Index-%EB%84%8C-%ED%81%B4%EB%9F%AC%EC%8A%A4%ED%84%B0%EB%93%9C-%EC%9D%B8%EB%8D%B1%EC%8A%A4-Non-Clustered-Index)
    

- **Index의 성능에서 고려해야 할 사항**
    1. 모든 쿼리에 Index를 적용할 경우 INSERT, DELETE, UPDATE 쿼리문을 실행할 때 INDEX에 대한 데이터도 처리해야 하는 성능 손실이 발생한다.
    2. 데이터의 형식과 인덱스의 범위에 따라 성능이 악영향을 미칠 수 있다.
        
        (이름, 나이, 성별 세 필드를 가지고 있는 테이블의 경우 성별로 인덱스를 생성하면 인덱스를 읽어도 많은 디스크 I/O가 발생하기 때문에 비효율적이다.)
        

# Normalization

---

> 한 릴레이션에 여러 Entity의 Attribute를 혼합하면 정보가 중복 저장되며 저장 공간을 낭비할 수 있다.
> 

- 갱신 이상의 종류
    1. 삽입 이상: 튜플 삽입 시 특정 속성에 해당하는 값이 없어 NULL이 입력된다.
    2. 삭제 이상: 하나의 자료를 삭제할 때 원치 않는 정보 손실이 발생할 수 있다.
    3. 수정 이상: 일부 튜플만 갱신되어 데이터가 불일치한다.

## 제 1 정규형 (원자값)

---

1. 각 컬럼이 하나의 속성을 가져야 한다.
2. 하나의 컬럼은 같은 종류나 타입이어야 하며, 유일해야 한다.
3. 컬럼의 순서가 상관 없어야 한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e90a2276-169e-4f2d-9236-a6961354125f/Untitled.png)

(정규화 전)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/598be29a-5808-47d7-8cb2-fedc0a8849db/Untitled.png)

(정규화 후) → 하나의 컬럼이 두 개의 값을 가지고 있는 것을 방지.

## 제 2정규형 (부분 종속 제거)

---

모든 컬럼이 완전 함수 종속을 만족해야 한다.

⇒ 기본 키의 부분 집합이 결정자가 되어서는 안된다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a8ccf1bc-7b07-4af8-adae-2cb2fbb8c41f/Untitled.png)

기본 키가 (학생번호 + 과목) 일 때 지도 교수는 기본키의 부분 집합인 과목에 완전히 종속된다. 

## 제 3정규형 (이행 종속 제거)

---

- 기본 키를 제외한 속성들 간의 이행 종속성이 없어야 한다.
    
    A → B, B → C 일 때 A → C가 성립하면 이행 종속이라 한다.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/79c0e95a-0c2c-47bd-be18-9ad0f6033d38/Untitled.png)
    

## BCNF (Boyce-Codd Normal Form)

---

- 모든 결정자가 후보키 집합에 속해야 한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b975a186-03dc-4b78-aa3d-c183b2e0796f/Untitled.png)

기본키는 학생번호 + 과목이다.

같은 과목을 다른 교수가 가르칠 수도 있기 때문에 과목 → 지도교수 종속은 성립하지 않으나 지도교수가 가르치는 과목이 정해져 있다면 지도교수 → 과목의 종속은 성립한다. 이 때 지도교수는 후보키 집합이 아니기 때문에 BCNF를 만족하지 않는다.

---

### 정규화의 장점

- 데이터베이스 변경 시 이상 현상을 제거할 수 있다.
- 새로운 데이터 형의 추가로 인한 확장 시, 구조를 변경하지 않거나 일부만 변경해도 된다.

### 정규화의 단점

- 릴레이션 간 JOIN 연산이 많아져 질의에 대한 응답시간이 느려질 수 있다.
- 조인이 너무 많이 발생해 성능 저하가 나타날 경우 **반정규화**를 적용한다.

### 반정규화

---

정규화된 엔티티, 속성, 관계를 시스템의 성능 향상을 위해 중복, 통합, 분리를 수행하는 데이터 모델링 기법 중 하나이다.

⇒ 자주 사용되는 테이블에 액세스하는 프로세스의 수가 많고, 항상 일정한 범위를 조회하는 경우, 테이블에 대량의 데이터가 있어 처리 중 이슈가 발생하는 경우, 지나치게 조인을 많이 사용해 데이터를 조회하는 것이 어려운 경우 사용한다.

# Transaction

---

논리적인 작업 셋을 전부 완성하도록 작업의 완전성을 보장해주는 것.

논리적인 하나의 작업 흐름이 완전히 실행되거나, 완벽하게 실행되거나 일관성 있게 작동하는 것을 보장한다.

### 특성 (ACID)

---

1. 원자성: 트랜잭션은 모든 작업이 수행되거나, 수행되지 않아야 한다.
2. 일관성: 트랜잭션이 완료된 이후에도 데이터의 일관성을 보장해야 한다.
3. 고립성: 각각의 트랜잭션은 독립적으로 수행되어야 한다.
4. 지속성: 트랜잭션이 정상적으로 종료된 후에는 영구적으로 작업의 결과가 저장되어야 한다.

### 연산

---

크게 Commit과 Rollback이 있다.

1. **Commit**
    
    하나의 트랜잭션이 성공적으로 종료된 후 결과를 최종적으로 DB에 반영하는 연산이다.
    

1. **Rollback**
    
    트랜잭션이 비정상적으로 종료되었을 때 지금까지 실행한 연산의 결과가 취소되고, 트랜잭션 수행 이전의 상태로 돌아간다.
    

![[https://rebro.kr/162](https://rebro.kr/162)](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4cca0243-5d2e-4ef6-be01-ff258eb514c4/Untitled.png)

[https://rebro.kr/162](https://rebro.kr/162)

### 상태

---

트랜잭션에 5가지의 상태가 존재한다.

![[https://rebro.kr/162](https://rebro.kr/162)](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5231e7be-9820-4f2c-9efe-7edcb61e7844/Untitled.png)

[https://rebro.kr/162](https://rebro.kr/162)

1. 활성화 (Active): 트랜잭션이 작업을 하는 상태
2. 실패 (Failed): 오류가 발생해 실행이 중단된 상태
3. 철회 (Aborted): 트랜잭션의 비정상적 종료로 Rollback 연산을 수행한 상태
4. 부분 완료 (Partially Committed): 트랜잭션의 마지막 연산까지 실행하고 commit 요청이 들어온 상태
5. 완료(Commited): 트랜잭션이 성공 후 commit 연산을 실행한 후 상태

- **트랜잭션 적용 시 주의할 점**
    
    데이터베이스 커넥션의 개수가 제한적이므로 트랜잭션의 범위는 최소화해야 한다. 커넥션의 점유 시간이 늘어난다면 복수의 트랜잭션 사용 시 **교착 상태**가 일어날 수 있다.
    
    교착상태란, 두 개 이상의 트랜잭션이 특정 자원의 잠금을 획득한 채 다른 트랜잭션이 소유하고 있는 잠금을 요구할 경우 이도 저도 못하는 상황에서 발생한다.
    
    ⇒ 빈도를 낮추기 위해서는 
    
    1. 트랜잭션을 자주 커밋하거나, 
    2. 트랜잭션들이 테이블에 동일한 순으로 접근하게 하거나,
    3. 데이터 수정이 아닌 읽기 연산에서는 LOCK을 피한다.
    

### **데이터베이스 커넥션**

---

애플리케이션과 데이터베이스의 연결을 의미하며, 애플리케이션에서 데이터베이스에 접속하고 종료하는 일련의 과정을 의미한다.

⇒ WAS에서 미리 일정한 수의 커넥션을 만들고 필요한 시점에 애플리케이션에 제공하는 서비스 및 관리 체계를 **데이터베이스 커넥션 풀**이라고 한다.

![*http://devbox.tistory.com/entry/JSP-커넥션-풀-1*](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/db28ab1b-be04-4a5a-9725-aa8781c6aef5/Untitled.png)

*http://devbox.tistory.com/entry/JSP-커넥션-풀-1*

1. WAS가 시작될 때 일정 수의 커넥션을 미리 생성해 풀을 구성한다.
2. Request에 따라 생성된 커넥션 객체를 전달한다.
3. 일정 수 이상의 커넥션이 사용되면 새로운 커넥션을 만든다.
4. 기본 커넥션 제외, 사용하지 않는 커넥션은 종료한다.
    
    커넥션 풀은 JNDI (Java Naming and Directory Interface) 라는 네이밍 서비스를 통해 접근할 수 있다.
    

### 트랜잭션 격리 수준 (Isolation level)

---

트랜잭션에서 일관성 없는 데이터를 허용하도록 하는 수준.

트랜잭션이 DB를 다루는 동안 다른 트랜잭션이 관여하지 못하도록 하는 Locking의 범위를 줄여야 성능을 유지할 수 있다.

- **종류**
    
    [https://joont92.github.io/db/트랜잭션-격리-수준-isolation-level/](https://joont92.github.io/db/%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EA%B2%A9%EB%A6%AC-%EC%88%98%EC%A4%80-isolation-level/)
    
    1. **Read Uncommitted**
        
        Select 문이 수행되는 동안 데이터에 Shared Lock이 걸리지 않는 계층
        
        → 트랜잭션이 처리 중이거나, commit되지 않은 데이터를 다른 트랜잭션이 읽을 수 있음 → 데이터베이스 일관성 유지 불가능.
        
    2. **Read committed**
        
        Select 문이 수행되는 동안 데이터에 Shared Lock이 걸리는 계층
        
        → 트랜잭션이 수행되는 동안 다른 트랜잭션이 접근할 수 없어 대기
        
    3. **Repeatable Read**
        
        트랜잭션이 완료될 때까지 Select 문장이 사용하는 모든 데이터에 Shared Lock이 걸리는 계층
        
        → 트랜잭션이 범위 내에서 조회한 데이터 내용이 항상 동일하며, 다른 사용자는 트랜잭션 영역에 해당하는 데이터에 대한 수정이 불가 (MySQL Default)
        
    4. **Serializable**
        
        트랜잭션이 완료될 때까지 Select 문장이 사용하는 모든 데이터에 Shared Lock이 걸리는 계층
        
        → 완벽한 읽기 일관성을 보장하며 다른 사용자는 트랜잭션 영역에 해당하는 데이터에 대한 수정 및 입력이 불가
        

- **낮은 단계의 Isolation Level을 활용할 경우**
    1. Dirty Read (Read Uncommitted)
        
        어떤 트랜잭션에서 아직 끝나지 않은 다른 트랜잭션에 의한 변경사항 목격
        
    2. Non-repeatable Read (~Read Committed)
        
        한 트랜잭션에서 같은 쿼리를 두 번 수행할 때 그 사이에 다른 트랜잭션이 값을 수정하며 두 쿼리의 결과가 상이하게 나타남
        
    3. Phantom Read (~Repeatable Read)
        
        한 트랜잭션 안에서 일정 범위의 레코드를 두 번 이상 읽었을 때, 첫번째 쿼리에서 없던 내용이 두번째에서 나타나는 현상.
        

# Statement vs PreparedStatement

---

[https://webstone.tistory.com/56](https://webstone.tistory.com/56)

- **Statement의 동작 과정**
    1. SQL문의 틀을 만들고 DBMS로 전송한다.
    2. DBMS는 SQL의 틀을 컴파일 한다.
    3. SQL문 내 변수를 지정하면 DBMS는 처리문을 실행하며 변수에 값을 바인딩한다.

⇒ PreparedStatement는 1, 2번의 과정을 캐시에 담아 재사용하기 때문에 동일한 쿼리를 반복 수행할 경우 성능이 좋아진다.

# SQL Injection

---

해커에 의해 조작된 SQL 쿼리문이 데이터베이스에 그대로 전달되어 비정상적 명령을 실행시키는 공격 기법

1. 인증 우회
    
    입력 창에 값과 함께 다른 SQL 구문도 입력한다.
    
    ```abap
    SELECT * FROM USER WHERE ID = "abc" AND PASSWORD = "1234";
    SELECT * FROM USER WHERE ID = '' OR 1=1;
    ```
    

1. 데이터 노출
    
    시스템에서 발생하는 에러 메시지를 이용해 공격하는 방법이다.
    
    GET 방식으로 동작하는 URL 쿼리 스트링을 추가해 에러를 발생시키고, 오류문의 내용으로 DB 구조를 유추할 수 있다.
    

- 방어 방법
    1. input 값을 받을 때 특수문자 여부 검사
    2. SQL 오류 발생 메시지 감추기
    3. preparestatement 사용 → 특수문자를 자동으로 escaping하고 서버측에 지정된 값만을 쿼리의 변수로 설정할 수 있다. (setString)
