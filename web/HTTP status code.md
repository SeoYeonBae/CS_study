# 🌎 HTTP status code


HTTP 요청에 대한 상태를 알려주는 코드

![image](https://user-images.githubusercontent.com/63834758/234469847-1044f452-b75d-4aa0-9cd9-4661f05e1a5d.png)

- 1XX : 요청이 수신되어 처리 중
- 2XX : 요청 정상 처리
- 3XX : 요청을 완료하려면 추가 행동 필요
- 4XX : 클라이언트 오류, 잘못된 문법 등으로 서버가 요청을 수행할 수 없음
- 5XX : 서버 오류, 서버가 정상 요청을 처리하지 못함



## (1) 100번대(informational) 
요청이 수신되어 처리중이라는 의미.  
다만 협업에서도 잘 사용되지 않는 코드이기 때문에 깊게 다루어지지는 않는다

|상태코드(상태메세지)|설명|
|-----|--|
|**100(Continue)**|처리가 되었으니 다음으로 진행|
|**101(Switching Protocols)**|서버가 프로토콜을 전환 중|
|**102(Processing)**|서버가 요청을 아직 처리 중이라 제대로 된 응답을 알려줄 수 없음|
|**103(Early Hints)**|웹에 필요한 리소스에 대한 힌트를 제공하여 리소스를 사전 로드 -> 빠른 로딩|

<br>
 

## (2) 200번대(Success)
요청이 정상 처리되었다는 의미.

|상태코드(상태메세지)|설명|비고|
|-----|---|--|
|**200(OK)**| 요청 성공 ||
|**201(Created)**| 요청이 성공했으며 그 결과로 새로운 리소스가 생성된 경우| 주로 POST나 PUT 이후에 나타난다 |
|**202(Accepted)**| 요청이 접수되었으나 처리가 완료되지 않은 경우 | 1시간 뒤에 처리하는 배치 프로세스 등에 나타난다 |
|**204(No Content)**| 요청을 수행했으나 본문에 보낼 데이터가 없는 경우| 게시글 임시저장 버튼 등에 나타난다 |

<br>
 

## (3) 300번대 (Redirection)

- 요청을 완료하려면 추가 행동이 필요한 경우를 의미.
- 결과에 Location header가 있다면 자동으로 Location 위치로 이동한다.
    - 총 3가지 리다이렉션이 있다.
 
1️⃣ **영속적인 리다이렉션(301, 308)**
- _특정 리소스의 URI가 영구적으로 이동한다._
- 해당 URI로 접근하면 다른 URI로 보내준다. 검색엔진은 이에 따른 URL을 갱신한다.

2️⃣ **일시적인 리다이렉션(302, 303, 307)**
- _리소스의 URI가 일시적으로 변경되며 검색엔진은 이에 따른 URL을 갱신하지 않는다._
- POST로 주문 후에 웹 브라우저로 새로고침을 하면 중복 주문이 될 수 있으니 이를 방지 차원해서 주로 사용한다.  
    - 예시 : 결제 👉 결제 완료 화면을 GET 리다이렉트 👉 새로고침시 GET 으로 리다이렉트 된 결제 완료 화면 조회

3️⃣ **특수 리다이렉션(300, 304)**
- _결과 대신 캐시를 사용한다._ (캐시된 복사본으로 페이지를 redirect)




![image](https://user-images.githubusercontent.com/63834758/234468886-af032ea5-564c-4997-932e-fa3657a2842c.png)
  
  
  
|상태코드(상태메세지)|설명|
|-----|---|
|**300(Multiple Choice)**|요청에 대해 하나 이상의 응답이 가능(거의 사용되지 않는다)|
|**301(Moved Permanetly)**| ▪ 영구 리다이렉션 <br>▪ 원래 URI를 사용하지 않을 때 사용<br> ▪ redirect 요청 시 요청 메서드들이 GET로 변하고 본문이 제거될 수 있다.|
|**302(Found)**| ▪ 임시 리다이렉션 <br> ▪ 검색엔진은 이에 따른 URL을 갱신 X <br> ▪ redirect 요청 시 요청 메서드가 GET으로 변하고 본문이 제거될 수 있다.|
|**303(Seee Other)**| ▪ 임시 리다이렉션<br> ▪ 검색엔진은 이에따른 URL을 갱신 X<br> ▪ redirect 요청 시 요청 메서드가 GET으로 변경된다.|
|**304(Not Modified)**| ▪ 캐시를 목적으로 사용<br> ▪ 클라이언트에게 리소스가 수정되지 않았음을 알려주며, 클라이언트는 로컬의 저장 캐시를 사용(캐시 리다이렉트)<br> ▪ Response 에 Body를 포함하면 안된다.||
|**307(Temporary Redirect)**| ▪ 임시 리다이렉션<br> ▪ 검색엔진은 이에 따른 URL을 갱신 X<br> ▪ redirect 시 요청 메서드들이 변화하지 않으며 본문 또한 유지된다. |
|**308(Permanent Redirect)**| ▪ 영구 리다이렉션<br> ▪ 원래 URI를 사용하지 않을 때 사용<br> ▪ redirect 시 요청 메서드들이 변화하지 않으며 본문 또한 유지된다. |



<br>
 


## (4) 400번대 (Client Error)

클라이언트 오류를 의미.
한번 오류가 발생하면 새로고침을 해도 똑같은 실수가 발생한다.



|상태코드(상태메세지)|설명|비고|
|-----|---|---|
|**400(Bad Request)**|클라이언트가 잘못된 요청을 하였으며 이에 따라 서버가 요청을 처리할 수 없음||
|**401(Unauthorized)**|인증이 되지 않음. <br>해당 오류 발생 시 응답에 WWW-Authenticate 헤더와 함께 전송.|로그인, 권한에 따라 해당 오류를 나타낸다.|
|**403(Forbidden)**|서버가 요청을 이해했지만 승인을 거부한다.|로그인은 했으나 관리자 권한에 접근한 경우|
|**404(Not Found)**|요청 리소스가 서버에 없거나 권한이 부족한 리소스에 접근할 때 사용||
 
<br>
 
 
## (5) 500번대 (Server Error)
서버 오류를 의미

|상태코드(상태메세지)|설명|
|-----|---|
|**500(Internal Server Error)**|서버 내부 문제로 오류 발생|
|**503(Service Unavailable)**|서버가 일시적인 과부하 또는 예정된 작업으로 잠시 요청을 처리할 수 없음.<br>Retry-After 필드를 사용해서 예상 복구시간을 포함해서 보낼 수 있다.|


 
 
 
 <hr>
 
 
 ### 출처
 
 - [HTTP 기본 지식 - HTTP Status Code](https://loy124.tistory.com/371)
 - [HTTP 상태 코드(1XX ~ 5XX) 종류 총정리](https://inpa.tistory.com/entry/HTTP-%F0%9F%8C%90-%EC%83%81%ED%83%9C-%EC%BD%94%EB%93%9C-1XX-5XX-%EC%B4%9D%EC%A0%95%EB%A6%AC%ED%8C%90-%F0%9F%93%96)
