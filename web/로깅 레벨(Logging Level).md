# 📊 0. 로깅 레벨을 신경써야 하는 이유

> 로그를 무분별하게 사용하면 정작 확인해야 하는 로그를 확인하지 못하는 문제가 발생
따라서, log4j 라는 표준에 맞게 정리된 로깅 레벨을 사용!

# 📊 1. 로깅 레벨

- log4j의 최근 버전에 의하면 높은 등급에서 낮은 등급으로의 6개의 로그 레벨을 가지고 있다.
- 로그레벨 순서
  
  - TRACE > DEBUG > INFO > WARN > ERROR > FATAL

|레벨|설명|
|-|-|
|TRACE|DEBUG보다 더 세분화 된 정보를 지정|
|**DEBUG**|프로그램 디버깅하기 위한 정보를 지정|
|**INFO**|상태변경과 같은 정보성 메세지 지정|
|**WARN**|처리 가능한 문제, 향후 시스템 에러의 원인이 될 수 있는 경고성 메세지 지정|
|**ERROR**|요청을 처리 도중 문제가 발생한 경우|
|FATAL|프로그램을 중단 할 수 있는 심각한 오류, 작동이 불가능할 경우|

> 프로젝트 진행 시 대체로 개발가이드에는 **DEBUG, INFO, WARN, ERROR** 4가지를 구분하여 출력하도록 되어 있다.

# 📊 2. 로깅 레벨 설정

WARN을 로그 레벨로 지정을 하게 되면 그 아래 WARN, ERROR, FATAL까지 로그가 찍히게 된다.

```
import org.apache.log4j.*;

public class LogClass {
   private static org.apache.log4j.Logger log = Logger.getLogger(LogClass.class);
   
   public static void main(String[] args) {
      log.setLevel(Level.WARN);

      log.trace("Trace Message!");
      log.debug("Debug Message!");
      log.info("Info Message!");
      log.warn("Warn Message!");
      log.error("Error Message!");
      log.fatal("Fatal Message!");
   }
}
```

실행 결과

```
Warn Message!
Error Message!
Fatal Message!
```

# 📌 3. DEBUG

로컬 및 개발서버 환경 출력하며, 개발 및 디버깅 시 출력한다.

```
String param1 = "param1";
String param2 = "param2";
 
log.debug("value1 : {}, value2 : {}", param1, parma2);	// {} 순서대로 매핑됨
```

실행 결과

```
value1 : param1, value2 : param2
```

# 📌 4. INFO

운영서버 환경에서 출력하며, 프로세스 정상 동작 여부 출력한다.(개인정보 출력 금지)

# 📌 5. WARN

정상 프로세스가 아닌 경우 출력한다.
강제로 Exception 발생 시 주로 사용한다.

```
HashMap<String, Object> session = (HashMap<String, Object>)session.getAttribute("name");
 
if(session == null){
    log.warn("Not Exist Session: name");
    throw new Exception();
}

```

# 📌 6. ERROR

에러 발생 시 출력한다.

```
try {
    int result = service.insertMember(vo);
}catch(Exception e) {
    log.error(e.getMessage(), e);
}
```

---

##### 참고
- [Logging Level](https://gyoogle.dev/blog/web-knowledge/Logging%20Level.html)
- [로그 레벨 별 로그 내용](https://jangiloh.tistory.com/18)
- [로깅 레벨(Logging Level)](https://velog.io/@whanhee97/%EB%A1%9C%EA%B9%85-%EB%A0%88%EB%B2%A8Logging-Level)
- [log4j - Logging Levels](https://www.tutorialspoint.com/log4j/log4j_logging_levels.htm)
- [[Java] Log4j Level 설정(로그 올바른 사용법)](https://string.tistory.com/7)
