# Bean Scope
- Spring Bean
- Spring Bean Scope
  - Singleton
  - Prototype
  - request
  - session
  - application


<br>

## Spring Bean
- Spring에서 POJO(Plain, Old Java Object)를 Bean이라고 부른다. (POJO 기반 객체)
- Bean의 scope를 따로 지정하지 않는 경우, 기본적으로 Singleton으로 생성하여 관리한다.          


  ``` java
  <!-- A simple bean definition-->
  <bean id="..." class="...""></bean>

  <!-- A bean definition with scope, 위와 동일함-->
  <bean id="..." class="..." scope="singleton"></bean>

  <!-- A bean definition with scope-->
  <bean id="..." class="..." scope="prototype"></bean>
  ```
<br>



## Spring Bean Scope
>  Bean이 존재할 수 있는 범위, 즉 사용 범위를 뜻한다.

<br>

### Singleton
- Spring은 Spring Container에 Spring Bean을 등록할 때, 기본으로 Singleton으로 등록한다.
- 유일하게 하나만 등록해서 공유한다는 뜻으로, 같은 Spring Bean이면 모두 **같은 인스턴스**이다.
- Spring Containter에 한 번만 생성되며 Container가 사라질 때 Bean 제거된다.

<br>

### Prototype
- 하나의 Bean 정의에 대해 다수의 객체가 존재할 수 있다.
- Prototype Bean은 의존성 관계의 Bean에 주입될 때 새로운 객체가 생성되어 주입된다.
- 정상적인 방법으로 GC에 의해 Bean 제거된다.
  ```java
  <!-- A bean definition with scope in xml-->
  <bean id="..." class="..." scope="singleton"></bean>
  
  <!-- annotation in java -->
  @Scope("prototype")
  ```

<br>



### Web 관련 Scope
>  웹 환경에서만 동작한다.       
>  Spring MVC Web Application에서만 사용된다.

**request**
  - 하나의 Bean 정의에 대해 하나의 HTTP request의 생명주기 안에 단 하나의 객체만 존재한다.      

  
**session**
  - 하나의 Bean 정의에 대해 하나의 HTTP Session의 생명주기 안에 단 하나의 객체만 존재한다.           


**application**
  - 하나의 Bean 정의에 대해 하나의 Global HTTP Session의 생명주기 안에 단 하나의 객체만 존재한다. 


<hr>


### 참고자료

- [[Spring] Spring Bean의 개념과 Bean Scope 종류](https://gmlwjd9405.github.io/2018/11/10/spring-beans.html)
- [[Spring] 빈 스코프(Bean Scope)란? Dependency Lookup(DL)이란?](https://code-lab1.tistory.com/186)
