# JPA의 개념과 특징

# 📜 1. JPA란?

- Java Persistence API
- 개발자가 직접 SQL을 작성하지 않고 JPA API를 활용해 DB를 저장하고 관리할 수 있게 하는 것
- Spring에서 많이 활용되고 있지만 Spring이 제공하는 API가 아닌 ```Java가 제공하는 API임!!!```
- Java ORM 기술에 대한 표준 명세로 Java Application에서 관계형 DB를 사용하는 방식을 정의한 인터페이스

# 🛠️ 2. ORM이란?

- Object Relational Mapping
- Java 객체와 관계형 DB를 매핑함
- 즉, 객체가 DB 테이블이 되도록 만들어 주는 것
- Hibernate, EclipseLink, DataMucleus 등이 있음
- ORM을 사용하면 SQL을 사용하지 않아도 직관적인 메소드로 데이터를 조작할 수 있다는 장점이 있음 (= 개발자의 생산성 향상)

# 🌿 3. Spring Boot에서 JPA 사용
- ![image](https://github.com/SeoYeonBae/CS_study/assets/101535851/12bbaa68-3b7a-41dc-a0f2-f5d6f0ba5755)
- 스프링 부트에서는 spring-boot-starter-data-jpa로 패키지를 가져와 사용하며, 이는 Hibernate 프레임워크를 활용
- JPA는 애플리케이션과 JDBC 사이에서 동작하며, 개발자가 JPA를 활용했을 때 JDBC API를 통해 SQL을 호출하여 데이터베이스와 호출하는 전개가 이루어짐
- 즉, 개발자는 JPA의 활용법만 익히면 DB 쿼리 구현없이 데이터베이스를 관리할 수 있음

# 📌 4. JPA의 특징

## 1. 객체 중심 개발 가능

- SQL 중심 개발이 이루어진다면, CRUD 작업이 반복해서 이루어져야 함
- 하나의 테이블을 생성해야할 때 이에 해당하는 CRUD를 전부 만들어야 함
- 추후에 컬럼이 생성되면 관련 SQL을 모두 수정해야 함
- 또한, 개발 과정에서 실수할 가능성도 높아진다.

## 2. 생상성 증가

- SQL 쿼리를 직접 생성하지 않고, 만들어진 객체에 JPA 메소드를 활용해 데이터베이스를 다루기 때문에 개발자에게 편리성을 제공

## 3. 유지보수 용이

- 쿼리 수정이 필요할 때, 이를 담아야 할 DTO 필드도 모두 변경해야 하는 작업이 필요하지만 JPA에서는 엔티티 클래스 정보만 변경하면 되므로 유지보수에 용이함

## 4. 성능 증가

- 사람이 직접 SQL을 짜는 것과 비교해서 JPA는 동일한 쿼리에 대한 캐시 기능을 지원해주기 때문에 비교적 높은 성능 효율을 경험할 수 있

# ⚠️ 5. 제약 사항

- JPA는 복잡한 쿼리보다는 실시간 쿼리에 최적화
- 예를 들어 통계 처리와 같은 복잡한 작업이 필요한 경우에는 기존의 Mybatis와 같은 Mapper 방식이 더 효율적일 수 있음
- Spring에서는 JPA와 Mybatis를 같이 사용할 수 있기 때문에, 상황에 맞는 방식을 택하여 개발하면 됨

---

##### 참고

- [JPA](https://gyoogle.dev/blog/web-knowledge/spring-knowledge/JPA.html)
- [JPA(Java Persistence API)의 개념](https://velog.io/@modsiw/JPAJava-Persistence-API%EC%9D%98-%EA%B0%9C%EB%85%90)
- [JPA(Java Persistence Api)의 장점과 단점 및 사용해야 하는 이유.](https://wedul.site/506)
