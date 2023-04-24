# 📌 REST API

> REST를 기반으로 만들어진 API

## 1. REST란?

- REST(Representational State Transfer)의 약자로 자원을 이름으로 구분하여 해당 자원의 상태를 주고받는 모든 것을 의미
- HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(POST, GET, PUT, DELETE, PATCH 등)를 통해 해당 자원(URI)에 대한 CRUD Operation을 적용하는 것을 의미

## 2. REST 구성 요소

- 자원(Resource) : HTTP URI
- 자원에 대한 행위(Verb) : HTTP Method
- 자원에 대한 행위의 내용 (Representations) : HTTP Message Pay Load

## 3. REST의 특징

### 1. Uniform (유니폼 인터페이스)

- URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일

### 2. Stateless (무상태성)

- REST는 무상태성 성격을 지님
- 다시 말해 작업을 위한 상태정보를 따로 저장하고 관리하지 않음
- 세션 정보나 쿠키정보를 별도로 저장하고 관리하지 않기 때문에 API 서버는 들어오는 요청만을 단순히 처리하면 됨
- 때문에 서비스의 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않음으로써 구현이 단순해짐

### 3. Cacheable (캐시 가능)

- 가장 큰 특징 중 하나
- HTTP라는 기존 웹표준을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라를 그대로 활용 가능
- 따라서, HTTP가 가진 캐싱 기능 적용 가능
- HTTP 프로토콜 표준에서 사용하는 Last-Modified태그나 E-Tag를 이용하면 캐싱 구현이 가능

### 4. Self-descriptiveness (자체 표현 구조)

- REST의 또 다른 큰 특징 중 하나
- REST API 메시지만 보고도 이를 쉽게 이해 할 수 있는 자체 표현 구조로 되어 있다는 것

### 5. Client - Server 구조

- REST 서버는 API 제공, 클라이언트는 사용자 인증이나 컨텍스트(세션, 로그인 정보)등을 직접 관리하는 구조
- 각각의 역할이 확실히 구분되기 때문에 클라이언트와 서버에서 개발해야 할 내용이 명확해지고 서로간 의존성이 줄어듦

### 6. 계층형 구조

- REST 서버는 다중 계층으로 구성될 수 있음
- 보안, 로드 밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있고 PROXY, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할 수 있게 함

## 4. REST API 디자인 가이드

### 가장 중요한 점! 다른 건 다 잊어도 이건 기억해야 함!!

- 첫 번째, URI는 정보의 자원을 표현해야 한다.
- 두 번째, 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.

### 1. URI는 동사보다는 명사를, 대문자보다는 소문자를 사용하여야 한다.

```
Bad Example http://khj93.com/Running/
Good Example  http://khj93.com/run/  
```

### 2. 마지막에 슬래시 (/)를 포함하지 않는다.

```
Bad Example http://khj93.com/test/  
Good Example  http://khj93.com/test
```


### 3. 언더바 대신 하이폰을 사용한다.

```
Bad Example http://khj93.com/test_blog
Good Example  http://khj93.com/test-blog  
```


### 4. 파일확장자는 URI에 포함하지 않는다.

```
Bad Example http://khj93.com/photo.jpg  
Good Example  http://khj93.com/photo  
```

### 5. 행위를 포함하지 않는다.

```
Bad Example http://khj93.com/delete-post/1  
Good Example  http://khj93.com/post/1  
```

---

##### 참고

- [REST API 제대로 알고 사용하기](https://meetup.nhncloud.com/posts/92)
- [[네트워크] REST API란? REST, RESTful이란?](https://khj93.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-REST-API%EB%9E%80-REST-RESTful%EC%9D%B4%EB%9E%80)
