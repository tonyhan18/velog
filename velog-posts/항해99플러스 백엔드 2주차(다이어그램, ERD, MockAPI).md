<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/eef1daac-76e7-46e8-9124-48ecd7f687a8/image.png" /></p>
<p>이번주는 향후 남은 기간동안 진행할 프로젝트를 선정하고 설계하는 시간을 가졌다.
처음 해보는 설계이다보니 과연 내가 하고 있는게 맞을까하는 고민을 많이 해 볼 수 있었다.
그 사이에서 나만의 철학을 발견하기도 했으니 내용을 공유하고자 한다.</p>
<h1 id="과제-발제">과제 발제</h1>
<p>3주차의 발제는 아래와 같다.</p>
<p>시나리오를 선택할 수 있었다. 아래와 같이 세 가지 선택사항이 있었고 각각의 요구사항을 보고 고르면 됐었다.</p>
<p>e-커머스 서비스
콘서트 예약 서비스</p>
<p>여기에서 우리조는 콘서트 예약 서비스를 하기로 결정했다.</p>
<hr />
<p><strong>[ STEP 3 - 분석 ]</strong></p>
<ul>
<li><p>프로젝트 Milestone / 진행계획 작성을 하였는지</p>
</li>
<li><p>시나리오 요구사항을 적절히 분석하고 필요한 다이어그램들을 통해 설계문서를 작성하였는지 ( 시퀀스 다이어그램, ERD 필수 )</p>
<blockquote>
<p>시퀀스 다이어그램 - <strong>시스템 내/외 의 주요 기능상 흐름</strong>을 포함하고 있어야 함
  ERD - 각 시나리오별 기능을 구성하는 <strong>필수적인 데이터 모델들</strong>은 포함하고 있어야 함
  그 외 - 자율</p>
</blockquote>
</li>
</ul>
<p><strong>[ STEP 4 - 실행 ]</strong></p>
<ul>
<li>Mock API 및 Swagger API 가 작성되었는지</li>
<li><strong>(NiceToHave)</strong> API E2E 테스트가 작성되었는지<ul>
<li>이외 모든 내용 포함되어 있으며, BP 선정 기준 정도로 추가해도 괜찮을 것 같습니다.</li>
</ul>
</li>
</ul>
<h1 id="과제를-진행하면서의-고민들">과제를 진행하면서의 고민들</h1>
<p>모든 로직이 중요해 보이는데 매번 토큰을 검사해야 하는가?</p>
<h1 id="결과물-및-피드백">결과물 및 피드백</h1>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/fcdcb4ab-a1ed-47ef-ac06-26fb49559cb6/image.png" /></p>
<p>아무래도 토큰 검사가 매번 필요하지는 않은 모양이다</p>
<h1 id="결과물">결과물</h1>
<p><a href="https://github.com/tonyhan18/hhplus-concert-server-java/tree/step4">github</a></p>
<h1 id="이번주-느낀-점--배운-것">이번주 느낀 점 &amp; 배운 것</h1>
<ul>
<li><p>개발 전 문서화 과정은 굉장히 중요하다!!!!
개발자 뿐만 아니라 모든 이해관계자들과 소통을 유의미 있고 효율적으로 하기 위해서는 꼭 필요한 과정이라 느꼈다.</p>
</li>
<li><p>설계에 충분한 시간을 쓰면 개발은 덤으로 따라온다</p>
</li>
<li><p>created_at, updated_at 은 기본적으로 넣어주기</p>
</li>
<li><p>DB 에 enum 을 사용하는 것보다는 varchar 사용하기
enum 은 특정 DB 에 종속적이며, 변경 사항이 있을 때마다 업데이트를 쳐줘야 하는 등의 작업을 해줘야 한다.</p>
</li>
<li><p>pk 는 bigint 혹은 string(uuid 사용) 표현하자. </p>
<ul>
<li>분산 트랜잭션 환경까지 고려해서 uuid를 사용할 수 있도록 준비하자.</li>
</ul>
</li>
<li><p>데이터베이스에서는 스네이크 케이스 표기법이 기본 권장된다.</p>
</li>
<li><p>GET 요청이더라도, 다양한 프로퍼티를 통해 요청 질의해야 한다면 이를 명시하고 의도적으로 POST 로 작성할 때도 많다. ( 예를 들면 뭐를 조회하는데, 쿼리에 필요한 다양한 요구사항을 수용하는 경우 )</p>
</li>
<li><p>특정 동작을 트리깅하거나, 별도의 리소스가 필요하지 않은 경우 POST 도 RequestBody 를 포함하지 않아도 된다. ( 이건 표준 )</p>
</li>
<li><p>테이블이 많다고 꼭 좋은게 아니다</p>
</li>
</ul>