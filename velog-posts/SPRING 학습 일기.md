<h1 id="필수적인-패키지들">필수적인 패키지들</h1>
<p>lombok</p>
<h1 id="일반-spring">일반 Spring</h1>
<h2 id="requiredargsconstructor">RequiredArgsConstructor</h2>
<p>C#에서 <code>RequiredArgsConstructor</code>와 유사한 기능은 <strong>생성자 자동 생성</strong>을 지원하는 기능으로 간주할 수 있으며, 이는 <strong><a href="https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-9#record-types">Record</a></strong>나 <strong>Primary Constructor(주 생성자)</strong>와 같은 C#의 특정 기능을 통해 구현할 수 있습니다.
<code>RequiredArgsConstructor</code>는 클래스의 <code>final</code> 필드나 명시적으로 <code>@NonNull</code> 필드에 대해 <strong>자동으로 생성자</strong>를 만들어주는 Lombok의 애노테이션입니다. C#의 기능 중에는 다음과 같은 방법이 비슷한 역할을 수행할 수 있습니다.</p>
<h2 id="autowired">Autowired</h2>
<p>Spring Framework에서 <strong>오토와이어링(AutoWiring)</strong>이란 <strong>의존성 주입(Dependency Injection)</strong>을 자동으로 처리해주는 기능을 말합니다. 개발자가 객체를 수동으로 생성하고 연결하지 않아도, Spring이 애플리케이션 컨텍스트(Application Context)에서 적절한 <code>Bean</code>을 찾아 자동으로 연결(연관)해 줍니다. </p>
<h3 id="오토와이어링의-핵심-개념">오토와이어링의 핵심 개념</h3>
<p><strong>의존성 주입(Dependency Injection)</strong>은 클래스가 다른 클래스(종속된 객체)와 협력해야 할 때, 그 객체를 해당 클래스가 직접 생성하지 않고 외부에서 주입받는 방식입니다. 오토와이어링은 이 의존성 주입을 Spring이 자동으로 처리해 주는 기능입니다.</p>
<p>Spring은 애플리케이션 실행 시점에, 특정 객체가 필요로 하는 의존성을 주입할 수 있도록 <strong>Bean</strong>을 관리하고, 이를 자동 매칭(Auto-Wiring)하여 연결합니다.</p>
<hr />
<h3 id="왜-오토와이어링을-사용할까">왜 오토와이어링을 사용할까?</h3>
<ul>
<li>객체 간 의존성을 수동으로 해결하지 않아도 되기 때문에 코드를 간결하고 관리하기 쉽게 만듭니다.</li>
<li>설계 원칙인 <strong>의존성 주입(DI)</strong>과 <strong>제어의 역전(IOC)</strong>를 구현하는 기본 도구 중 하나입니다.</li>
<li>애플리케이션이 더 유연하고 테스트 가능해집니다. (Mocking 등을 이용하여 테스트하기 쉬워짐)</li>
</ul>
<h4 id="빈이-생성되지-않았거나-구성되지-않음"><strong>빈이 생성되지 않았거나 구성되지 않음</strong></h4>
<p>Spring Bean으로 등록되지 않은 객체는 <code>Autowired</code>를 통해 주입될 수 없습니다.
이 문제는 주로 클래스에 <code>@Component</code>, <code>@Service</code>, <code>@Repository</code>, <code>@Configuration</code> 같은 Spring 관리 애노테이션을 누락하거나, 클래스가 Spring Component Scan 경로에 포함되지 않을 때 발생합니다.</p>
<hr />
<h1 id="테스트">테스트</h1>
<h3 id="springboottest-">*<em><code>@SpringBootTest</code> *</em></h3>
<p><code>@SpringBootTest</code>는 Spring Boot 기반 테스트를 위한 어노테이션입니다. 이 어노테이션을 사용하면 <strong>Spring Context (애플리케이션 컨텍스트)</strong>가 로드되고, 테스트는 애플리케이션 전체를 대상으로 동작할 수 있게 됩니다.</p>
<ul>
<li><strong>통합 테스트 용도</strong>: 실제 애플리케이션과 유사한 환경에서 테스트를 실행하려고 할 때 사용됩니다. 스프링 컨텍스트를 초기화하며, 빈들(bean, 컴포넌트, 서비스, 리포지토리 등)이 로드됩니다.</li>
<li><strong>기본적으로 애플리케이션을 로드함</strong>: 테스트가 설정 파일(<code>/application.properties</code> 또는 <code>/application.yml</code> 등)을 읽고, <code>@SpringBootApplication</code> 설정을 기반으로 컨텍스트를 생성합니다.</li>
</ul>
<h3 id="autoconfiguremockmvc-">*<em><code>@AutoConfigureMockMvc</code> *</em></h3>
<p><code>@AutoConfigureMockMvc</code>는 Spring Boot 테스트 환경에서 <strong>MockMvc</strong>를 자동 구성하기 위한 어노테이션입니다.</p>
<h4 id="mockmvc란">MockMvc란?</h4>
<ul>
<li>MockMvc는 Spring MVC 애플리케이션에서 HTTP 요청과 응답을 <strong>가볍게(mocking) 테스트</strong>할 수 있는 도구입니다.</li>
<li>실제 서버를 실행하지 않고도 컨트롤러의 동작(예: RESTful API 엔드포인트)을 테스트할 수 있습니다.</li>
</ul>