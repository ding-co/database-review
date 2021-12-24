## [Introduction to Database]

### _Data & Database_

- Data

  - A formal description of an entity, event, phenomena, or idea <br/>
    that is worth recording
  - 정형화되고 기록할 만한 가치가 있다고 판단되는 <br/>
    어떤 현상이나 사건, 아이디어에 대한 묘사

- Database (DB)
  - Data + Base
  - An integrated collection of <br/>
    persistent data <br/>
    representing the information of interest <br/>
    for various programs that compose the computerized <br/>
    information system of an organization.
  - Data are separated from the programs that use them. <br/>
    (DB <> DBMS)
  - 조직이나 개인이 사용하는 조작 가능한, 저장된 데이터의 모임.

### _DBMS_

- set of programs to access the data
- convenient, efficient to use 한 환경 제공
- DB applications (사용 예)
  - banking, airlines, universities, sales, <br/>
    manufacturing, human resources
- Commercial Systems (상용화)
  - Oracle, IBM DB2, ...

### _Database 기반 시스템_

- DB - DBMS - Web Server/Middleware - Application User
- Application Developer (ODBC/JDBC)
- DBA (SQL), DB에 직접 접근 가능 (DB 관리자)

### _File Systems_

- File System (Disk File System/Program/Software)
  - part of OS
  - stores programs, data, documents, or anything
  - (in disk)
- 과거, 응용 프로그램 별도로 각각 만들어서 <br/>
  그에 대한 필요한 데이터 파일도 각각 만들어 작업했음 <br/>
  (응용 프로그램들이 각각의 별개의 데이터 파일과 1:1로 연결)
- Drawbacks of using file systems
  - Data redundancy and inconsistency
  - Difficulty in accessing data
    - 각 데이터 포맷이 달라서 접근 방법 다를 수 있음
  - Data dependency
    - 어떤 응용 프로그램은 특정 데이터 파일에 접근하는 용도로만 업무 수행 가능
    - 응용 프로그램과 데이터 file이 매우 tight 한 관계
  - Data isolation
    - 데이터가 고립되지 않고 공유되어야 함
    - 응용 프로그램이 데이터 파일 사용 중이면 다른 응용 프로그램이 접근 불가
  - Integrity problems
    - Integrity Constraint (무결성); 결점이 없는 상태
    - 일반 파일 시스템에서는 은행 계좌 잔고가 항상 양수여야 하는 조건 위해 <br/>
      코드 일일이 다 작성해야 하는 단점 있음
    - DBMS가 알아서 항상 무결성 만족시키도록 할 수 있음
  - Atomicity of updates
    - 파일 시스템에서는 갱신의 원자성 보존되지 않음
    - ex) A 계좌 -> B 계좌로 500원 옮김
      - 돈 옮기던 도중에 시스템 죽음 (500원 중간에 증발)
      - 트랜잭션의 원자성 보존 필요 (DBMS는 알아서 해줌)
  - Concurrent access by multiple users
    - 여러 사용자들이 동시에 Data file 접근 불가 (file system)
    - DBMS는 여러명 동시 접근 가능
  - security problems

### _DBMS_

- 모든 응용 프로그램들을 하나의 DBMS로 관리 가능
- 데이터의 종속성과 중복성 문제 해결
  - 중복된 데이터 여러 곳에 저장하지 않고 한 곳에만 잘 저장
- DB 공유, 관리 시스템
- DBMS 장점
  - 데이터 중복(redundancy) 최소화
  - 데이터 공용(sharing)
  - 일관성(consistency) 유지
  - 무결성(integrity) 유지
  - 보안(security) 보장
  - 표준화(standardization) 용이
    - std_id, stid (서로 다른 테이블의 각 컬럼 명칭) -> 표준화!
  - 전체 데이터 요구 조정
- DBMS 단점
  - 비용: H/W, DBMS, 운영비, 교육비, 개발비
  - 프로그램 복잡화 (JDBC/ODBC 통해 sql 작성해서 DB에서 다시 데이터 끌어옴)
  - 성능상 오버헤드
    - 큰 DB에서 데이터 찾을 때 속도 저하 발생 가능 등 여러 문제...

### _Data Independence Property_

- 추상화 수준/단계
  - Level 3: View Level (프로그램의 데이터 구조)
  - Level 2: Logical Level (데이터베이스의 논리적 구조)
  - Level 1: Physical Level (데이터베이스의 물리적 구조)
- Physical data independence
  - physical level에서 어떤 데이터 변화가 일어나도 logical level 영향 X (독립성 보장)
- Logical data independence
  - logical level 에서 어떤 데이터 변화가 일어나도 view 레벨에서 영향 X or 최소화
- Levels of Abstraction
  - View Level: hide details of data types, information
  - Logical Level: column, data type
  - Physical Level: record

### _DBMS Architecture_

- User Query (질의)
- Query Processor (질의 처리기)
- storage manager
- disk storage

### _Evolution of DB technology_

- 1960s
  - Data collection, 네트워크 형태의 DBMS
- 1970s
  - RDB model
- 1980s
  - RDBMS, Application-oriented DBMS
  - RDBMS 상용화 됨 (오라클)
  - SQL 표준으로 제정됨
  - 병렬/분산 DB
  - OO-DBMS 소개됨
- 1990s
  - Data mining, Data warehousing, web db search engines
  - OR-DBMS
  - 수 TB 규모의 데이터 웨어하우스
