<p>본 게시글은 인프런의 모든 개발자를 위한 HTTP 웹 기본 지식 (김영한) 강의를 듣고 정리한 내용입니다.</p>
<p>HTTP 헤더 개요
HTTP 헤더 형식
HTTP 헤더 필드는 아래와 같은 형식으로 구성된다
header-field: field-name: “:” (Optional White Space; OWS) field-value (OWS)
field-name은 대소문자 구분을 하지 않는다.
ex) Host: <a href="http://www.google.com">www.google.com</a>
ex2) Content-Type: text/html;charset=UTF-8
ex3) Content-Length: 3423
HTTP 헤더 용도
HTTP 전송에 필요한 모든 부가정보
ex) 메세지 바디 내용, 메세지 바디 크기, 압축, 인증, 요청 클라이언트, 서버 정보, 캐시 관리 정보
표준 헤더 매우 많음. 필요 시, 임의 헤더 추가 가능</p>
<p>HTTP 헤더 (과거)
RFC2616 헤더 개요
과거(RFC2616)에는 네 가지로 헤더를 분류함
General 헤더: 메세지 전체에 적용되는 정보 (ex. Connection: close)
Request 헤더: 요청 정보 (ex. User-Agent: Mozilla/5.0)
Response 헤더: 응답 정보 (ex. Server: Apache)
Entity 헤더: 엔티티 바디 정보 (ex. Content-Type: text/html, Content-Length: 3234)
엔티티 헤더: 실제 메세지 바디에 들어가는 내용과 관련된 정보 (ex. 타입이 무엇인지 알려줌, 데이터 유형, 데이터 길이, 압축 정보 등등)
메시지 본문은 엔티티 본문을 전달하는데 사용
엔티티 본문: 요청이나 응답에서 전달할 실제 데이터
<img alt="엔티티 본문" src="https://velog.velcdn.com/images/tonyhan18/post/971dafc7-ce31-4834-b52a-d1af86aebf4b/image.png" /></p>
<p>그런데, 1999년에 만든 RFC2616가 폐지되고, 2014년에 RFC7230 ~ 7235가 등장하면서 많이 개정됨</p>
<p>HTTP 헤더 (최신)
RFC7230 ~ 7235 헤더 개요
엔티티 → 표현(Representation)으로 나타냄
Representation = representation Metadata + Representation Data
표현 = 표현 메타데이터 + 표현 데이터
표현 헤더는 표현 메타데이터 &amp; 페이로드 메세지 구분 생략함
ex) 회원 데이터를 JSON 형태로 전달할 수도 있고, html로 전달할 수 도 있음. 그래서 이런 데이터 및 형태 등 실제 전달하는 것을 '표현'으로 뜻함</p>
<p><img alt="표현" src="https://velog.velcdn.com/images/tonyhan18/post/10c1e2a9-de61-48e2-aaf9-b11b151d0a38/image.png" /></p>
<p>표현
아래는 표현과 관련된 헤더들임:
Content-Type: 표현 데이터 형식
Content-Encoding: 표현 데이터 압축 방식
Content-Language: 표현 데이터 자연 언어 (한/영)
Content-Length: 표현 데이터 길이
표현 헤더는 전송/응답에 둘다 사용가능</p>
<p>Content-Type
Content-Type: 표현 데이터의 형식 설명
미디어 타입, 문자 인코딩 등
ex) html은 Content-Type:text/html;charset=UTF-8
ex) JSON은 Content-Type: application/json
ex) image/png 등</p>
<p><img alt="이미지" src="https://velog.velcdn.com/images/tonyhan18/post/18a26fd0-cf2f-4269-929c-7e5412e4cf07/image.png" /></p>
<p>Content-Encoding
Content-Encoding: 표현 데이터 인코딩
표현 데이터를 압축하기 위해서 사용함
서버에서 압축 후 전달하면, 클라이언트가 뭘 압축한건지 알아야 함. 이 압축을 풀기 위해 인코딩 헤더를 보내줌
ex) gzip, deflate, identity(압축 x)</p>
<p><img alt="Content-Encoding" src="https://velog.velcdn.com/images/tonyhan18/post/7a0a5aee-677a-4ba9-8a8d-5105726c143c/image.png" /></p>
<p>Content-Language
Content-Language: 표현 데이터의 자연 언어
ex) ko, en, en-US
다국어처리 등 부가적인 처리를 할 수 있음</p>
<p><img alt="Content-Language" src="https://velog.velcdn.com/images/tonyhan18/post/79d86c4d-38bb-4ece-8787-e0d2eb4106da/image.png" /></p>
<p>Content-Length
Content-Length: 표현 데이터의 길이
ex) Content-Length: 5
바이트의 단위
Transfer-Encoding(전송 코딩) 사용하면 content-length 사용하면 안됨. transfer-encoding 안에 정보 다 있음 (뒤에서 다시 설명)</p>
<p>콘텐츠 협상
콘텐츠 협상: 쉽게 말하면, 클라이언트가 선호하는 표현으로 요청하는 것
물론 서버가 못줄수도 있음
협상 헤더는 요청시에만 사용
ex) Accept-Charset 보내면 클라이언트가 선호하는 문자 인코딩으로 데이터 전달해줘~ 라고 요청하는 것</p>
<p>아래는 콘텐츠 협상 헤더 예시:
Accept: 클라이언트가 선호하는 미디어 타입 전달
Accept-Charset: 클라이언트가 선호하는 문자 인코딩
Accept-Encoding: 클라이언트가 선호하는 압축 인코딩
Accept-Language: 클라이언트가 선호하는 자연 언어
Accept-Language</p>
<p>Accept-Language를 적용하지 않는다면?
ex) 한국에서 한국어 브라우저를 사용하는데, accept-language 사용하지 않으면 기본 값인 영어를 보내줌
Accept-Language를 적용한다면?
ex) accept-language를 요청하면 서버에서 인식하고 한국어로 기본 내용 보여줌</p>
<table>
<thead>
<tr>
<th>Accept-Language 적용 전</th>
<th>Accept-Language 적용 후</th>
</tr>
</thead>
<tbody><tr>
<td><img alt="Accept-Language 적용 전" src="https://velog.velcdn.com/images/tonyhan18/post/3a695357-5f4e-466a-aaa2-549aa24be586/image.png" /></td>
<td><img alt="Accept-Language 적용 후" src="https://velog.velcdn.com/images/tonyhan18/post/9876949c-3623-47c0-bf5e-c41b44aacf2d/image.png" /></td>
</tr>
</tbody></table>
<p>Accept-Language를 사용해도 문제가 생기는 경우에는?
ex) 한국어 브라우저 사용해서 한국어로 보냈는데, 기본이 독어(2순위 영어)라서 독어로 옴. 이때, 나는 차라리 영어를 받고 싶음. 어떻게 해야할지?
이를 위해서는 우선순위가 필요함 (아래내용 참고)
협상과 우선순위 (1)
협상에서 우선순위를 매기기 위해서는 Quality Values (q 값)을 사용해서 보내줌
0~1, 클수록 높은 우선순위이고, 생략하면 1값으로 들어감
ex) Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
위 예시에서 우선순위는 아래와 같음:</p>
<p>1) ko-KR;q=1 (q생략)
2) ko;q=0.9
3) en-US;q=0.8
4) en;q=0.7
위 예시처럼 원하는 언어 값에 우선순위 (1, 0.9, 0.8... 등)을 명시해서 보내줄 수 있음. 이렇게 설정하는 경우, 상위 우선순위 값인 한국어가 없으면, 그 다음 우선순위인 ‘영어’값을 보내줌</p>
<p><img alt="협상과 우선순위" src="https://velog.velcdn.com/images/tonyhan18/post/914eb592-a3f0-49c4-a6ff-ea5ba88f67f4/image.png" /></p>
<p>협상과 우선순위 (2)
그 외 우선순위는 ‘구체적’인 것이 우선함
ex) Accept: text/, text/plain, text/plain;format=flowed, /*
위 예시에서 우선순위는 아래와 같음:</p>
<p>1) text/plain;format=flowed
2) text/plain
3) text/*
4) /</p>
<p>협상과 우선순위 (3)
구체적인 것을 기준으로 미디어 타입을 맞춘다
ex) Accept: text/;q=0.3, text/html;q=0.7, text/html;level=1,  text/html;level=2;q=0.4, /*;q=0.5</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/ece7a524-e0e6-484b-bfcf-22a0f9382a76/image.png" /></p>
<p>전송방식
전송 방식은 아래와 같이 네 가지가 있음:
단순 전송
압축 전송
분할 전송
범위 전송</p>
<p>단순 전송
요청하면 다 전송해주는 방식
전송 콘텐츠에 대한 길이값을 단순히 요청하고 다 받음</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/a65d211b-f61b-4c28-a407-03e21ad1be4d/image.png" /></p>
<p>압축 전송
서버에서 콘텐츠를 gzip 등으로 압축해서 전송함
이때, 압축 형식도 같이 헤더에 넣어서 보내줌</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/fae6d751-bf8d-4516-af4b-2a28f6a9fe8a/image.png" /></p>
<p>분할 전송
chunk: 덩어리. 이 덩어리를 쪼개서 보낸다는 뜻</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/564fd6dd-63fb-42a9-ad77-1ce8fd4cd664/image.png" /></p>
<p>5 byte (hello)를 먼저 보냄 → 그후 5 byte (World) 보냄
클라이언트는 오는 순서대로 바로바로 화면에 보여줌
용량이 큰 경우 쪼개서 보낼 수 있음
분할 전송은 Content-Length를 넣으면 안됨. 왜냐하면 각각 쪼개진 길이를 모르기 때문
범위 전송
ex) 이미지를 받는데 절반만 오면, 다시 다 요청하는게 아니라 절반 이후로 부터 달라고 범위 전송을 요청할 수 있음</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/effefd44-b804-4b92-8673-d0c245e5dbcb/image.png" /></p>
<p>일반 정보
HTTP 헤더의 일반 정보에는 다음과 같은 속성들이 있음:
From: 유저 에이전트의 이메일 정보
Referer: 이전 웹 페이지 주소
User-Agent: 유저 에이전트 애플리케이션 정보
Server: 요청을 처리하는 오리진 서버의 소프트웨어 정보
Date: 메시지가 생성된 날짜</p>
<p>From
From: 유저 에이전트의 이메일 정보
일반적으로 잘 사용되지 않음
검색 엔진 같은 곳에서, 주로 사용
요청에서 사용</p>
<p>Referer
Referer: 이전 웹 페이지 주소
현재 요청된 페이지의 이전 웹 페이지 주소
A -&gt; B로 이동하는 경우 B를 요청할 때 Referer: A 를 포함해서 요청 Referer를 사용해서 유입 경로 분석 가능
ex) google -&gt; wiki의 레퍼러는 wiki. wiki -&gt; wiki korea 레퍼러는 wiki
장점: 유입 경로 분석 (데이터 분석)할 때 사용
요청에서 사용
참고: referer는 단어 referrer의 오타</p>
<p>User-Agent
User-Agent: 유저 에이전트 애플리케이션 정보
클라이언트의 애플리케이션 정보 (웹 브라우저 정보 등등)
ex) user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.183 Safari/537.36
통계 정보를 내거나, 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능
요청에서 사용
Server
Server: 요청을 처리하는 ORIGIN 서버의 소프트웨어 정보
프록시 서버가 아닌, 최종 데이터 가지고 있는 마지막 서버 (=오리진 서버)의 정보
ex) Server: Apache/2.2.22 (Debian)
ex) Server: nginx
응답에서 사용
Date
Date: 메시지가 발생한 날짜와 시간
ex) Date: Tue, 15 Nov 1994 08:12:31 GMT
응답에서 사용</p>
<p>특별한 HTTP 정보
특별한 HTTP 정보에는 아래와 같은 속성들이 있음:
Host: 요청한 호스트 정보(도메인)
Location: 페이지 리다이렉션
Allow: 허용 가능한 HTTP 메서드
Retry-After: 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간</p>
<p>Host
Host: 요청한 호스트 정보(도메인)
진짜 중요한 필수값
하나의 서버에 여러 도메인 적용되어 있을 때 처리해주는 것
ex) GET /search?q=hello&amp;hl=ko; HTTP/1.1 Host: <a href="http://www.google.com">www.google.com</a>
만약 host 정보가 없으면, 어떤 도메인인지 모름 (IP로만 통신하기 때문에)
따라서, host 헤더를 통해 실제 호스트를 알려줘야 함
이미지</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/35f53b3b-d7b4-4c3d-b799-7924e7c61188/image.png" /></p>
<p>예를 들어, 위 처럼 가상 서버가 있음. 해당 가상 서버에는 가상 호스트를 통해 여러 도메인을 한번에 처리하고 있음</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/43356b64-6279-4ac4-a10b-d6984f2d912a/image.png" /></p>
<p>약 host 정보가 없으면, 어떤 도메인인지 모름 (IP로만 통신하기 때문에)
초창기에 해당 이슈 때문에 문제가 많이돼서 필수 내용이 됨</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/14639230-94b4-47fd-9e55-711aa2a35640/image.png" /></p>
<p>이런식으로 실제 호스트를 명시해줘야 함
Location
Location: 페이지 리다이렉션 위치 알려주는 정보
웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동 (리다이렉트)
응답코드 3xx에서 설명
201 (Created): Location 값은 요청에 의해 생성된 리소스 URI
3xx (Redirection): Location 값은 요청을 자동으로 리디렉션하기 위한 대상 리소스를 가리킴
Allow
Allow: 허용 가능한 HTTP 메서드
405 (Method Not Allowed) 에서 응답에 포함해야함
Allow: GET, HEAD, PUT
Retry-After
Retry-After: 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간
503 (Service Unavailable): 서비스가 언제까지 불능인지 알려줄 수 있음
ex) Retry-After: Fri, 31 Dec 1999 23:59:59 GMT (날짜 표기)
ex) Retry-After: 120 (초단위 표기)
인증
HTTP 인증 정보는 아래와 같이 두 가지 속성이 있음:
Authorization: 클라이언트 인증 정보를 서버에 전달
WWW-Authenticate: 리소스 접근시 필요한 인증 방법 정의
Authorization
Authorization: 클라이언트 인증 정보를 서버에 전달하는 것
Authorization: Basic xxxxxxx 형태
인증 방식마다 들어가는 값은 모두 다름. 하지만, http authorization 헤더는 어떤 인증인지 상관없지 값을 제공하는 것
WWW-Authenticate
WWW-Authenticate: 리소스 접근시 필요한 인증 방법 정의
만약 접근했는데 인증에 문제가 있다면, 401 Unauthorized 응답을 남기고 함께 사용
ex) WWW-Authenticate: Newauth realm=&quot;apps&quot;, type=1,  title=&quot;Login to &quot;apps&quot;&quot;, Basic realm=&quot;simple&quot;
ex 해석) 위 정보들을 참고해서 인증을 제대로 해라~
쿠키
쿠키란? 웹 서버에서 생성하여, 브라우저에 전송 &amp; 저장되는 작은 텍스트 파일
쿠키를 사용할 때는 set-cookie, cookie 두 가지를 사용함
Set-Cookie: 서버가 클라이언트로 쿠키 전달 (응답)
Cookie: 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달
쿠키를 사용하지 않을 때
만약 쿠키를 사용하지 않는다면?</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/25b272c2-40c1-41a4-9774-b88cb9e2a977/image.png" /></p>
<p>로그인 되었으나, 홍길동 사용자의 정보가 저장되어있지 않음. 그 이유는 서버에서 로그인 사용자인지 아닌지 구분할 수 없기 때문.</p>
<p>왜냐? http는 stateless이기 때문에</p>
<p>Stateless
HTTP는 무상태 프로토콜임 (stateless)
클라이언트 ↔︎ 서버 요청 응답 주고 받으면 연결이 끊어짐
클라이언트가 다시 요청하면 서버는 이전 요청 기억하지 못함
따라서, 클라이언트와 서버는 서로 상태를 유지하지 않는다
대안 1
모든 요청에 사용자 정보 포함해서 넘김</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/63d477a3-90b2-4097-b91c-8122b09266b5/image.png" /></p>
<p>ex) GET /welcom?user=홍길동
문제점: 모든 요청과 링크에 사용자 정보를 포함해야함??
→ 보안에 취약함. 브라우저 완전히 종료하고 다시 열면 또 다시 문제.
이를 해결하기 위한 방법은 쿠키
대안 2 (해결법)
set-cookie 헤더에 홍길동 정보를 넣어서 브라우저에 보내는 방법으로 해결 가능 (key=value)
브라우저에서 해당 정보를 쿠키 저장소에 저장해둠</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/af253a5a-2ed8-4d73-b7a6-429009153551/image.png" /></p>
<p>이 다음부터는 서버에 요청 보낼 때 마다 쿠키값을 HTTP 값을 포함해서 보냄
쿠키는 모든 요청에 모든 쿠키 정보를 자동으로 포함해서 보냄</p>
<table>
<thead>
<tr>
<th>쿠키 적용 로그인 1</th>
<th>쿠키 적용 로그인 2</th>
</tr>
</thead>
<tbody><tr>
<td><img alt="Accept-Language 적용 전" src="https://velog.velcdn.com/images/tonyhan18/post/2057d879-2e3c-4576-ba79-2f67a457a2b0/image.png" /></td>
<td><img alt="Accept-Language 적용 후" src="https://velog.velcdn.com/images/tonyhan18/post/b2a7fee5-ae20-471e-baf5-9008d856f67e/image.png" /></td>
</tr>
</tbody></table>
<p>쿠키 개요
쿠키는 아래와 같이 사용함
예) set-cookie: sessionId=abcde1234; expires=Sat, 26-Dec-2020 00:00:00 GMT; path=/; domain=.google.com; Secure
쿠키 사용처
사용자 로그인 세션 관리
광고 정보 트래킹
쿠키 정보는 항상 서버에 전송되므로 추가 트래픽 유발
네트워크 트래픽 추가 유발
따라서! 최소한의 정보만 사용(세션 id, 인증 토큰)
서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장하고 싶으면 웹 스토리지 (localStorage, sessionStorage) 참고
localStorage: 데이터를 브라우저에 반영구적으로 저장하며, 브라우저 종료 후 재시작해도 데이터가 남아있음
sessionStorage: 데이터를 브라우저에 저장하나, 브라우저가 닫히면 지워짐
보안에 민감한 데이터는 쿠키에 저장하면 안됨! 웹 스토리지도!
생명주기
쿠키를 평생 보관하지 않고 만료일 넣을 수 있음 (생명주기 관리 가능)
expires, max-age를 줄 수 있음
Set-Cookie: expires=Sat, 26-Dec-2020 ...
만료일이 되면 쿠키 삭제
Set-Cookie: max-age=3600 (초단위)
0이나 음수를 지정하면 쿠키 삭제
세션 쿠키: 만료 날짜 생략하면 브라우저 종료시 까지만 유지
영속 쿠키: 만료 날짜 입력하면 해당 날짜까지 오래 유지
도메인
쿠키에 도메인을 지정해서 특정 도메인 요청에만 보낼 수 있음
도메인을 명시하면 명시한 문서 기준 도메인 + 서브 도메인 모두에게 전송됨 (쿠키 접근)
예) domain=example.org
명시: 명시한 문서 기준 도메인+서브 도메인 포함
domain=example.org를 지정해서 쿠키 생성시, example.org는 물론이고 dev.example.org도 쿠키 접근
생략: 현재 문서 기준 도메인만 적용
example.org 에서 쿠키를 생성하고 domain 지정을 생략하면, example.org 에서만 쿠키 접근할 수 있고, dev.example.org는 쿠키 미접근
경로
도메인 뿐만 아니라, 경로(path) 지정 가능
예) path=/home
이 경로를 포함한 하위 경로 페이지만 쿠키 접근
일반적으로 path=/ 루트로 지정
예)
path=/home 지정
/home -&gt; 가능
/home/level1 -&gt; 가능
/home/level1/level2 -&gt; 가능
/hello -&gt; 불가능
보안
Secure, Httponly, Samesite 속성으로 쿠키 보안 설정 가능
Secure
secure 적용하면 https인 경우에만 전송 (쿠키는 디폴트로 http/https 모두 전송)
HttpOnly
XSS 공격 방지. 원래 javascript에서 쿠키 접근 가능하지만, HttpOnly 사용하면 js가 접근할 수 없음
대신, HTTP 전송에만 사용해서 보안 강화함
따라서, XSS 공격 방지할 수 있음
SameSite
XSRF 공격 방지
요청 도메인과 쿠키에 설정된 도메인이 같은 경우에만 쿠키 전송하도록 제한</p>
<p>참고
모든 개발자를 위한 HTTP 웹 기본 지식 - 김영한</p>