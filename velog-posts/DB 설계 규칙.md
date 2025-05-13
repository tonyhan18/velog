<blockquote>
<p>DB 설계의 핵심은 &quot;중복을 없애는 것&quot;이다</p>
</blockquote>
<h1 id="1-한-칸에는-한-가지-정보만-들어가도록-만들어라---1">1. 한 칸에는 한 가지 정보만 들어가도록 만들어라 - 1</h1>
<blockquote>
<p>요약</p>
</blockquote>
<ul>
<li>한 칸에는 한 가지 정보만 들어가야 한다.</li>
<li>한 칸에 두 가지 이상의 정보가 들어가있을 땐, 테이블을 분리해서 FK를 활용하면 된다.</li>
<li>특정 테이블에 FK를 도입했을 때 <code>규칙 1</code>이 안 지켜진다면, 다른 테이블로 FK를 옮겨보자.</li>
<li>‘한 가지 정보’의 기준은 절대적이지 않다. 따라서 서비스에 맞게 판단해야 한다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/adb32d3d-264d-44e2-95bf-b0cde4078bf6/image.png" /></p>
<p>예를 들어 위와같이 이메일이라는 컬럼 안에 두 개의 이메일이 들어간 것을 볼 수 있다.</p>
<blockquote>
<p>판매 상품을 조회해서 사용할 때마다 중간에 있는 콤마(,)를 제거하고 배열에 집어넣는 로직을 넣어야 한다. 판매 상품을 삽입할 때든 삭제할 때든 항상 콤마(,)를 신경써서 작업해야 한다. 그리고 한 칸에 데이터를 여러개 집어넣다보면 실수로 데이터를 중복해서 넣어버리기도 한다. 따라서 한 칸에는 한 가지의 정보만 넣으려고 하는 것이다. </p>
</blockquote>
<h3 id="한-칸에-2가지-이상의-정보가-들어가있을-때는-테이블을-분리하자">한 칸에 2가지 이상의 정보가 들어가있을 때는 테이블을 분리하자</h3>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/0bf47a64-509e-47a7-8ae8-e1ec8625cde8/image.png" /></p>
<p>그래서 위와같이 사용자 id를 FK로 분리해서 표에 넣어주자</p>
<blockquote>
<p>이 과정을 보고 데이터베이스 이론에서는 제1정규형</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/10d666da-6df1-4d25-83ae-c76ffbe6c1b5/image.png" /></p>
<p><strong>둘 다 올바른 관점이다. 말 그대로 ‘한 가지 정보’라는 건 절대적이지 않다. 자신의 서비스에 맞게 판단해야 한다.</strong> </p>
<blockquote>
<p>그럼 어떻게 판단해야 할까? 
→ <strong>서비스에서 데이터의 사용 방식에 따라 결정해야 한다!</strong></p>
</blockquote>
<p>예를 들어, 서비스에서 성과 이름을 따로따로 조회해야 하는 경우가 많다면 2번째 테이블의 형태로 구성하는 게 좋다. 반대로 서비스에서 성과 이름을 따로따로 조회할 일이 없고 통째로 쓰는 경우만 있다면 1번째 테이블의 형태로 구성하는 게 좋다.</p>
<h1 id="2-어떤-테이블에-fk를-넣어도-규칙-1을-못-지킬-때는-중간-테이블을-하나-더-만들어라">2. 어떤 테이블에 FK를 넣어도 ‘규칙 1’을 못 지킬 때는 중간 테이블을 하나 더 만들어라</h1>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/b104ee8a-f0c2-4ec8-9d36-ccac1dd6970b/image.png" /></p>
<p>어떤 테이블에 FK를 넣어도 ‘규칙 1’을 못 지킬 때는 중간 테이블을 하나 더 만들어야 한다. </p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/a441e886-66cd-4548-9cc3-981c6863fbd3/image.png" /></p>
<h1 id="규칙-3-헷갈릴-땐-관계11-1n-nm를-파악해봐라---1">[규칙 3] 헷갈릴 땐 관계(1:1, 1:N, N:M)를 파악해봐라 - 1</h1>
<p>엔티티 간의 관계에서 패턴을 찾은 것이다. 그게 바로 1:1 관계, 1:N 관계, N:M 관계라는 패턴</p>