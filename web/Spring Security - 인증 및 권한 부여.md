## Spring Security - 인증 및 권한 부여

> Spring 기반의 애플리케이션의 보안(인증, 권한, 인가 등)을 담당하는 Spring 하위 프레임워크                 
> Spring Security를 사용하면 개발자는 모든 것을 처음부터 구축하지 않아도 웹 애플리케이션에서 보안 조치를 쉽게 구현할 수 있다.
                
 <br>      
 
### 보안 용어
- 인증 *(Authentication)*
  - 해당 사용자가 본인이 맞는지 확인하는 절차
  - 회원가입 및 로그인
- 인가 *(Authorization)* 
  - 인증된 사용자가 요청한 자원에 접근 가능한지 결정하는 절차             
      
![image](https://github.com/SeoYeonBae/CS_study/assets/63505110/29da95ce-fcdd-41cd-a313-723c51213c37)

*Spring Security는 이러한 인증과 인가를 위해 Principal을 아이디로, Credential을 비밀번호로 사용하는 **Credential 기반의 인증 방식**을 사용한다.*
- Principal(접근 주체)
  - 보호받는 리소스에 접근하는 대상
- Credential(비밀번호)
  - 리소스에 접근하는 대상의 비밀번호 

- 권한
  - 인가 과정에서 해당 리소스에 대한 제한된 최소한의 권한을 확인 


### 특징
- Filter 기반으로 동작하기에 Spring MVC와 분리되어 관리 및 동작한다.
  - Spring을 사용하지 않더라도 서블릿을 사용하고 있다면 따로 적용 가능하다. (서블릿 필터 기반 동작) 
- 세션-쿠키 방식으로 인증한다.
- Spring의 DispatcherServlet 앞단에 Filter 형태로 위치한다.
- DispatcherServlet으로 넘어가기 전에 Filter가 요청을 가로채서 클라이언트의 리소스 접근 권한을 확인하고, 없는 경우 인증 요청 화면으로 자동 리다이렉트한다.

### 아키텍처
![image](https://github.com/SeoYeonBae/CS_study/assets/63505110/fe61894b-1849-4529-b411-9c3ce5f6d1a1)
     
1. 사용자가 로그인을 시도한다.
2. `AuthenticationFilter` 가 요청을 가로챈다. 사용자가 입력한 정보를 바탕으로 `UsernamePasswordAuthenticationToken` 객체(미검증 상태)를 생성한다.
3. `AuthenticationManager`의 구현체인 ProviderManager에게 `UsernamePasswordAuthenticationToken`를 전달한다.
4. `AuthenticationProvider`에게 `UsernamePasswordAuthenticationToken`를 전달한다.
5. 실제 DB로부터 사용자 정보를 가져오는 `UserDetailService`에게 사용자 정보를 넘겨준다.
6. DB에 존재하는 사용자라면 `UserDetails`로 받아온다.
7. `AuthenticationProvider`는 사용자 정보와 `UserDetails`를 비교한다.
8. 인증이 완료되면 사용자 정보를 담은 `Authentication`을 반환한다.
9. 최초의 `AuthenticationFilter`에 `Authentication`이 반환된다.
10. Spring Security의 in-memory 세션 저장소인 `SecurityContextHolder`에 `Authentication`을 저장한다.

-> 실질적인 인증 과정은 사용자가 입력한 데이터와 `UserDetailService`의 메서드가 반환하는 `UserDetails`객체를 비교함으로써 동작한다.

### 참고
- [Spring Security](https://velog.io/@jummi10/Spring-Security-0k15d6af)
- [[SpringBoot] Spring Security란?](https://mangkyu.tistory.com/76)
- [Spring Security #1 기본동작](https://jiwondev.tistory.com/244)


