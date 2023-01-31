## 📌 Redis 간단 요약 ❗

  - key, value 구조의 비정형 데이터를 저장하고 관리하기 위한 오픈 소스 기반의 비관계형 데이터베이스 관리 시스템(DBMS)
  - DB, 캐시, 메세지 브로커로 사용
  - 인메모리 데이터 구조를 가진 저장소
  - 보통 데이터베이스는 하드 디스크나 SSD에 저장하지만 Redis는 메모리(RAM)에 저장해서 디스크 스캐닝이 필요없어 매우 빠른 장점이 존재
  - 캐싱도 가능해 실시간 채팅에 적합하며 세션 공유를 위해 세션 클러스터링에도 활용

## 1️⃣ DB와 Redis를 함께 사용하는 이유 

### 1. 개요
- DB는 데이터를 물리 디스크에 직접 쓰기 때문에 서버에 문제가 발생해서 다운되더라도 데이터가 손실되지 않음.
- 그러나, 매번 디스크에 접근하기 때문에 사용자가 많아질 수록 부하가 많아져 느려질 수 있음.

### 2. 캐시 서버의 필요성
- 규모가 작은 서비스의 경우 WEB-WAS-DB 구조도 무리가 가지 않음
- 규모가 커질 수록 사용자가 늘어나 DB 과부하가 생길 수 있어 캐시 서버를 도입해야함.
- 이때, 캐시 서버로 사용할 수 있는 것이 Redis!

## 2️⃣ 캐시 서버의 패턴

### 1. Look aside cache

1. 클라이언트가 데이터 요청
2. 웹서버는 데이터가 존재하는지 cache 서버에 먼저 확인
3. cache 서버에 데이터가 있으면 DB에 데이터를 조회하지 않고 cache 서버에 있는 결과값을 클라이언트에게 바로 반환 (cache hit)
4. cache 서버에 데이터가 없으면 DB에 데이터를 조회해 cache 서버에 저장하고 결과값을 클라이언트에게 반환 (cache miss)

### 2. Write Back

1. 웹서버는 모든 데이터를 cache 서버에 저장
2. cache 서버에 특정 시간 동안 데이터가 저장됨
3. cache 서버에 있는 데이터를 DB에 저장
4. DB에 저장된 cache 서버의 데이터를 삭제

- insert 쿼리를 한 번씩 500번 날리는 것보다 500개를 모아서 한 번만 날리는 것이 더 효율적이라는 원리
- 데이터가 DB에 저장되기 전에 cache에 저장되기 때문에 이 공간에 머무르는 동안 서버 장애가 발생되어 다운되면 데이터가 손실될 수 있음

## 3️⃣ Redis의 특징

- key, value 구조이기 때문에 쿼리 사용 필요 없음
- 데이터를 디스크에 쓰는 구조가 아닌 메모리에서 데이터를 처리하기 때문에 속도가 빠름
- String, List, Sets, Sorted Sets, Hashes 자료 구조 지원
	- String : 가장 일반적인 key- value 구조
  - Sets: String 집합, 여러 개의 값을 하나의 value에 넣을 수 있음, 포스트 tag 같은 곳에 사용될 수 있음
  - Sorted Sets: 중복된 데이터를 담지 않는 Set 구조에 정렬 Sort를 적용한 구조, 랭킹 보드 서버 같은 구현에 사용
  - Lists: Array 형식의 데이터 구조, 처음과 끝에 데이터를 넣는 것이 빠름, 중간에 데이터를 삽입하거나 삭제하는 것음 어려움
- Single Threaded: 한 번에 하나의 명령만 처리, 중간에 긴 명령어가 들어오면 뒤에 명령어들은 모두 앞에 있는 명령어가 처리될 때까지 대기가 필요, get & set 명령어의 경우 초당 10만개 처리 가능

## 4️⃣ Redis 사용 예시

- 캐싱
- 채팅, 메시징 및 대기열
- 게임 순위표
- 세션 저장
- 미디어 스트리밍
- 지리 공간 데이터 저장
- 머신 러닝
- 실시간 분석

## 5️⃣ 메시징 구현 방법

### 1. Message Queuing 

  - 오직 한 수신자만 메시지 수신
  - 즉, 1:1 통신

![](https://velog.velcdn.com/images/baebae/post/5bb339ae-33e2-4d9c-9dd6-bdbd81d18877/image.png)

### 2. Pub / Sub

  - 클라이언트의 수를 늘려 동시에 여러 메시지 처리
  - 수신자 모두에게 메시지 전송
  - 모든 클라이언트에게 서버측에서 같은 메시지를 한 번에 전송

![](https://velog.velcdn.com/images/baebae/post/0e0c7b87-6c20-450f-942b-ad907acf5442/image.png)

## 6️⃣ Redis의 Pub & Sub

- Redis는 기본으로 Pub & Sub 기능 제공
- Spring으로 채팅 서비스를 개발하고자 할 때 가장 먼저 접함
- 메시지 지속성은 없음 = 전송 후 해당 메시지는 삭제되고 Redis 어디에도 저장되지 않음
- 실시간으로 데이터를 처리해야할 때는 매우 적합하나 메시지가 저장되지 않는다는 점은 반드시 인지하고 개발해야 함

## 7️⃣ Redis 사용 시 주의할 점

- 서버에 장애가 발생할 경우 운영 플랜이 반드시 필요
	- 인메모리 데이터 저장소이기 때문에 서버에 장애가 발생할 경우 데이터 유실이 생길 수 있기 때문
- 메모리 관리가 중요
- 싱글 스레드의 특성상 처리하는데 시간이 오래 걸리는 요청, 명령은 피해야 함.

---

##### 참고
[Redis 101](https://dabeen.medium.com/redis-101-6dd36bca2ac)
[Redis란? 레디스의 기본적인 개념 (인메모리 데이터 구조 저장소)](https://wildeveloperetrain.tistory.com/21)
[[Spring Boot] Spring Boot, JWT, OAuth2](https://ozofweird.tistory.com/entry/Spring-Boot-Spring-Boot-JWT-OAuth2)
[[Java / Spring] Redis - Pub/Sub](https://wonsjung.tistory.com/405)
[Redis](https://gyoogle.dev/blog/computer-science/data-base/Redis.html)
