<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/f1a4b0dd-3692-48f8-9361-7420dac2e765/image.png" /></p>
<blockquote>
<p>본 게시글은 인프런의 모든 개발자를 위한 HTTP 웹 기본 지식 (김영한) 강의를 듣고 정리한 내용입니다.</p>
</blockquote>
<h1 id="http-기본">HTTP 기본</h1>
<p><strong>HTTP는 hypertext transfer protocol의 약자</strong>로, 초기에는 HTML 등 링크를 통해 연결 할 수 있는 문서 (하이퍼텍스트)를 전송하는 프로토콜로 시작하였다. 다만, 현재는 모든 형태의 데이터를 전송하는 프로토콜로 사용중이며, <strong>HTML 뿐만 아니라, TEXT, image, 음성, 영상, 파일, JSON, XML 형식의 데이터를 모두 전송할 수 있다.</strong> 또한, 서버간 통신을 할 때도 대부분 http 프로토콜로 연결하고 있다. (이전 게시글에서 배운 TCP는 게임 서버 등 특정 상황에서만 사용한다.)</p>
<h2 id="http-역사">HTTP 역사</h2>
<p>그렇다면 HTTP는 언제 어떻게 시작되었을까? 간단히 역사를 알아보자면 아래와 같다:</p>
<ul>
<li>HTTP/0.9 1991년: GET 메서드만 지원, HTTP 헤더X</li>
<li>HTTP/1.0 1996년: 메서드, 헤더 추가</li>
<li>HTTP/1.1 1997년: 가장 많이 사용, 우리에게 가장 중요한 버전
RFC2068 (1997) -&gt; RFC2616 (1999) -&gt; RFC7230~7235 (2014) HTTP/2 2015년: 성능 개선</li>
<li>HTTP/3 진행중: TCP 대신에 UDP 사용, 성능 개선</li>
</ul>
<p>위 버전중에 가장 중요한 HTTP는 1997년에 나온 HTTP/1.1이다. HTTP/1.1 버전에 우리가 사용하는 거의 모든 HTTP 기능이 들어있으며, 이후에 나온 버전들은 거의 개선에 초점을 두었다.</p>
<p>이 HTTP 1.1 도 사용기간이 오래되다보니 관심처럼 굳어진 부분들이 있다. 뒤에서 자세하게 알아보자.</p>
<p>HTTP가 기반하는 프로토콜은 버전마다 다른데, HTTP/1.1, HTTP/2는 TCP를 기반으로 작동하며, HTTP/3 부터는 속도를 빠르게 개선하기 위해 UDP 기반으로 작동한다. 다만 아직까지는 주로 HTTP/1.1를 사용하고 있다. 각 HTTP가 어떤 버전인지는 개발자 도구의 네트워크 탭에서 어떤 버전을 쓰는지 protocol을 열어서 확인할 수 있다.</p>
<p><img alt="크롬 개발자도구" src="https://velog.velcdn.com/images/tonyhan18/post/bba04159-a7bf-40d1-8e35-1f2a31966540/image.png" /></p>
<p>HTTP 특징으로는 크게 다섯가지가 있다. 우선 HTTP는 클라이언트 서버 구조, 즉 클라이언트가 서버에 HTTP 요청을 보내고, 서버에서 결과를 만들어 응답이 오면 응답 결과를 열어서 동작하는 Request Response 구조로 구성되어있다.
또한, HTTP는 무상태 프로토콜이며 비연결성이라는 특징을 가지고 있다. HTTP 메세지를 통해서 통신한다는 점과 단순하고 확장 가능점도 특징중 하나이다. 해당 특징들을 하나하나 살펴보며 HTTP에 대해서 더 자세히 알아보자.</p>
<h2 id="클라이언트-서버-구조">클라이언트 서버 구조</h2>
<p><img alt="클라이언트 서버 구조" src="https://velog.velcdn.com/images/tonyhan18/post/8c0d7f42-9509-48ac-af91-6a0aaf12766c/image.png" /></p>
<p>HTTP는 클라이언트가 서버에 HTTP 요청을 보내고, 서버에서 결과를 만들어 응답이 오면 응답 결과를 열어서 동작하는 클라이언트 서버 구조로 분리되어있다. </p>
<p>클라이언트와 서버 개념을 분리하는게 중요한데, HTTP 덕분에 비즈니스 로직이랑 데이터 로직은 서버에, 클라이언트는 UI에 집중할 수 있게 되었다.</p>
<h3 id="무상태-프로토콜-stateless">무상태 프로토콜 (Stateless)</h3>
<p>HTTP는 상태를 저장하지 않는 무상태 프로토콜이다. 무상태 프로토콜이란, 서버가 클라이언트 상태를 보존하지 않는 것을 뜻한다. 무상태의 장점은 서버가 상태를 저장하거나 의존하지 않기 때문에 확장성이 높아진다는 것이다. 반면에, 단점은 클라이언트의 상태를 매번 알려줘야 하기 때문에 추가 데이터를 전송해야 한다는 것이다.</p>
<p>Stateless의 예시를 Stateful이라는 반대 단어와 비교해서 알아보자.</p>
<h4 id="stateful">Stateful</h4>
<ul>
<li>예를 들어, 노트북 매장에서 두 개의 노트북을 신용카드로 결제한다고 해보자. A라는 직원에게 두 노트북을 요청하고 결제까지 같은 직원에게 한다면 원활하게 결제까지 완료할 수 있다.</li>
<li>반면에, A라는 직원이 중간에 B라는 직원으로 교체된다면 문제가 생길 수 있다. '노트북 두개를 신용카드로 산다'는 상태는 A직원만 알고있기 때문이다. 따라서 B 직원이 오면 어떤 상품을 어떤 수단으로 결제해야하는지 A직원을 통해 인수인계를 받거나, 클라이언트가 다시 알려주어야 한다.</li>
</ul>
<p><img alt="stateful" src="https://velog.velcdn.com/images/tonyhan18/post/34420d80-bfca-40ad-8999-4f03a7e93db6/image.png" /></p>
<p>이미지 출처: 모든 개발자를 위한 HTTP 웹 기본 지식 (김영한)</p>
<h4 id="stateless">Stateless</h4>
<ul>
<li>다시 노트북 예시를 들어보다. 동일한 상황에서 무상태일 경우, 노트북 두개를 신용카드로 사고싶다는 얘기를 매 단계마다 해야한다. '노트북 두개를 신용카드로 사고 싶다'는 내용을 구체적으로 매번 말하게 된다면 중간에 점원이 B, C로 바뀌어도, 어떤 내용인지 인식할 수 있기 때문에 문제가 없다.</li>
<li>다만, 매번 '노트북 두개를 신용카드로 사고 싶다'는 상태를 상대방에게 알려야 한다는 번거로움이 있다.</li>
</ul>
<p><img alt="stateless" src="https://velog.velcdn.com/images/tonyhan18/post/85cfaf92-f4c7-4a2e-8b85-83e9ed34d534/image.png" /></p>
<p>결국, stateful한 경우 항상 같은 서버를 호출해야한다. 서버가 정보를 저장하고 있기 때문에 중간에 서버 장애가 나면 큰일난다. (중간에 직원이 갑자기 바뀌는 경우). 반대로, stateless의 경우 다른 서버 (B, C 직원)로 변경되어도 흐름을 이어가는데 문제가 생기지 않는다. 호출할 때 마다 원하는 정보를 모두 전달하기 때문에 서버가 바뀌어도 괜찮다. 따라서, 무상태일 경우에 스케일 아웃하기더 쉬워진다 (무한한 서버 증설 가능).</p>
<p>다만, 실무에서는 모든것을 무상태로 설계할 수 없는 경우가 있다. 예를 들어 로그인을 한 상태를 매번 요청마다 전달해야하는 경우에는 매번 상태 데이터를 넘겨줘야하기 때문에, 데이터를 너무 많이 넘긴다는 단점이 있다.</p>
<h1 id="비-연결성connectionless">비 연결성(connectionless)</h1>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/cee58ba1-991e-4189-ac0d-379c31a710fe/image.png" /></p>
<p>마지막으로, HTTP는 비연결성 (connectionless)라는 특징이 있다. 기본적으로 연결을 유지해야하는 TCP/IP와는 반대의 개념이다. TCP/IP의 경우, 서버 연결이 계속 유지되므로 서버 자원이 소모된다는 단점이 있다. </p>
<blockquote>
<p>다시 말해, HTTP는 서버 연결을 유지 하지 않아도 되어, 최소한의 자원을 유지할 수 있다는 장점이 있다.
비연결성이라는 HTTP의 특징 덕분에 한번 서버에 요청을 하더라고, 그 이후에 연결을 유지하지 않는다. </p>
</blockquote>
<p>따라서, 초 단위 이하의 빠른 속도로 응답할 수 있으며, 1시간 동안 수천명이 서비스 사용해도 실제 서버 동시 처리 요청은 수십개 이하로 매우 작다. (ex. 동시에 검색 버튼 여러번 누르지 않듯이). 즉, HTTP는 서버 자원을 매우 효율적으로 사용할 수 있는 프로토콜이다.</p>
<p><img alt="비연결성" src="https://velog.velcdn.com/images/tonyhan18/post/f73b90e2-3599-486a-b8b5-c172d1c2725c/image.png" /></p>
<p>다만, 비연결성의 한계점도 존재한다. HTTP는 클라이언트와 서버가 서로 연결을 유지하지 않기 때문에, TCP/IP 프로토콜에 따라 연결과 종료를 반복할때 요청에 대한 응답을 여러번 반복하게 되면서 서버의 자원과 시간(3 way handshake 시간)이 낭비된다. 또한, 웹 브라우저 요청 시 HTML 하나만 받아오는게 아니라, 자바스크립트, css, 이미지등 수많은 파일들을 불러오는데, 연결이 되지 않는다면 파일 하나하나당 매번 요청을 보내야한다는 불편함이 있다.</p>
<p><img alt="지속 연결" src="https://velog.velcdn.com/images/tonyhan18/post/d8f4d6a7-d981-474b-a766-92da0f905ff2/image.png" /></p>
<p>이러한 문제점을 개선하고자, HTTP/1.1 버전부터는 Keep-Alive 라는 기능을 이용해 지속 연결(Persistent Connection) 방식을 도입하게 되었다. 아래 사진과 같이 여러개의 HTTP 요청과 응답을 서버, 클라이언트간 연결을 유지하면서 더 효율적으로 처리하게 되었다.</p>
<h1 id="http-메시지">HTTP 메시지</h1>
<p>HTTP 메세지는 요청 메세지와 응답 메세지 크게 두 종류로 나뉘어져 있다. 아래와 같이 요청 / 응답 메세지 형태가 조금씩 다르게 나타나고, 기본적인 구조는 다음과 같다:</p>
<ul>
<li>시작 라인 (start-line)</li>
<li>헤더 (header)</li>
<li>공백 라인 (CRLF, empty line)</li>
<li>바디 (message body)</li>
</ul>
<p><img alt="http 메시지 구성" src="https://velog.velcdn.com/images/tonyhan18/post/da1cc889-11ee-4d6f-b5d5-c95362a7962f/image.png" /></p>
<p>위 네가지 구조가 구체적으로 어떻게 구성되어있는지 확인해보자.</p>
<p><strong>시작 라인</strong>
시작 라인은 크게 request-line / status-line으로 구분된다. 구체적으로, 요청 메세지인지 응답 메세지인지에 따라서 request / status로 내용 구성이 변경된다.</p>
<p><strong>[요청 메세지]</strong>
요청 메세지는 request-line이다. 이때, request-line 구조는 method SP (공백) request-target SP HTTP-version CRLF(엔터)로 구분이 된다. 요청 메세지에 들어갈 수 있는 HTTP 메서드는 GET, POST, PUT, DELETE 등 여러가지가 있으며, 요청 대상은 절대 경로와 쿼리를 조합해서 작성할 수 있다. 또한, 요청 메세지 시작 라인에는 HTTP 버전 정보가 함께 들어간다.</p>
<p>[<strong>응답 메세지]</strong>
응답 메세지는 status-line으로 응답이 온다. statue-line 구조는 다음과 같다: HTTP-version SP status-code SP reason-phrase CRLF. 응답 메세지의 시작 라인에서는 HTTP 상태 코드가 오는데, 요청 성공, 혹은 실패를 나타낸다. (200 성공, 400 클라 요청 오류, 500 서버 내부 오류)</p>
<p><strong>헤더</strong></p>
<p><img alt="헤더" src="https://velog.velcdn.com/images/tonyhan18/post/cc61db6b-0b92-4045-b210-9fa8aaae6414/image.png" /></p>
<p>HTTP 헤더는 HTTP 전송에 필요한 모든 부가 정보를 담기 위해 생성된다. 예를 들어, 메세지의 바디 내용, 크기, 압축, 인증, 요청 클라 정보, 서버 정보, 캐시 관리 등등 여러 부가적인 정보가 들어간다. 적용할 수 있는 표준 헤더 종류는 굉장히 많고, 임의 헤더를 추가해서 보낼 수도 있다</p>
<p><strong>HTTP 메세지 바디</strong>
마지막으로 HTTP 메세지 바디는 실제 전송할 데이터를 담고있다. 예를 들어, HTML 문서, 이미지, 영상, JSON 등 byte로 표현할 수 있는 모든 데이터가 바디가 될 수 있다.</p>
<p>결국, HTTP는 매우 단순하고 확장 가능한 기술이다.</p>
<hr />
<p>참고
모든 개발자를 위한 HTTP 웹 기본 지식 (김영한)</p>