<p>제가 생각하는 클린 + 레이어드
&quot;간단&quot;하다.
선만 안 넘으면 된다.</p>
<ol>
<li>패키지로 감는다.</li>
</ol>
<p>/interfaces &lt;-- 피상계층 ( 제일 바깥에 있는 애들... )
    /api
        /concert
            ConcertController.java
        /user
            UserController.java
    /scheduler
        /concert
            ConcertScheduler.java
    /consumer
    ..</p>
<hr />
<p>(표현) Presentation 계층 ( Business Usecase 계층만 호출 가능 )</p>
<hr />
<p>Business 계층</p>
<hr />
<p>/application &lt;-- 응용 계층 ( Facade, Usecase )
    /concert &lt;-- 이 주체는 어떻게 정하는데요? 주인 도메인이 어디냐..
        ConcertFacade.java
    /user
        UserFacade.java</p>
<hr />
<p>(응용) Business Usecase 계층</p>
<hr />
<p>/domain
    /concert
        Concert.java
        ConcertSchedule.java // 콘서트 공연 도메인 객체
        ConcertService.java
        ConcertRepository.java // interface</p>
<hr />
<p>(도메인) Business Domain 계층 ( 애플리케이션의 &quot;핵&quot; = Core )</p>
<hr />
<hr />
<p>[[[[[[ 스프링이 메꿔줌 Dependency Injection ]]]]]</p>
<p>/infrastructure
    /concert
        ConcertRepositoryImpl.java
        ConcertJpaRepository.java
        ConcertXXRepository.java</p>
<hr />
<p>(근간..등등) Infrastructure 계층 ( Business Domain 계층을 알고 있음 )</p>
<hr />
<p>Presentation -&gt; Application -&gt; Domain &lt;- Infrastructure
(입출력)                                           (입출력)</p>
<p>비즈니스는 &quot;입출력&quot; 에 의존해서는 안된다.
&quot;입출력&quot; 의 방식이 변경되어도 비즈니스는 영향을 받으면 안된다.
&quot;추상화&quot; 를 활용하면 된다.</p>
<p>비즈니스는 &quot;추상적&quot; 으로 어떻게 입출력될지만 알고 있고.
실제 입출력은 &quot;구현&quot; 된 후, 스프링에 의해 주입되면 된다.</p>
<ol>
<li>왜 도메인 지켜? -&gt; 우리 애플리케이션의 진짜 핵심, 이유</li>
<li>인프라스트럭쳐, 프레젠테이션 (입출력) -&gt; 언제든 바뀔 수 있다.</li>
</ol>
<p>HTTP WEB 통신 -&gt; @RestController
이건 언제든 비즈니스는 동일하되 CLI 로 바뀔 수도 있고
gRPC 로 바뀔 수도 있고...</p>
<p>하지만 비즈니스는 &quot;불변&quot;</p>
<p>Domain = 왕 / 싸장님
Application = 비서
Presentation = 전화기 / 핸드폰
Infrastructure = 도구 ( 언제든 바뀔 수 있는 도구 )</p>
<p>Domain, Application =&gt; 이번 과제
외부 IO 없이 테스트가 가능한 영역 ( 단위테스트, 통합테스트를 DB 든 뭐든 필요 없다 이거야.. )</p>
<p>이제 DB 를 붙여야징!
--&gt; Domain, Application 수정해야해? 없다.</p>
<hr />
<p>Presentation</p>
<ul>
<li>Controller</li>
</ul>
<hr />
<p>Application</p>
<ul>
<li>Service</li>
</ul>
<hr />
<p>Domain</p>
<ul>
<li>Entity</li>
<li>Repository</li>
</ul>
<hr />
<p>Infrastructure</p>
<ul>
<li>RepositoryImpl</li>
</ul>
<hr />
<p>class 준규서비스 {
    준규Repository // interface
    형재Repository // interface
}</p>
<ol>
<li>Presentation 계층 (프레젠테이션 계층)
사용자와 가장 가까운 계층, UI 또는 API 요청을 처리하는 역할</li>
</ol>
<p>무엇을 하냐?
사용자의 입력을 받고, 응답을 반환함.
웹이라면 Controller나 View, REST API 등이 여기에 해당됨.</p>
<p>예시
사용자가 /order로 주문을 요청 → OrderController가 요청을 받고 처리 흐름 시작.</p>
<p>기술 예시
Spring Boot의 @RestController, Blazor의 Razor 페이지 등</p>
<ol start="2">
<li>Application 계층 (애플리케이션 계층)
비즈니스 로직의 흐름을 조정하는 역할</li>
</ol>
<p>무엇을 하냐?
유저의 요청을 받아서 도메인 객체를 호출하고, 작업 순서를 관리함.
자체적인 비즈니스 로직은 거의 없고, 도메인 계층을 이용해서 원하는 작업을 orchestration 함.</p>
<p>예시
주문 요청을 받으면, 재고 확인 → 결제 → 주문 등록 등의 흐름을 조정</p>
<p>기술 예시
Service 클래스 (OrderService, PaymentService 등)</p>
<ol start="3">
<li>Domain 계층 (도메인 계층)
핵심 비즈니스 로직이 구현되는 계층, 시스템의 핵심 규칙이 여기에 있음</li>
</ol>
<p>무엇을 하냐?
실제 업무 규칙을 구현하고, 도메인 모델(Entity, Value Object, Aggregate 등)을 정의함.</p>
<p>예시
Order, Item, User와 같은 객체들이 있고,
&quot;한 사용자는 하루에 3번만 주문할 수 있다&quot; 같은 규칙이 여기에 구현됨.</p>
<p>기술 예시
Java 클래스들 (Entity, Domain Service, Value Object 등)</p>
<ol start="4">
<li>Infrastructure 계층 (인프라 계층)
외부 시스템과의 연결, 기술적 세부 구현을 담당</li>
</ol>
<p>무엇을 하냐?
DB 접근, 메시지 브로커, 외부 API 호출 등 기술적인 작업을 실제로 수행함.
Application이나 Domain에서 필요한 기능들을 실제로 수행할 수 있게 도와주는 계층임.</p>
<p>예시
OrderRepositoryImpl이 JPA를 이용해 DB에 주문을 저장함.
또는 외부 결제 시스템(PG)과 연동함.</p>
<p>기술 예시
Spring Data JPA, Redis, Kafka, AWS SDK, 외부 API 클라이언트 등</p>
<p>요약 구조</p>
<pre><code>[Presentation] → [Application] → [Domain] ←→ [Infrastructure]
        ↓               ↓              ↓              ↑
   사용자 요청      흐름 조정      핵심 로직     기술적 구현</code></pre><p>필요하면 그림으로도 정리해줄게. 이해 안 되는 계층 있으면 더 자세히 파볼 수 있어.</p>
<hr />
<p>✅ 유즈케이스 (Use Case)
“사용자의 목적을 이루는 비즈니스 흐름”
→ 하나의 구체적인 행위를 정의하고 실행하는 책임</p>
<p>예: &quot;회원가입&quot;, &quot;상품 주문&quot;, &quot;비밀번호 변경&quot;</p>
<p>형태: OrderUseCase, SignupService, LoginUseCase 등</p>
<p>역할:</p>
<p>도메인 객체를 이용해 비즈니스 플로우를 조정</p>
<p>필요시 인프라 계층 호출(DB 저장, 외부 API 호출)</p>
<p>특징: 유저의 액션 단위로 쪼개져 있음</p>
<p>✅ 파사드 (Facade)
“여러 유즈케이스나 서비스, 컴포넌트를 통합한 하나의 진입점”
→ 복잡한 내부 흐름을 감추고, 단순한 API로 제공</p>
<p>예: OrderFacade, UserFacade</p>
<p>역할:</p>
<p>여러 유즈케이스를 묶어서 더 고수준의 기능 제공</p>
<p>외부에서 사용할 때 의존성을 단순화</p>
<p>언제 쓰냐:</p>
<p>클라이언트가 여러 서비스를 직접 호출하지 않게 하려는 경우</p>
<p>테스트하기 쉽게 인터페이스를 단순화하고 싶은 경우</p>