# Introduction to the Relational Model

## _Contents_

- Structure of Relational Databases
- Database Schema
- Keys
- Relational Query Languages
  - SQL
  - Relational Algebra Operations

## _Relational Database_

- Example of a Relation
  - a set of tuples
  - ex. Account_branch(account-number, branch-name, balance)
- Example of a Relation with terms
  - attributes(columns)
  - tuples(rows)
  - ex. Professor(id, name, dept_name, salary)
- Attribute Types (형)
- 각각의 attribute는 이름이 있음
- (attribute) domain; 각각의 attribute가 가질 수 있는 값의 집합
  - ex. 학년 = {1, 2, 3, 4, null}
- null; undefined, special value, null은 모든 domain의 멤버
- attribute values are atomic, indivisible
  - multi-valued attribute values (atomic X)
    - ex. {100, 200}
  - composite attribute values (atomic X)
    - ex. {firstName: 'a', lastName: 'b'}
  - 위 두가지 경우는 RDB에 존재할 수 없음!
- null은 여러 operation에 문제 발생 가능

## _Relation Schema and Instance_

- Schema; 뼈대
  - R = (A1, A2, A3, ... An)
  - ex. Customer-schema = (customer-name, customer-street, customer-city)
    - Customer-schema 취하는 테이블 명칭은 customer (소문자)
    - customer (Customer-schema)
    - customer (customer-name, customer-street, customer-city) <- customer 스키마
- Instance; 찰나의 DB 컨텐츠 들어가 있는 상태/순간
- r(R)
  - r: relation/table
  - R: schema
- relation r
  - D1 x D2 x ... x Dn 의 subset <- 도메인
  - r(A1, A2, ... , An) <- Attribute
  - (a1, a2, ... , an) <- n tuples
- X (Cartesian Product); 카티션 곱, 각각 도메인 모든 값들의 combination
- n (degree of r(R)); attribute/column 개수, r(R)의 차수
- ex. D1 = {a, b}, D2 = {1, 2, 3}
  - D1 X D2 = {(a, 1), (a, 2), (a, 3), (b, 1), (b, 2), (b, 3)}
  - 2 x 3 => 총 6개 조합
- ex. customer(cust_name, cust_street, cust_city) <= 스키마
- 테이블 안에 컨텐츠 다 나열해서 쓴 것은 Instance

## _Relation Instance_

- relation instance; current values
- r(relation, 집합), t(tuple)

## _Relations are Unordered_

- 무순, 순서가 없는
- 튜플의 순서는 아무 의미 없음
- arbitrary order (무작위 순서)

## _Database_

- multiple relations/tables
- 필요한 정보 하나의 테이블로 막 넣으면 안됨
  - 정보 반복되서 나옴
  - null values의 필요성 (어쩔 수 없이 넣어야 하는 경우 많아짐)
    - null value는 최소화 시켜야 함!
- design good relational schemas using Normalization

## _Keys_

- superkey는 Schema 안에 포함되어 있는 attribute들의 집합
  - 튜플 unique
- superkey 중 minimal한 key는 candidate key
  - attribute 하나라도 제거해서 공집합이거나 <br/>
    tuple unique하지 않으면 candidate key 아님
- candidate key 중 하나를 PK로 설정
  - 선택되지 않은 다른 key는 alternative key
- Foreign key
  - constraint
  - referencing table
    - 참조하는 FK
    - FK의 도메인은 PK의 값이거나 NULL (FK Constraint)
  - referenced table
    - attribute가 PK임

## _University Database_

- student(id, name, dept_name, tot_cred)
  - PK; id
- takes(id, course_id, sec_id, semester, year, grade)
  - PK; (id, course_id, sec_id, semester, year)
  - FK; takes(id) -> student(id)
- instructor(id, name, dept_name, salary)
  - PK; id
- advisor(s_id, i_id)
  - PK; (s_id, t_id)
  - FK; advisor(s_id) -> student(id), advisor(i_id) -> instructor(id)

## _Entity Relationship Diagram_

- ERD (개체 관계 다이어그램)
  - ER Modeling 결과
  - ER Model에 기반한 상용 DBMS는 없음
  - DB 설계 시 사용!

## _E-R Diagram for the Banking Enterprise_

- 네모(직사각형); Entity (set)
- 다이아몬스; Relationship (set)
- 타원; Attribute
- 직관적으로 바로 DB 이해 가능
- but, ERD는 표준이 없음!

## _Determining keys from E-R Sets_

- Strong entity set
  - weak 아닌건 다 strong
- Weak entity set
  - ex. 버스 좌석
    - 창측 36번 A번
    - 버스가 다름
    - 버스 좌석은 weak entity set
      - 창측 36번 A번 좌석은 목포행 또는 광주행으로 붙어야 함
      - 좌석 번호는 PK가 아님
      - discriminator라고 함
      - discriminator; PK 역할 못함, 다른 strong entity의 PK와 조합되어야 PK 될 수 있음
- relationship set
  - relational cardinality
    - 교수; p1, p2 (p_id가 PK)
    - 학생; s1, s2, s3, s4, s5 (s_id가 PK)
    - 교수와 학생의 관계 - advisor (relationship set)
    - 교수 1명당 학생 1명 지도 => cardinality; 1:1
      - PK는 p_id or s_id (둘 중 어느것이든 상관없음)
    - 교수 1명이 여러 학생 지도 => cardinality; 1:m (1:n)
      - PK는 s_id
      - many 쪽
    - 교수가 여러 학생 지도 + 학생이 복수전공 => cardinality; m:n
      - PK는 {p_id, s_id}
      - 두 개 union
- relationship에 참여하는 entity set 개수가 2개이면 binary라고 표현

## _Relational Query Language_

- Query Language (질의어)
- procedural/pure; 절차적인
  - 이론상으로 존재하는데 상용 DBMS로 조작할 수는 없음
  - Relational Algebra; relational operators로 이루어져 있음
  - Tuple Relational Calculus
  - Domain Relational Calculus
- non-procedural/declarative
  - SQL
  - 어떤 정보가 필요한지만 표현! (what data O)
  - 방법은 기술 X (how X)
  - ex. SELECT 컬럼 FROM 테이블명칭 WHERE 컬럼이용한조건

## _From SQL to Relational Algebra_

- SQL 던져도 내부적으로는 relational algebra로 변환되어 수행됨
- query -> parsing & translator -> relational algebra expression <br/>
  optimizer -> execution plan -> evaluation engine -> query output

### [Quiz]

- SELECT ... FROM ... WHERE ...
  - 쿼리 결과

#

### [Note]

- atomic (원자성의)
