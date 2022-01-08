# Relational Algebra

## Contents

- Relational Algebra; 관계 대수
  - 대수; operator / operand
    - operator
      - basic/primitive operator
      - additional operator

## Relational Algebra

- Relational Model Query?
- Relational Algebra?

## Database 이용 예

- Design & Create Database (using DDL, DCL)
  - DB Schema (뼈대) 만들기
- Load Data (using DML)
  - 실제로 데이터 적재
- Execute Query / Modify Data (using DML)
  - 필요한 요구사항을 Query로 만들어서 실행
  - 필요한 데이터 수정
  - 반복

## Query?

- Query (질의)
  - RDB => SQL
  - Relational Algebra
- Relational Query Languages
  - 새로운 Relation 만들어내는 연산
    - closed (닫혀있다)
    - 열려있는 것은 결과로 relation 안나오는 경우임
  - Query Language
    - 대표적으로 2개 => Relational Algebra, SQL

## Basic Operation

- select
- project
- union
- set difference
- cartesian product
- rename

## Relational Algebra

- Procedural Language (절차적인 언어)
- what data + how
- 6개의 기본 연산자들이 있음
- unary operator / binary operator

## Select

- select/selection 연산자
- 시그마 기호로 표현
- 시그마 p (r)
  - 시그마가 연산자
  - p는 연산 조건
    - selection predicate (선택 조건)
    - term들이 and, or, not 같은 것으로 connected 되어 있음
    - 비교 연산자도 있음
  - r는 relation
- Get a Horizontal Subset!
- 연산 결과는 새로운 relation
- unary operator (하나의 operand/relation만 취함)

## Project

- project/projection
- 파이 기호로 표현
- 파이 A1, A2, ..., Ak (r)
  - 컬럼에 해당하는 것만 가져와서 새로운 relation 만듦
- Get a Vertical Subset!
- may be used for reordering the columns
- unary operator (하나의 operand/relation만 취함)
- Duplicate rows removed from result, since relations are sets!!
  - 동일한 튜플/행들은 결과에서 제거
  - relation은 기본적으로 튜플의 집합이기 때문에 동일한 원소 존재할 수 없음

## Union

- 합집합
- U자 기호로 표현
- r U s valid 조건
  - r, s 두 relation이 동일한 스키마를 가져야 함!
    - same arity (컬럼 개수 같아야 함)
  - 각각의 attribute domain이 compatible (동일!)
    - 컬럼 이름과 순서가 동일해야 함
    - 결국 스키마 동일!
- binary operator

## Set-Difference

- 차집합
- `-` 기호로 표현 (간혹 `/` 로 표현하기도 함)
- r - s valid 조건 (같은 스키마!)
  - same arity
  - attribute domain들이 compatible
- binary operator

## Cartesian-Product

- 카티션 곱, product
- `x` 기호로 표현
- r(R)과 s(S)가 disjoint 하면?
  - 테이블 r이 R 스키마 취하고, 테이블 s가 S 스키마 취함
  - R n S => 공집합 (같은 것이 없음)
  - 만약 disjoint 하지 않으면 => 카티션 곱 하기 전에 반드시 renaming 필요! (p 기호)
- binary operator

## Rename

- 이름 바꾸는 연산자
- p 기호로 표현
- p d (E)
  - d는 소첨자
  - E는 Relational Algebra Expression
  - E 결과는 relation => 그것을 d라 부르겠다!
- 카티션 곱할 때 disjoint 하지 않으면 rename 사용

### [Quiz]

- Example
  - 학생, 교수, 학과 테이블
  - 각 쿼리에 대해서 relational algebra로 표현해보기!
  - basic operator 만 사용하기

#

### [Note]

- Relational Algebra
  - 개념/이론상으로만 존재하는 언어임!
  - 이것을 직접 활용하여 수행할 수 있는 DBMS는 없음
- relation; set of tuples
- section (강좌)
