# :pushpin: SQL vs NOSQL

![image](https://user-images.githubusercontent.com/69101568/211065609-09645188-907f-4840-99d7-f9a4dcb92242.png)

## :computer: 관계형 데이터베이스

_구조화된 쿼리 언어(**S**tructured **Q**uery **L**anguage) 사용_

- 관계형 데이터베이스 관리 시스템(RDBMS)에서 데이터를 저장, 수정, 삭제 및 검색
- 데이터는 정해진 데이터 스키마에 따라 테이블에 저장
- 데이터는 관계를 통해 여러 테이블에 분산
- 스키마를 준수하지 않은 레코드는 테이블에 삽입 불가
- 관계형 데이터베이스 예시
  
        - MySQL
        - Oracle
        - SQLite
        - MariaDB
        - PostgresSQL

---

## :computer: 비관계형  데이터베이스

_관계형 데이터베이스를 뺀 나머지 유형을 총칭_

:heavy_check_mark: 비관계형 데이터베이스 유형

- Key-Value 타입
  - 속성을 Key-Value의 쌍으로 나타내는 데이터를 배열의 형태로 저장
  - Key : 속성 이름
  - Value : 속성에 연결된 데이터 값
  - ex) Redis, Dynamo
- 문서형 데이터베이스
  - 테이블이 아닌 문서처럼 저장
  - 대부분 json과 유사한 형식의 데이터를 문서화하여 저장
  - 각각의 문서는 하나의 속성에 대한 데이터를 가지고 있고, 컬렉션이라고 하는 그룹으로 묶어서 관리
  - ex) MongoDB
- Wide-Column Store 데이터베이스
  - 열(column)에 대한 데이터를 집중적으로 관리
  - 각 열에는 key-value 형식으로 데이터 저장, 컬럼 패밀리라고 하는 열의 집합체 단위로 데이터 처리
  - 하나의 행에 많은 열을 포함할 수 있음 -> 유연성 높음
  - ex) Cassandra, HBase
- 그래프(Graph) 데이터베이스
  - 자료구조의 그래프와 비슷한 형식으로 데이터 간의 관계를 구성하는 데이터베이스
  - ex) Neo4J, InfiniteGraph
  
---

## :computer: SQL 데이터베이스와 NoSQL 데이터베이스 장단점

:heavy_check_mark: SQL
- 장점
  - 명확하게 정의된 스키마
  - 관계는 각 데이터를 중복없이 한 번만 저장
- 단점
  - 덜 유연함 (데이터 스키마를 사전에 계획하고 알려야 함)
  - 관계를 맺고 있어 조인문이 많은 복잡한 쿼리
  - 대체로 수직적 확장만 가능함

:heavy_check_mark: NoSQL
- 장점
  - 스키마가 없어서 유연
  - 데이터는 애플리케이션이 필요로 하는 형식으로 저장됨 -> 데이터 읽어오는 속도 빨라짐
- 단점
  - 유연성으로 인한 데이터 구조 결정 미룸
  - 데이터 중복으르 계속 업데이트
  - 데이터가 여러 컬렉션에 중복되어 있기 때문에 수정시 모든 컬렉션에서 수행해야 함

_둘 중 뭐가 더 좋은가???_

**관계를 맺고 있는 데이터가 자주 변경될 경우 SQL이 더 좋다!
읽기는 자주 하지만 데이터 변경은 자주 없는 경우 NoSQL이 더 좋다!**



---

<br>

참고

- [SQL과 NOSQL의 차이](https://gyoogle.dev/blog/computer-science/data-base/SQL%20&%20NOSQL.html)
- [[데이터베이스] SQL(구조화 쿼리 언어) vs NoSQL(비구조화 쿼리 언어)](https://hanamon.kr/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-sql-vs-nosql/)
- [[데이터베이스] SQL과 NoSQL의 차이](https://overcome-the-limits.tistory.com/283)
- [[DB]SQL vs NoSQL(mySQL vs MongoDB) 비교, 차이점](https://mjmjmj98.tistory.com/43)