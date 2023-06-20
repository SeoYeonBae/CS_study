# :pushpin: 더티 체킹 (Dirty Checking)

## :computer: 더티 체킹이란?

_JPA에서 영속성 컨테이너가 관리하는 엔티티의 상태를 감지해서 변경된 부분이 있다면 자동으로 트랜잭션이 끝나는 시점에 데이터베이스를 변경하는 기능_

## :white_check_mark: 더티 체킹 조건

1. 영속성 컨텍스트에서 관리되는 데이터

   - 영속성 컨텍스트는 **엔티티를 처음 조회할 때** 시작되며, 이후 변경을 감지
   - 준영속/비영속 상태의 엔티티는 더티 체킹의 대상이 되지 못함

   ![image](https://github.com/SeoYeonBae/CS_study/assets/69101568/4a875111-f9fc-4d4a-bc99-4398d53b0235)

   - 준영속(detached) : 영속성 컨텍스트에 저장되었다가 분리된 상태
   - 비영속(new/transient) : 영속성 컨텍스트와 전혀 관계가 없는 상태

2. Transaction이 커밋되었을 때
   - 트랜잭션이 커밋되기 전까지 영속성 컨텍스트는 변경사항을 추적하기만 하고, db에 반영하지는 않음
   - 그래서 **@Transactional** 어노테이션 등으로 하나의 트랜잭션으로 묶어주고 변경해야 적용됨

---

## :white_check_mark: 더티 체킹 코드예시

    @Slf4j
    @RequiredArgsConstructor
    @Service
    public class PayService {

        public void updateNative(Long id, String tradeNo) {
            EntityManager em = entityManagerFactory.createEntityManager();
            EntityTransaction tx = em.getTransaction();
            tx.begin(); //트랜잭션 시작
            Pay pay = em.find(Pay.class, id);
            pay.changeTradeNo(tradeNo); // 엔티티만 변경
            tx.commit(); //트랜잭션 커밋
        }
    }

- 코드 흐름 : 트랜잭션 시작 -> 엔티티 조회 -> **엔티티의 값 변경** -> 트랜잭션 커밋
- 코드를 보면 별도로 데이터베이스에 save 하지 않음
- 그럼에도 쿼리가 실행되는 걸 보면 update 쿼리가 실행됨!
- 더티체킹이 이루어졌기 때문에 엔티티를 조회한 시점에 스냅샷을 찍고 트랜잭션이 끝나는 지점에 변경 사항이 있으면 알아서 update 쿼리가 실행됨

---

## :white_check_mark: @DynamicUpdate

_더티 체킹은 기본적으로 모든 필드를 업데이트_

만약에 변경된 필드만 업데이트 하고 싶으면 entity 최상단에 **@DynamicUpdate**를 선언

    @Getter
    @NoArgsConstructor
    @Entity
    @DynamicUpdate // 변경한 필드만 대응
    public class Pay {

        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        private Long id;

        private String tradeNo;
        private long amount;

---

<br>

참고

- [더티 체킹 (Dirty Checking)이란?](https://jojoldu.tistory.com/415)
- [[JPA] 더티 체킹(Dirty Checking)](https://velog.io/@_koiil/JPA-%EB%8D%94%ED%8B%B0-%EC%B2%B4%ED%82%B9-Dirty-Checking)
- [JPA 더티 체킹(Dirty Checking) 이란?](https://velog.io/@jiny/JPA-%EB%8D%94%ED%8B%B0-%EC%B2%B4%ED%82%B9Dirty-Checking-%EC%9D%B4%EB%9E%80)
- [[JPA] 더티 체킹(dirty checking) 정리](https://everydayyy.tistory.com/157)
- [JPA 영속성 컨텍스트란?](https://velog.io/@neptunes032/JPA-%EC%98%81%EC%86%8D%EC%84%B1-%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8%EB%9E%80)
