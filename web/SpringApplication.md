# :pushpin: SpringApplication

## :leaves: SpringApplication란?

_Class that can be used to bootstrap and launch a Spring application from a Java main method._

## :heavy_check_mark: 정의 및 선언 방법

- SpringApplication 클래스는 main() 메서드에서 spring 응용 프로그램을 쉽게 bootstrap 할 수 있는 방법을 제공함
- 보통의 경우 다음과 같이 SpringApplication.run 메서드로 spring 응용 프로그램을 실행함

        @SpringBootApplication
        public class MyApplication {

            public static void main(String[] args) {
                SpringApplication.run(MyApplication.class, args);
            }
        }

- 객체 선언 방식 ver

        public static void main(String[] args) {
            SpringApplication app = new SpringApplication(Application.class);
            app.run(args);
        }

- 커스터마이징을 할 경우는 다음과 같이 바꿀 수 있음

        @SpringBootApplication
        public class MyApplication {

            public static void main(String[] args) {
                SpringApplication application = new SpringApplication(MyApplication.class);
                // 배너를 끄는 커스터마이징
                application.setBannerMode(Banner.Mode.OFF);
                application.run(args);
            }
        }

## :heavy_check_mark: Application Event 설정

- spring boot 애플리케이션이 시작할 때나 시작 직후 등 시점에서 Evnet Listener를 통해 다양한 이벤트를 실행할 수 있음

        @Component
        public class JumpListener implements ApplicationListener<ApplicationStartingEvent> {

            @Override
            public void onApplicationEvent(ApplicationStartingEvent applicationStartingEvent) {
            System.out.println("==================================");
            System.out.println("Starting");
            System.out.println("==================================");

                }
        }

- 애플리케이션이 맨 처음 실행되면 JumpListener를 자동으로 실행함
- 하지만 이 경우에 실행이 안된다
- 그 이유는 **Event 발생 기점 때문!!!**

- Application Context가 만들어지기 이전에 발생하는 이벤트 (ex. ApplicationStartingEvent)이면 Listener가 동작을 안함

        public static void main(String[] args) {
            SpringApplication app = new SpringApplication(Application.class);
            // listener 등록
            app.addListeners(new JumpListener());
            app.run(args);
        }

- 그래서 따로 listener를 등록해주어야 함

## :heavy_check_mark: WebApplicationType 설정

       @SpringBootApplication
        public class Application {
            public static void main(String[] args) {
                SpringApplication app
                    = new SpringApplication(Application.class);
                app.setWebApplicationType(WebApplicationType.NONE);
                app.setWebApplicationType(WebApplicationType.SERVLET);
                app.setWebApplicationType(WebApplicationType.REACTIVE);

                app.run(args);
            }
        }

- WebApplication에는 세가지 타입이 있음
  1. SERVLET : Spring MVC가 있으면 기본적으로 SERVLET 타입
  2. REACTIVE : Spring WebFlux가 있다면 기본적으로 REACTIVE 타입
  3. NONE : 둘다 없으면 NONE으로 동작
- 적용 순서는 **SERVLET -> REACTIVE -> NONE**

---

<br>

참고

- [[Spring Boot] 스프링부트 활용 - 기능 소개, Spring Application](https://velog.io/@dsunni/Spring-Boot-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-%ED%99%9C%EC%9A%A9-%EA%B8%B0%EB%8A%A5-%EC%86%8C%EA%B0%9C-Spring-Application)
- [SpringApplication 관련 정리](https://jump-developer.tistory.com/69)