- 2000s
  - Stream data management and mining (IoT)
  - Semantic web technology (XML)
- 2010s
  - Big Data
  - NoSQL, Hadoop, Map Reduce, ...

### _Relational Model_

- Data model
  - Data 표현 방법
    - List? Tree? Graph? Array?
  - A collection of tools for describing
    - data, data relationships, data semantics, data constraints
  - DBMS마다 data model 다를 수 있음
  - 주요 data model
    - Relational data model
    - Entity-Relationship(E-R) data model
      - ER data model에 기반한 상용 DBMS는 없음!
      - DB 설계에 주로 이용됨! (DB 구축 전)
    - Object-Oriented/Object-Relational
      - OR-DBMS (현재 대부분의 RDBMS)
    - 기타; Network, Hierarchical, ...
  - Relational Model (관계형 모델)
    - Relation(table) 기반한 모델, 사용 편리, 성능 우수
    - SQL은 RDB에만 적용되는 표준 질의어!
  - Relational Model 주요 개념
    - Domain (type): Attribute가 가질 수 있는 값의 집합
      - Domain(학년) = {1,2,3,4}
    - Attribute (field, column): 속성
    - Tuple (row, record): set of values for attributes, 행
    - Relation (table): set of tuples (record, row)
    - Database: set of relations (tables)
- Schema vs. Instance
  - Schema (Scheme)
    - 뼈대(구조)
    - the logical/skeletal structure of the database
    - physical schema, logical schema
    - 어떤 테이블의 이름, 테이블의 여러 column(attribute)
  - Instance
    - 뼈대(구조)에 들어가 있는 실제 Contents (variables 같은 것, type은 schema)
    - 찰나의 순간, DB의 스냅샷
    - the actual content of the database at a particular point in time
    - 실제 내용물 (데이터 계속 변화 가능)

### _Key_

- Key: Tuple을 구별하기 위한 Attribute 집합
  - Relation은 동일한 tuple이 있을 수 없음 (완전히 동일한 row 중복 불가)
    - row 중 하나의 값 다른 것은 괜찮
  - 학생 테이블의 학번 컬럼, 주민번호 컬럼
    - 동일한 학번 or 동일한 주민번호 불가
    - {학번, 주민번호}도 key로 가능
    - {학번, 이름}도 가능
  - 이름 컬럼만은 Key가 아님 (동명이인 가능)
- Superkey (수퍼키)
  - Relation에서 Unique하게 Tuple을 식별할 수 있는 Attribute의 집합
  - Key == SuperKey
  - 유일성
- Candidate Key (후보키)
  - SuperKey 중에서 Minimal 한 Key
  - Minimal: Attribute 집합에서 하나의 Attribute라도 빼면 더 이상 Key가 아님
  - 유일성 + 최소성
  - {주민번호, 학번}은 Candidate Key가 아님, 하지만 Super Key임
    - 두 attribute 중 하나 빼더라도 key 가능
  - {주민번호}는 minimal한 Superkey 이므로 candidate key 가능
- Primary Key (기본키/주키, PK)
  - Candidate Key 중 하나 선택 (Relation을 정의할 때 선택)
  - Candidate key 중에서 선택되지 않은 key => alternative key (대체키)
  - Entity Integrity: PK는 NULL이 될 수 없음
- Foreign Key (참조키/외래키, FK)

  - 타 relation을 참조하는 attribute
  - 참조하는 relation에서 key가 아닐지라도, 참조되는 relation에서 PK인 경우
  - 참조하는 테이블 (Referencing) -> 참조받는 테이블 (Referenced)
  - Referential Integrity: FK 값들이 반드시 참조되는 relation의 PK 값에 존재하거나 NULL이어야 함

- NULL
  - unknown/undefined
  - 모든 Domain은 NULL 값 포함 (따로 not null 안한다고 가정)

#

Quiz 1

- 학생, 교수, 학과 테이블의 key들을 모두 찾기
- 각 key가 왜 성립하는지 설명

#

### [Note]

- entity (개체), object (객체)
- integrated (통합된)
- 학사정보시스템; 학생의 학번, 주민번호, 이름, 학년, 전공 등 <br/>
  (data: 기록할 만한 가치가 있는 정보)
- DB는 컨텐츠 자체
- DBMS (System/Software/Program)
- 서버에 S/W를 띄움 <br/>
  => s/w는 instance, 메모리 상에 프로그램이 올라가서 서버에서 돎
- Connectivity (연계)
- SQL (Structured Query Language, 구조화된 질의어) <br/>
  DB에 접근 가능, 필요 data 추출
- 파일 시스템을 사용하면서 생기는 불편한 점들을 DBMS 사용으로 해소
- drawback (단점/문제점)
- redundancy (중복성)
- inconsistency (불일치성/부정합성)
- CSV (Comma Separated Value)
- dependency (의존성)
- isolation (고립성)
- integrity constraint (무결성); 결점이 없는 상태
- Atomicity (원자성)
- Concurrent (동시의)
- Concurrent <> Simultaneous (동시의)
  - Concurrent; 잠시 TV 봤다가 잠시 공부했다가 ~ (CPU 1개)
  - Simultaneous; 2명이 있고 한 사람은 TV만 보고 다른 사람은 공부만 함 (CPU 2개)
- Independence (독립성)
- semantics (의미)
- constraint(s) (제약사항)
- relation (table, 표)
- set (집합)
- candidate (후보)
