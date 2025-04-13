<pre><code>오라클 다운로드는 정말 신중하게 해야 한다.
필자는 오라클 설치하다 날려먹은 기억이 너무 많아서 항상 신중에 신중을 가해서 설치하곤 한다.</code></pre><p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/6a4f5436-d33b-4d3a-ba9f-fa0896a7a828/image.png" /></p>
<p>먼저 폴더는 위와같이
<code>developer &gt; DataBase &gt; Oracle</code> 위치를 하는 것을 추천한다.
특별한 이유는 없고 관리를 위해서이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/7f339510-b87f-4dc0-b6f6-55bd8c14fa29/image.png" /></p>
<p>폴더에 들어가면 setup 이 있는데
반드시! 관리자 권한으로 실행 해야한다.
이렇게 안하면 간혹가다가 프로그램 설치 중간에 멈추기 때문에 필연적인 과정이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/a23fdbb5-00a7-461a-ba57-2f03b5f4a033/image.png" /></p>
<p>이 옵션의 경우 RAC로 DB를 설치할 것인가에 대한 질문이다.
지금은 학습 용도이기 때문에 선택하지 않을 것이지만 후에 RAC 설치 부분만 추가로 넣고자 한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/d16bbb5a-d608-46c0-83e4-e43eb86dc78b/image.png" /></p>
<p><a href="https://myalpaca.tistory.com/17">https://myalpaca.tistory.com/17</a></p>
<p>RAC란 쉽게 말해서 하나의 DB를 여러개의 인스턴스(DBMS - ex.ORACLE)에서 접근 가능하도록 만드는 방법이다. 이를 위해서 Disk를 외부에 두는 등의 행위가 필요하다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/ed85a183-2e8a-4139-9277-f8a7b52aabd0/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/0841fd39-1578-4e3c-aeda-ba7a1eea4161/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/c3e53d9b-dfa0-4a70-9570-d2026fec8518/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/93baa1d7-b4c8-44a8-a234-851fb3403efc/image.png" /></p>
<p>비밀번호는 <code>oracle</code>로 작성하였다.
가급적 <code>컨테이너 데이터베이스로 생성</code>을 꺼주자. 19c 버전의 특징인데 DB를 container 형태로 관리할 수 있다.</p>
<p>컨테이너니 좋아보이지만 우리같은 개인은 이 기술을 경험해보기 쉽지 않고(그만큼 데이터도 없고)
그냥 진행시 굉장히 SQL 문법에 오류를 많이 일으켜서 나는 좋아하지 않는다.</p>
<p>단순하게 개발 및 테스트 용도로 사용한다면 끄는 것이 좋다고 본다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/745d30f8-9174-4423-8ecc-da26ca378ff4/image.png" /></p>
<p>결과적으로 이렇게 요약본이 나오게 된다.
이제 설치를 진행해주자.</p>
<hr />
<h1 id="sql-developer-설치">SQL Developer 설치</h1>
<p>이제 DBMS(oracle 19c)를 컨트롤 할 수 있는 DBA 도구를 설치하겠습니다.</p>
<p><a href="https://www.oracle.com/kr/database/sqldeveloper/technologies/download/">https://www.oracle.com/kr/database/sqldeveloper/technologies/download/</a>
우선은 위의 페이지에 접속하여 SQL 도구를 다운 받아줍니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/a8b36f8b-cc38-4207-b339-b097cf4e0380/image.png" /></p>
<p>Oracle 접속을 새롭게 만들어줍니다.</p>
<h1 id="데이터-넣기">데이터 넣기</h1>
<p><a href="https://1drv.ms/u/c/c4cf260a44b497fb/ESkvae8dTKlNoqsa94s6l5EBe2OFxrlPa3yxfUSkp76NsA?e=CHZ1zp">https://1drv.ms/u/c/c4cf260a44b497fb/ESkvae8dTKlNoqsa94s6l5EBe2OFxrlPa3yxfUSkp76NsA?e=CHZ1zp</a></p>
<p>위 링크로 가서 파일을 다운 받아 C 폴더에 풀어줍니다.
<img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/09228591-60da-4bc3-8fef-98376c7cbc7e/image.png" /></p>
<p>이 파일을 oracle DB에 Import 시켜주겠습니다.</p>
<p>SQL Plus 를 먼저 열고 system으로 접속해줍니다.</p>
<pre><code class="language-sql">CREATE OR REPLACE DIRECTORY data_dir AS 'C:\labs' ; 
host impdp system/oracle directory=data_dir dumpfile=sqlt01.dmp </code></pre>
<p>위쪽 쿼리를 실행시켜주겠습니다.
<img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/b9bcadd6-4109-4ec6-8a19-f15c2324dba0/image.png" /></p>
<p>그러면 데이터가 자동 삽입되는 것을 확인할 수 있습니다.</p>
<h1 id="데이터-확인">데이터 확인</h1>
<p>다시 SQL Developer 로 와서 접속해줍니니다.</p>
<ul>
<li>username : SQLT01</li>
<li>password : oracle</li>
<li>hostname : localhost</li>
<li>port : 1521(또는 1621)</li>
<li>SID : orcl</li>
</ul>
<p>그리고 간단한 쿼리문이나 도구를 활용해 데이터가 들어온 것을 확인해줍니다.</p>
<h1 id="기본-셋팅">기본 셋팅</h1>
<p>쿼리 튜닝을 위해서는 만들어놓은 파일 중 xplan을 사용해야 합니다.</p>
<p>그래서 Default Dir 를 SQL Developer에 셋팅해줄 필요가 있습니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/7b235092-f021-4241-8dad-e449b23ed171/image.png" /></p>
<p>도구 &gt; 환경설정 &gt; 데이터베이스 &gt; 워크시트
경로에 가보면 스크립트를 찾을 기본 경로를 선택할 수 있습니다.
여기에서 우리 압축을 풀어놓은 labs 폴더를 경로로 추가합니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/1265c435-2b48-41c4-83ec-2bace2611fff/image.png" /></p>
<pre><code class="language-sql">select * from employees;
@xplan</code></pre>
<p>프로그램 실행시 Analyze까지 함께 진행되는 것을 확인할 수 있습니다.</p>