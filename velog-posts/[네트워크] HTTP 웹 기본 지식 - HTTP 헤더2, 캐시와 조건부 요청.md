<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/2566c0a5-8f22-482b-b0f1-a3f346d6ec83/image.png" /></p>
<p>본 게시글은 인프런의 모든 개발자를 위한 HTTP 웹 기본 지식 (김영한) 강의를 듣고 정리한 내용입니다</p>
<p>웹 성능 최적화는 사용자 경험 향상을 위해 필수적인 과정 중 하나로, 이를 위해 캐시와 조건부 요청은 중요한 역할을 합니다. 이 글에서는 HTTP 헤더를 이용한 캐시 동작과 조건부 요청에 대해 더 자세히 살펴보겠습니다.</p>
<p>캐시: 기본 동작과 필요성
웹 페이지를 불러올 때, 매번 서버에서 모든 리소스를 다운로드하는 것은 비효율적입니다. 캐시는 브라우저가 이전에 받아온 리소스를 저장해두고, 동일한 요청이 발생할 때 다시 서버에 요청하지 않고 캐시된 데이터를 사용함으로써 네트워크 사용을 줄이고 로딩 속도를 높이는 역할을 합니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/1fb1b674-2f37-4030-a148-0293f0b1548b/image.png" /></p>
<p>그러나 캐시된 데이터가 항상 최신 상태를 유지해야 하는 것은 아닙니다. 서버의 데이터가 변경되고 브라우저에 캐시된 데이터가 여전히 유효한 경우, 사용자는 오래된 정보를 보게 됩니다.</p>
<p>캐시가 있을 때의 동작
캐시를 효과적으로 사용하기 위해 서버는 HTTP 헤더를 통해 캐시 제어 정보를 전달합니다. 헤더를 이용하면 캐시 유효 시간을 설정할 수 있습니다.<code>Cache-Control</code></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/c66e7ab8-24bf-46e8-944e-4ebfb07ae8b4/image.png" /></p>
<p>위의 예시에서는 캐시 유효 시간을 60초로 설정하고 있습니다. 브라우저는 이 정보를 활용하여 해당 시간 동안은 서버에 재요청 없이 캐시된 데이터를 사용합니다.</p>
<p>만약 캐시 시간이 만료된다면?</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/146a95dd-4e18-4544-b5cd-db64e27ea7cd/image.png" /></p>
<p>캐시 유효시간이 만료되면, 브라우저는 서버에 재요청하여 데이터를 갱신합니다. 이때, 서버에서 데이터가 변경되었는지 확인하는 데에 검증 헤더와 조건부 요청이 사용됩니다.</p>
<p>검증 헤더와 조건부 요청
캐시 유효시간이 초과된 후 서버에 재요청할 때, 서버는 데이터가 변경되지 않았다면 네트워크 다운로드를 최소화하기 위해 검증 헤더와 조건부 요청을 사용합니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/f4f17fee-2771-4b90-a623-b1430a8d5d3a/image.png" /></p>
<p>웹 브라우저는 이전에 받아온 데이터의 최종 수정일을 헤더로 저장하고, 캐시 만료 후 서버에 재요청 시 이 값을 헤더에 담아 전송합니다. 서버는 이 값을 이용해 데이터가 수정되었는지 확인하고, 수정이 없다면 304 Not Modified 응답을 반환하여 브라우저에게 데이터를 다시 받지 않아도 된다는 신호를 보냅니다. <code>Last-Modifiedif-modified-since</code></p>
<p>이러한 검증 헤더를 통한 조건부 요청은 네트워크 사용을 최소화하며 빠른 로딩을 가능케 합니다.</p>
<p>ETag와 If-None-Match
검증 헤더 중 ETag는 서버가 리소스에 부여한 임의의 고유 버전 이름입니다. 데이터가 변경될 때마다 ETag가 갱신되며, 이를 이용해 브라우저는 서버에 데이터가 변경되었는지 직접 확인합니다.</p>
<table>
<thead>
<tr>
<th><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/66fa42b3-5dd5-4565-bede-5577eeba82cb/image.png" /></th>
<th><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/56e6d806-fc18-42ae-bc44-19f8cd9d99fd/image.png" /></th>
</tr>
</thead>
</table>
<p>Accept-Language 적용 전    Accept-Language 적용 후
서버는 이전 응답에 포함된 ETag 값을 헤더로 받아와 사용하고, 데이터가 변경되지 않았다면 304 Not Modified 응답을 반환하여 브라우저에게 데이터를 재전송하지 않아도 된다는 신호를 보냅니다.if-none-match</p>
<p>ETag와 If-None-Match는 캐시 제어 로직을 서버에서 완전히 분리할 수 있게 하며, 클라이언트는 캐시 로직에 대해 몰라도 됩니다.</p>
<p>캐시 제어 헤더
캐시와 관련된 중요한 헤더들이 있습니다.</p>
<p>캐시 제어
Cache-Control 헤더는 캐시 제어에 가장 중요한 영향을 미치는 헤더입니다.</p>
<p>max-age: 캐시 유효시간을 초 단위로 나타냅니다.
no-cache: 데이터는 캐시해도 되지만, 항상 서버에 검증하고 사용해야 합니다.
no-store: 데이터를 저장하면 안되며, 메모리에서만 빠르게 사용하고 삭제해야 합니다.
프라그마
Pragma 헤더는 HTTP 1.0에서 사용되던 캐시 제어 헤더로, 현재는 거의 사용되지 않습니다. 지시어를 포함할 수 있습니다.no-cache</p>
<p>만료
Expires 헤더는 캐시 만료일을 지정하는데 사용됩니다. 초 단위가 아닌 정확한 날짜와 시간을 사용하며, 보다 낡은 형식입니다.max-age</p>
<p>프록시 캐시
프록시 캐시는 실제 데이터가 있는 서버를 원 서버라고 부르며, 중간에 위치한 프록시 캐시 서버를 통해 원 서버로부터 받은 리소스를 저장해둡니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/3644208c-5ed4-4316-af6a-2d7a7d637566/image.png" /></p>
<p>프록시 캐시는 캐시와 캐시로 나뉩니다. private 캐시는 개별 사용자 브라우저에만 저장되며, public 캐시는 중간에 공용으로 사용하는 프록시 캐시 서버에 저장됩니다.privatepublic</p>
<p>캐시 무효화
캐시가 항상 최신 상태를 유지해야 하는 경우, 캐시 무효화를 위한 헤더를 사용할 수 있습니다. 몇 가지 주요한 캐시 무효화 헤더는 다음과 같습니다.</p>
<p>Cache-Control: no-cache - 데이터는 캐시해도 되지만, 항상 원 서버에 검증하고 사용해야 합니다.
Cache-Control: no-store - 아예 캐시 되면 안될 때 사용합니다. (민감한 데이터 메모리에서만 사용하고 빨리 삭제)
Cache-Control: must-revalidate - 캐시 만료 후 최초 조회시 원 서버에 검증해야 합니다. 원 서버 접근 실패시 반드시 오류 발생 하며 (504 gateway timeout), 캐시 유효 시간이라면 캐시를 사용합니다.
Pragma: no-cache - HTTP 1.0 하위 호환 방식으로, 지금은 거의 사용되지 않습니다.
이러한 헤더를 사용하여 브라우저는 데이터를 항상 서버에 검증하고 사용하게 됩니다.</p>
<p>마무리
HTTP 캐시와 조건부 요청은 웹 성능 최적화에서 중요한 역할을 합니다. 올바른 캐시 전략과 조건부 요청을 통해 네트워크 사용을 최소화하고 빠른 로딩을 실현할 수 있습니다. 특히 캐시 제어 헤더와 프록시 캐시를 효과적으로 활용하면 사용자 경험을 향상시킬 수 있습니다.</p>