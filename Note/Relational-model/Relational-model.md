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

#

### [Note]

- atomic (원자성의)
-
