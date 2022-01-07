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
  -> optimizer -> execution plan -> evaluation engine -> query output

## _Relational Algebra_

- Algebra (대수); operators, operands
  - relational algebra (relation 대상으로 연산)
    - operands; relations
    - operators; basic/primitive operators (+ additional operations)
      - 기본 연산 ex. 덧셈 (`+`)
      - 곱셈 (`*`)은 기본 연산자가 아님, 덧셈 연산자들의 조합으로 표현 가능
        - additional operator
- Procedural Language
- 6개의 basic operators
  - select; 시그마 기호
  - project; 파이 비슷한 기호
  - union; U 기호
  - set difference; - 기호
  - Cartesian product; X 기호
  - rename; p 같은 기호
- 연산자들은 1개 또는 2개의 relations들을 input으로 삼아서 <br/>
  결과로 하나의 새로운 relation을 줌
  - 닫혀 있다 개념
- Selection of tuples
  - 시그마 기호로 표현
  - unary operator (단항 연산자, operand가 1개인 경우)
  - 테이블의 schema는 변함 없음
  - 조건에 맞는 튜플만 select
  - relational algebra로 표현할 수 있어야 함!
- Selection of Columns (attributes)
  - selection 이라기 보다는 projection/project 라고 함
  - 파이 기호로 표현
  - unary operator (연산항 1개임, 피연산자 => relation 1개)
  - project attributes(columns)
  - relational model에서는 중복 튜플 허용 X
  - 중복 튜플 자동으로 제거해서 결과 relation 나옴!!!!!
- Joining two relations - Cartesian Product
  - X 기호로 표현
  - 컬럼 수평으로 다 붙임
  - r X s => r 튜플 개수 x s 튜플 개슈
    - r에 있는 모든 튜플과 s에 있는 모든 튜플 join 되도록 만듦
  - Cartesian Product 연산자는 binary operator (피연산자, 즉 relation 2개)
- Union of two relations
  - 합집합
  - U 기호로 표현
  - 수학적으로 relation은 사실 tuple들의 집합임
  - 합집합 연산 성립하기 위해서는 피연산자 2개인 relation 2개가 <br/>
    compatible 해야 함!
    - 2개 relation이 schema 즉 구조가 똑같아야 함!
    - 각각 컬럼 구성이 똑같아야 함! (테이블 이름은 괜찮..)
  - 합집합 연산자는 binary operator
- Set difference
  - 차집합
  - `-` 기호로 표현
  - binary operator
  - 마찬가지로 피연산자 2개인 relation 2개가 모두 schema 같아야 함!
- Set intersection
  - 교집합
  - n자 기호 비슷
  - 두 relation 서로 compatible
  - binary operator
  - 중요) 교집합은 primitive/basic/기본 연산자가 아님!
    - 다른 연산자를 통해 교집합을 대체할 수 있음!
- Joining two relations - Natural Join (자연 조인)
  - 리본 모양 기호로 표현
  - binary operator
  - 2개의 relation을 수평적으로 합침
  - 조건: 2개의 relation 중에서 최소 하나 이상의 공통 column 있어야 함!
  - 공통 column 한번씩 합쳐짐
  - primitive operator 아님
- 2개의 table 합치는 연산자 중 primitive operator은 Cartesian Product가 유일함!
- 정리
  - Relational Model
    - Relation, tuple, attribute
    - Schema, Instance
    - keys
  - E-R Diagram
    - E-R Model
    - Keys
      - Cardinality
  - SQL vs. Relational Algebra
    - SELECT ... FROM ... WHERE
    - basic(primitive) relational operators
    - additional relational operators

### [Quiz]

- SELECT ... FROM ... WHERE ...
  - 쿼리 결과
- r n s 를 다른 연산자를 통해 대체해보기!
  - basic operator 이용해서
  - 집합 연산자를 사용해서 대체 가능 (집합 연산자들 중에서 기본 연산자)

#

### [Note]

- atomic (원자성의)
- operand (연산항, 피연산자)
- relational algebra에서는 어떤 operation 가해도 그 결과는 다시 relation으로 나옴!
- compatible (호환성 있는)
