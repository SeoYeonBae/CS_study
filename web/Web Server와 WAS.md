# Web Server와 WAS

## Web Server

![image](https://user-images.githubusercontent.com/63505110/235935502-ec3537ea-5f2e-4dc8-b305-cb59ca0a125c.png)
- HTTP 프로토콜로 서로 정보를 주고 받으며 정적 데이터를 제공한다.
- 정적인 컨텐츠만 처리하도록 기능 분배를 하여 서버 부담을 줄인다.

## WAS
![image](https://user-images.githubusercontent.com/63505110/235935572-c6651c6f-4ddf-4e81-bcf7-5fbe5e5fb8c6.png)

- DB 조회 및 다양한 로직 처리 요구시 *동적인 컨텐츠*를 제공하기 위해 만들어진 애플리케이션 서버
- 웹 컨테이너 혹은 서블릿 컨테이너라고 불림
  - 컨테이너란 JSP, Servlet을 실행시킬 수 있는 소프트웨어

- 

## Web Server와 WAS 차이

- Web Server는 정적 리소스(파일) 제공, WAS는 애플리케이션 로직 담당
  - 하지만, Web Server도 프로그램을 실행하는 기능을 포함하기도 하며
  - WAS도 Web Server의 기능을 제공함
  - 둘의 용어 경계 모호 ...

- Java는 서블릿 컨테이너 기능을 제공하면 WAS
  - 서블릿 없이 자바 코드를 실행하는 서버 프레임워크도 존재

- WAS는 애플리케이션 코드 실행하는데 더 특화

## Web Server와 WAS를 같이 사용하는 경우

![image](https://user-images.githubusercontent.com/63505110/235939554-6bbd08f3-91fa-4a1e-a0bb-88e34dfcfe54.png)   

> Web Server를 앞 단에 두고, WAS에 오류 발생할 경우 사용자가 이용하지 못하도록 막아둔 뒤 재시작할 수 있음

### 웹 서비스 흐름

- Client의 요청을 Web Server가 먼저 받은 뒤, WAS에게 보내 관련 Servlet을 메모리에 올림
- WAS는 web.xml을 참조해 해당 Servlet에 대한 스레드를 생성 (스레드 풀 이용)
  - 이때 HttpServletRequest와 HttpServletResponse 객체를 생성해 Servlet에게 전달 
- 스레드는 Servlet의 service() 메소드를 호출
- 요청에 맞게 doGet()이나 doPost() 메소드를 호출하여 적절한 동적 페이지를 Response 객체에 담아 WAS에 전달
- WAS는 Response 객체를 HttpResponse 형태로 바꿔 Web Server로 전달
- 생성된 스레드 종료하고, HttpServletRequest와 HttpServletResponse 객체 제거

#### 참고
https://gyoogle.dev/blog/web-knowledge/Web%20Server%EC%99%80%20WAS%EC%9D%98%20%EC%B0%A8%EC%9D%B4.html
