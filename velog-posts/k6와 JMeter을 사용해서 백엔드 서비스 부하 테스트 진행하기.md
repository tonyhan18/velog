<p>네, k6와 JMeter를 사용하여 .NET API에 부하 테스트를 수행하는 방법을 각각 안내해 드릴게요. k6는 코드로 간단하고 빠르게, JMeter는 GUI로 복잡하고 정교하게 테스트하는 데 강점이 있습니다.</p>
<h2 id="🚀-k6-사용법-개발자-친화적인-코드-기반">🚀 k6 사용법 (개발자 친화적인 코드 기반)</h2>
<p>k6는 JavaScript로 테스트 스크립트를 작성하여 터미널에서 실행하는 최신 부하 테스트 도구입니다.</p>
<h3 id="1-k6-설치">1. k6 설치</h3>
<p>운영체제에 맞게 설치합니다.</p>
<ul>
<li>Windows: winget install k6 또는 choco install k6</li>
<li>macOS: brew install k6<h3 id="2-테스트-스크립트-작성">2. 테스트 스크립트 작성</h3>
프로젝트 폴더에 script.js와 같은 이름으로 파일을 생성하고 아래 코드를 작성합니다.</li>
</ul>
<pre><code>// script.js
import http from 'k6/http';
import { check, sleep } from 'k6';

// 1. 테스트 옵션 설정
export const options = {
  // vus: 가상 사용자 수
  vus: 100,
  // duration: 테스트 지속 시간
  duration: '30s',
  // thresholds: 성능 목표 (예: HTTP 에러율 1% 미만, 95%의 요청이 200ms 안에 처리)
  thresholds: {
    'http_req_failed': ['rate&lt;0.01'], // HTTP 에러율이 1% 미만이어야 함
    'http_req_duration': ['p(95)&lt;200'], // 95%의 요청이 200ms 안에 처리되어야 함
  },
};

// 2. 테스트 시나리오 정의 (가상 사용자가 실행할 코드)
export default function () {
  // 테스트할 .NET API 엔드포인트로 변경하세요.
  const res = http.get('https://my-api.com/products/1');

  // 응답 검증
  check(res, { 'status was 200': (r) =&gt; r.status == 200 });

  // 다음 요청 전 1초 대기
  sleep(1);
}</code></pre><h3 id="3-테스트-실행">3. 테스트 실행</h3>
<p>터미널에서 아래 명령어를 실행합니다.</p>
<pre><code>k6 run script.js</code></pre><h3 id="4-결과-확인">4. 결과 확인</h3>
<p>테스트가 끝나면 터미널에 결과가 요약되어 나옵니다.</p>
<ul>
<li>http_req_duration: 요청의 평균, 최소, 최대 응답 시간. p(95)&lt;200 같은 목표를 달성했는지 확인합니다.</li>
<li>http_req_failed: 실패한 요청의 비율.</li>
<li>vus: 테스트에 사용된 가상 사용자 수.</li>
<li>http_reqs: 테스트 시간 동안 보낸 총 요청 수.</li>
</ul>
<h2 id="🐘-jmeter-사용법-강력한-gui-기반">🐘 JMeter 사용법 (강력한 GUI 기반)</h2>
<p>JMeter는 GUI를 통해 테스트 계획을 수립하는 자바 기반의 전통적인 부하 테스트 도구입니다.</p>
<h3 id="1-jmeter-설치-및-실행">1. JMeter 설치 및 실행</h3>
<ul>
<li>Java 설치: JMeter는 Java가 필요하므로 먼저 JDK 8 이상 버전을 설치합니다.</li>
<li>JMeter 다운로드: Apache JMeter 공식 사이트에서 최신 버전의 zip 파일을 다운로드하고 압축을 풉니다.</li>
<li>실행:<ul>
<li>Windows: bin 폴더의 jmeter.bat 파일을 실행합니다.</li>
<li>macOS/Linux: bin 폴더에서 jmeter.sh를 실행합니다.<h3 id="2-테스트-계획test-plan-수립">2. 테스트 계획(Test Plan) 수립</h3>
JMeter GUI 화면에서 마우스 오른쪽 클릭으로 요소를 추가하며 테스트를 설계합니다.</li>
</ul>
</li>
<li>Thread Group 추가:<ul>
<li>Test Plan 우클릭 → Add → Threads (Users) → Thread Group</li>
<li>Number of Threads (users): 가상 사용자 수 (예: 100)</li>
<li>Ramp-up period (seconds): 모든 사용자를 생성하는 데 걸리는 시간 (예: 10초면 1초에 10명씩 투입)</li>
<li>Loop Count: 각 사용자가 테스트를 반복할 횟수 (무한 반복은 Infinite)</li>
</ul>
</li>
<li>HTTP Request Sampler 추가:<ul>
<li>방금 만든 Thread Group 우클릭 → Add → Sampler → HTTP Request</li>
<li>Protocol: https</li>
<li>Server Name or IP: my-api.com (테스트할 서버 주소)</li>
<li>Path: /products/1 (API 엔드포인트 경로)</li>
</ul>
</li>
<li>Listener 추가 (결과 확인용):<ul>
<li>Thread Group 우클릭 → Add → Listener → View Results in Table (표로 결과 보기)</li>
<li>Thread Group 우클릭 → Add → Listener → Summary Report (통계 요약 보기)<h3 id="3-테스트-실행-1">3. 테스트 실행</h3>
상단의 초록색 시작 버튼(▶️)을 누르면 테스트가 시작됩니다.<h3 id="4-결과-확인-1">4. 결과 확인</h3>
테스트가 실행되는 동안 추가했던 View Results in Table이나 Summary Report 같은 Listener 탭에서 실시간으로 결과를 확인할 수 있습니다.</li>
</ul>
</li>
<li>Summary Report:<ul>
<li><h1 id="samples-총-요청-수">Samples: 총 요청 수</h1>
</li>
<li>Average: 평균 응답 시간</li>
<li>Throughput: 초당 처리량 (RPS)</li>
<li>Error %: 에러율</li>
</ul>
</li>
</ul>
<h2 id="🤔-어떤-도구를-선택할까요">🤔 어떤 도구를 선택할까요?</h2>
<table>
<thead>
<tr>
<th>특징</th>
<th>k6</th>
<th>JMeter</th>
</tr>
</thead>
<tbody><tr>
<td>작성 방식</td>
<td>JavaScript 코드</td>
<td>GUI</td>
</tr>
<tr>
<td>장점</td>
<td>개발자 친화적, Git으로 버전 관리 용이, 빠르고 가벼움</td>
<td>강력한 기능, 복잡한 시나리오 구성 용이, 비개발자도 사용 가능</td>
</tr>
<tr>
<td>단점</td>
<td>GUI 부재, 학습 곡선이 약간 있음</td>
<td>무겁고 리소스를 많이 사용, 버전 관리가 어려움</td>
</tr>
<tr>
<td>추천 대상</td>
<td>빠르게 API 성능을 확인하고 싶은 개발자, CI/CD 파이프라인에 통합</td>
<td>매우 복잡한 사용자 시나리오(로그인, 쿠키 등)를 테스트해야 하는 QA팀</td>
</tr>
</tbody></table>