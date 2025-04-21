<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/45ae35de-99d9-4d06-a48e-53e8eb96c1aa/image.png" /></p>
<p>본 게시글은 인프런의 모든 개발자를 위한 HTTP 웹 기본 지식 (김영한) 강의를 듣고 정리한 내용입니다.</p>
<p>HTTP 메서드
HTTP API 만들기
API URI를 만들 때 가장 중요한 것은 리소스 식별
회원과 관련된 API를 만들 때, 회원이라는 개념 자체가 리소스다.
따라서 회원이라는 리소스만 식별할 수 있도록 회원 리소스를 URI에 매핑하고, HTTP 메서드로 행위를 분리시켜야 한다. (아래 예시 참고)
BAD (❌)
회원 목록 조회 /read-member-list
회원 조회 /read-member-by-id
회원 등록 /create-member
회원 수정 /update-member
회원 삭제 /delete-member
GOOD (🟢)
GET 회원 목록 조회 /members
GET 회원 조회 /members/{id}
POST 회원 등록 /members/{id}
PATCH 회원 수정 /members/{id}
DELETE 회원 삭제 /members/{id}</p>
<p>HTTP 메서드 - GET, POST
HTTP 주요 메서드에는 다음과 같이 다섯가지가 있다: GET, POST, PUT, PATCH, DELETE
GET: 리소스 조회
POST: 요청 데이터 처리, 주로 등록에 사용
PUT: 리소스를 대체, 해당 리소스가 없으면 생성
PATCH: 리소스 부분 변경
DELETE: 리소스 삭제
그 외 자주 사용하는 메서드들은 아래와 같다:</p>
<p>HEAD: GET과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환
OPTIONS: 대상 리소스에 대한 통신 가능 옵션(메서드)을 설명(주로 CORS에서 사용)
CONNECT: 대상 리소스로 식별되는 서버에 대한 터널을 설정
TRACE: 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행</p>
<p>GET 메서드
GET 메서드는 리소스 조회 용도로 사용됨
서버에 전달하고 싶은 데이터는 query를 통해 전달 (query params, query string)
메세지 바디도 같이 전달할 수 있지만, 지원하지 않은곳이 많기 때문에 지양해야 함
GET 메서드 원리: GET 메세지 전달 → 서버 조회 → 서버 응답</p>
<table>
<thead>
<tr>
<th>GET 전달</th>
<th>서버 조회</th>
<th>서버 응답</th>
</tr>
</thead>
<tbody><tr>
<td><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/7b5092c9-9c25-4391-92b2-1a9fc5e5e2d2/image.png" /></td>
<td><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/5e1ffd70-6ace-4aeb-9fbe-738daa6307a5/image.png" /></td>
<td><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/a6872dc5-5005-4342-85f5-aa91e459ce2e/image.png" /></td>
</tr>
</tbody></table>
<p>POST 메서드
POST 메서드는 요청 데이터 처리 용도로 사용됨
메세지 바디를 통해 서버로 요청 데이터 전달하도록 함. 그러면 서버는 요청 데이터를 처리
ex) 신규 리소스 등록, 프로세스 처리 등
POST 메서드 원리: POST 메세지 전달 → 서버에서 신규 리소스 생성 → 응답</p>
<table>
<thead>
<tr>
<th>POST 메세지 전달</th>
<th>신규 리소스 생성</th>
<th>서버 응답</th>
</tr>
</thead>
<tbody><tr>
<td><img alt="POST 메세지 전달" src="https://velog.velcdn.com/images/tonyhan18/post/f4a05ea1-3575-4bb9-964f-252e21752081/image.png" /></td>
<td><img alt="신규 리소스 생성" src="https://velog.velcdn.com/images/tonyhan18/post/4771ce1f-0061-48e8-bd02-2de14f82bf8d/image.png" /></td>
<td><img alt="서버 응답" src="https://velog.velcdn.com/images/tonyhan18/post/68118c81-1ebf-4dc3-bc3f-39a54471295c/image.png" /></td>
</tr>
</tbody></table>
<p>그렇다면, POST 요청 데이터 처리란?
아래와 같은 예시를 들 수 있음:</p>
<p>HTML Form 회원 및 주문 데이터 처리
게시판, 뉴스에 메세지 게시
새 리소스 생성 (떼이터 생성)
기존 자원에 데이터 추가 (문서 내용 추가 등)
단순 생성, 수정 뿐만 아니라 '요청 데이터를 처리'한다는 개념임</p>
<p>HTTP 메서드 - PUT, PATCH, DELETE
PUT 메서드
리소스를 수정할 때 사용하며, 리소스를 대체하는 메서드
리소스가 있으면 대체, 없으면 생성 (덮어 씌움)
동일 리소스가 있는 경우 (PUT 요청 → 리소스 대체)
동일 리소스가 없는 경우 (PUT 요청 → 리소스 생성)
중요: 클라이언트가 리소스 식별 (POST와 다름)
클라이언트가 리소스 위치를 알고 URI 지정
PATCH 메서드
리소스를 부분 변경할 때 사용
PATCH 안되는 서버도 있음. 이 경우에는 POST 써도 됨
DELETE 메서드
리소스를 제거할 때 사용</p>
<p>HTTP 메서드의 속성
안전 (Safe Methods)
멱등 (Idempotent Methods)
캐시가능 (Cacheable Methods)</p>
<p><img alt="HTTP 속성" src="https://velog.velcdn.com/images/tonyhan18/post/5d1c1c36-c13e-45e5-90bd-daefe95b501e/image.png" /></p>
<p>안전 (Safe Methods)
호출해도 리소스를 변경하지 않는다.
ex) GET 요청 한다고 리소스 변경되지 않음
Q: 그래도 계속 호출해서, 로그 같은게 쌓여서 장애가 발생하면?
A: 안전은 해당 리소스만 고려한다. 그런 부분까지 고려하지 않는다.
멱등 (Idempotent Methods)
멱등: 여러번 호출하든 결과가 항상 같은 경우 f(f(x)) = f(x)
한 번 호출하든 두 번 호출하든 100번 호출하든 결과가 똑같다.
위에서 언급한 네 메서드 중에, POST만 멱등하지 않음!! (ex. 중복결제)
GET: 한 번 조회하든, 두 번 조회하든 같은 결과가 조회된다.
PUT: 결과를 대체한다. 따라서 같은 요청을 여러번 해도 최종 결과는 같다.
DELETE: 결과를 삭제한다. 같은 요청을 여러번 해도 삭제된 결과는 똑같다.
POST: 멱등이 아니다! 두 번 호출하면 같은 결제가 중복해서 발생할 수 있다.
필요성: 자동 복구 메커니즘
ex) 서버가 timeout 등으로 정상 응답 못할 때, 클라이언트가 다시 요청해도 되는가? 판단 근거
마찬가지로 외부 요인으로 리소스 변경되는 것 까지는 고려 x
캐시가능 (Cacheable Methods)
응답 결과 리소스를 캐시해서 사용해도 되는지?
GET, HEAD, POST, PATCH 캐시 가능
하지만 실제로는 GET, HEAD 정도만 캐시로 사용함. (POST, PATCH는 캐시 키 고려해야하는데 구현 쉽지 않음)</p>
<p>HTTP 상태코드
상태코드: 클라이언트가 보낸 요청의 처리 상태를 응답에서 알려주는 기능</p>
<p>크게 다섯가지로 분류됨:</p>
<p>1xx (Informational): 요청이 수신되어 처리중
2xx (Successful): 요청 정상 처리
3xx (Redirection): 요청을 완료하려면 추가 행동이 필요
4xx (Client Error): 클라이언트 오류, 잘못된 문법등으로 서버가 요청을 수행할 수 없음
5xx (Server Error): 서버 오류, 서버가 정상 요청을 처리하지 못함
참고로, 1xx는 거의 사용하지 않으므로 위에 개념만 알고 넘어가도 됨</p>
<p>만약 모르는 상태 코드가 나타나면, 클라이언트는 상위 상태코드로 해석해서 처리</p>
<p>ex) 299 ??? -&gt; 2xx (Successful)
ex) 451 ??? -&gt; 4xx (Client Error)
ex) 599 ??? -&gt; 5xx (Server Error)
2xx - 성공
클라이언트의 요청을 성공적으로 처리 했을 때 사용하는 메서드
200 OK
201 Created
202 Accepted
204 No Content
200 OK
<img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/1c93bff1-0af6-4eef-a0cd-eeb2c1b01d9c/image.png" /></p>
<p>201 Created
<img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/c00c721f-3a79-47b6-ba9c-9bf85c68131e/image.png" /></p>
<p>202 Accepted
요청이 접수되었으나 처리가 완료되지 않았음
배치 처리 같은 곳에서 사용
ex) 요청 접수 후 1시간 뒤에 배치 프로세스가 요청을 처리함
204 No Content
서버가 요청을 성공적으로 수행했지만, 응답 페이로드 본문에 보낼 데이터가 없음
ex) 웹 문서 편집기에서 save 버튼
save 버튼의 결과로 아무 내용이 없어도 된다.
save 버튼을 눌러도 같은 화면을 유지해야 한다.
결과 내용이 없어도 204 메시지(2xx)만으로 성공을 인식할 수 있음</p>
<p>3xx - 리다이렉션1
요청을 완료하기 위해 유저 에이전트의 추가 조치 필요
300 Multiple Choices
301 Moved Permanently
302 Found
303 See Other
304 Not Modified
307 Temporary Redirect
308 Permanent Redirect
리다이렉션이란?
<img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/81c21002-504a-4a97-8e28-780ff2e96635/image.png" /></p>
<p>웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동 (리다이렉트)</p>
<p>세 가지의 리다이렉션이 있음:</p>
<p>1) 영구 리다이렉션 - 특정 리소스의 URI가 영구적으로 이동</p>
<p>ex) /members -&gt; /users
ex) /event -&gt; /new-event
2) 일시 리다이렉션 - 일시적인 변경</p>
<p>주문 완료 후, 주문 내역 화면으로 이동
PRG: Post/Redirect/Get
3) 특수 리다이렉션</p>
<p>결과 대신 캐시를 사용</p>
<p>영구 리다이렉션 (301, 308)
리소스의 URI가 영구적으로 이동
원래의 URL를 사용X, 검색 엔진 등에서도 변경 인지</p>
<table>
<thead>
<tr>
<th>메서드</th>
<th>내용</th>
</tr>
</thead>
<tbody><tr>
<td>301 Moved Permanently</td>
<td>리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음</td>
</tr>
<tr>
<td>308 Permanent Redirect</td>
<td>리다이렉트시 요청 메서드와 본문 유지</td>
</tr>
</tbody></table>
<p>일시 리다이렉션 (302, 307, 303)
리소스의 URI가 일시적으로 변경
따라서 검색 엔진 등에서 URL을 변경하면 안됨</p>
<table>
<thead>
<tr>
<th>메서드</th>
<th>내용</th>
</tr>
</thead>
<tbody><tr>
<td>302 Found</td>
<td>리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음</td>
</tr>
<tr>
<td>307 Temporary Redirect</td>
<td>302와 기능은 같으나, 리다이렉트시 요청 메서드와 본문 유지</td>
</tr>
<tr>
<td>303 See Other</td>
<td>302와 기능은 같고, 리다이렉트시 요청 메서드가 GET으로 변경</td>
</tr>
</tbody></table>
<p>307, 303을 권장하지만 현실적으로 이미 많은 애플리케이션 라이브러리들이 302를 기본값으로 사용함. 따라서, 자동 리다이렉션시에 GET으로 변해도 되면 그냥 302를 사용해도 큰 문제 없음</p>
<p>PRG: Post/Redirect/Get
POST로 주문후에 웹 브라우저를 새로고침 하면, 다시 요청이 가서 중복 주문이 될 수 있음. 이러한 현상을 방지하지 위해 PRG를 활용할 수 있음</p>
<p>PRG를 사용하면 POST로 주문후에 새로 고침으로 인한 중복 주문 방지를 할 수 있음. POST로 주문후에 주문 결과 화면을 GET 메서드로 리다이렉트 하기 때문에, 새로고침해도 결과 화면을 GET으로 조회하게 됨. 결국 중복 주문 대신에 결과 화면만 GET으로 다시 요청</p>
<p>기타 리다이렉션 (300, 304)</p>
<table>
<thead>
<tr>
<th>메서드</th>
<th>내용</th>
</tr>
</thead>
<tbody><tr>
<td>300 Multiple Choices</td>
<td>- 요청에 대해서 하나 이상의 응답이 가능</td>
</tr>
<tr>
<td>- 거의 안씀</td>
<td></td>
</tr>
<tr>
<td>304 Not Modified</td>
<td>- 요청된 리소스를 재전송할 필요가 없음</td>
</tr>
<tr>
<td>- 캐시를 목적으로 사용 (캐시의 암묵적인 리다이렉트)</td>
<td></td>
</tr>
<tr>
<td>- 클라이언트에게 리소스가 수정되지 않았음을 알려줌 → 클라이언트는 로컬에 저장된 캐시를 재사용</td>
<td></td>
</tr>
<tr>
<td>- 304 응답은 응답에 메시지 바디를 포함하면 안됨 (로컬 캐시를 사용해야 함) 조건부 GET, HEAD 요청시 사용</td>
<td></td>
</tr>
</tbody></table>
<p>4xx - 클라이언트 오류
클라이언트 오류가 났을 때 사용하는 메서드
400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
오류의 원인이 클라이언트에 있음
클라이언트가 이미 잘못된 요청, 데이터를 보내고 있기 때문에, 똑같은 재시도가 실패함</p>
<table>
<thead>
<tr>
<th>메서드</th>
<th>내용</th>
</tr>
</thead>
<tbody><tr>
<td>400 Bad Request</td>
<td>- 클라이언트가 잘못된 요청을 해서 서버가 요청을 처리할 수 없음</td>
</tr>
<tr>
<td>- 요청 구문, 메시지 등등 오류</td>
<td></td>
</tr>
<tr>
<td>401 Unauthorized</td>
<td>- 클라이언트가 해당 리소스에 대한 인증이 필요함</td>
</tr>
<tr>
<td>- 인증(Authentication) 되지 않음</td>
<td></td>
</tr>
<tr>
<td>- 401 오류 발생시 응답에 WWW-Authenticate 헤더와 함께 인증 방법을 설명</td>
<td></td>
</tr>
<tr>
<td>403 Forbidden</td>
<td>- 서버가 요청을 이해했지만 승인을 거부함</td>
</tr>
<tr>
<td>- 주로 인증 자격 증명은 있지만, 접근 권한이 불충분한 경우</td>
<td></td>
</tr>
<tr>
<td>404 Not Found</td>
<td>- 요청 리소스를 찾을 수 없음</td>
</tr>
<tr>
<td>- 요청 리소스가 서버에 없거나, 클라이언트가 권한이 부족한 리소스에 접근할 때 해당 리소스를 숨기고 싶을 때</td>
<td></td>
</tr>
</tbody></table>
<p>5xx - 서버 오류
서버에서 오류가 났을 때 사용하는 메서드
500 Internal Server Error
503 Service Unavailable
서버에 문제가 있기 때문에 재시도 하면 성공할 수도 있음(복구가 되거나 등등)</p>
<table>
<thead>
<tr>
<th>메서드</th>
<th>내용</th>
</tr>
</thead>
<tbody><tr>
<td>500 Internal Server Error</td>
<td>- 서버 문제로 오류 발생, 애매하면 500 오류</td>
</tr>
<tr>
<td>- 서버 내부 문제로 오류 발생시</td>
<td></td>
</tr>
<tr>
<td>503 Service Unavailable</td>
<td>- 서비스 이용 불가</td>
</tr>
<tr>
<td>- 서버가 일시적인 과부하 또는 예정된 작업으로 잠시 요청을 처리할 수 없음</td>
<td></td>
</tr>
<tr>
<td>- Retry-After 헤더 필드로 얼마뒤에 복구되는지 보낼 수도 있음</td>
<td></td>
</tr>
</tbody></table>
<hr />
<p>참고
모든 개발자를 위한 HTTP 웹 기본 지식 - 김영한</p>