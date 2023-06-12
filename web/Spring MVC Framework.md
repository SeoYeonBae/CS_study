# Spring MVC Framework

> 스프링 MVC 프레임워크가 동작하는 원리는 무조건 이해해야 함!

# 📌 1. Spring MVC 구조

![image](https://github.com/SeoYeonBae/CS_study/assets/101535851/086e66a4-c5a4-4170-b3cf-74906973c55e)

## 1. Dispatcher Servlet

- 제일 앞단에서 HTTP Request를 처리하는 Controller
- HTTP Request가 왔을 때 Dispatcher Servlet이 Request를 처리할 Controller를 정함
- 즉, Request를 처리할 Controller를 지정하는 Super Controller
- 참고, 이렇게 앞쪽에서 처리하는 Controller를 따로 두는 패턴을 Front Controller 패턴이라고 함

## 2. Handler Mapping

- 클라이언트의 request url을 어떤 컨트롤러가 처리해야 할 지 찾아서 DispatcherServlet에게 전달하는 역할
- 컨트롤러 상에서 url을 매핑시키기 위해 @RequestMapping을 사용하는데 핸들러가 이를 찾아주는 역할을 함

## 3. Controller (Handler)

- HTTP Request를 처리해 Model을 만들고 View를 지정
- HTTP Request의 메세지를 처리해 필요한 데이터를 뽑아 Model에 저장
- 또한, HTTP Request에 따라서 보여줄 View Name을 지정함
- View Name 뿐만 아니라 View를 반환할 수도 있지만 View에 Model의 데이터를 세팅하지는 않음

## 4. ModelAndView

- Controller에 의해 반환된 Model과 View가 Wrapping된 객체
- Model: Map<String, Value> 형태의 데이터 저장소
- View, View Name: View Resolver에서 그릴 View를 지정

## 5. View Resolver

- ModelAndView를 처리하여 View 그리기
- 즉, 모델에 저장된 데이터를 사용해 View를 그리는 것
- 여기서 View란 사용자에게 보여줄 완성된 View이고 그대로 유저에게 반환됨
- 우리가 특정 url로 들어갔을 때 우리가 보는 View가 바로 이곳에서 만들어지는 것

# 📌 2. Spring MVC 의의

- HTTP Request를 처리하는 Controller, 데이터를 처리해 정제된 데이터를 넣는 Model, 정제된 데이터를 활용해 사용자에게 보여지는 View에 대한 역할 분리가 되어 있음
- 따라서, Spring MVC를 사용하면 Controller, Model, View 모두를 규격화해놓아 유연하고 확장성 있게 웹 어플리케이션을 설계할 수 있음

> Spring MVC는 웹 어플리케이션을 유연하고 확장 가능하게 만들어 줌!

# 🌟 3. Spring MVC 진행 과정 🌟
![image](https://github.com/SeoYeonBae/CS_study/assets/101535851/086e66a4-c5a4-4170-b3cf-74906973c55e)

> 클라이언트가 서버에게 url을 통해 요청할 때 일어나는 스프링 프레임워크의 동작

1. 클라이언트가 url을 요청하면, 웹 브라우저에서 스프링으로 request가 보내진다.
2. Dispatcher Servlet이 request를 받으면, Handler Mapping을 통해 해당 url을 담당하는 Controller를 탐색 후 찾아낸다.
3. 찾아낸 Controller로 request를 보내주고, 보내주기 위해 필요한 Model을 구성한다.
4. Model에서는 페이지 처리에 필요한 정보들을 Database에 접근하여 쿼리문을 통해 가져온다.
5. 데이터를 통해 얻은 Model 정보를 Controller에게 response 해주면, Controller는 이를 받아 Model을 완성시켜 Dispatcher Servlet에게 전달해준다.
6. Dispatcher Servlet은 View Resolver를 통해 request에 해당하는 view 파일을 탐색 후 받아낸다.
7. 받아낸 View 페이지 파일에 Model을 보낸 후 클라이언트에게 보낼 페이지를 완성시켜 받아낸다.
8. 완성된 View 파일을 클라이언트에 response하여 화면에 출력한다.

---

##### 출처

- [Spring MVC Framework란 무엇인가? Spring MVC의 구조와 의](https://kotlinworld.com/326)
- [Spring MVC Framework](https://gyoogle.dev/blog/web-knowledge/spring-knowledge/Spring%20MVC.html)
- [Spring MVC Architecture](https://www.egovframe.go.kr/wiki/doku.php?id=egovframework:rte:ptl:spring_mvc_architecture)
