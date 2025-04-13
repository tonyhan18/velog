<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/a4209c82-f7ee-4e58-ac22-c3fa674d15be/image.png" /></p>
<h1 id="link-state">link state</h1>
<p>다익스트라 알고리즘</p>
<p>• Input
– A graph with edge weights (distance) : 그래프와 엣지 그리고 distance</p>
<p>• Output
– Shortest paths from one node to all others : 어떤 노드에서부터 다른 노드까지 shortest path를 계산</p>
<p>Dijkstra algorithm
<img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/ab6ab8f6-c1b6-43c5-8b9e-7f306a80caee/image.png" /></p>
<p>Dijkstra algorithm</p>
<ul>
<li>소스가 되는 노드를 집합에 넣고 시작한다.</li>
<li>N-1번 루프를 돈다.</li>
<li>각 경로에서 최단경로와 거치어서 가는 경로중 보다 더 최단 경로인것을 선택한다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/c41be69e-2b8f-4b09-8ccf-38fa7703b647/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/e0104499-2cbc-4168-8c14-fc58fbeb4c9c/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/8d60edd4-4368-490c-b26e-aaa90c55b8d1/image.png" /></p>
<p>다익스트라 알고리즘의 문제점은 oscillation 문제가 있다.</p>
<h1 id="distance-vector">distance vector</h1>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/c1c2aa25-d6e4-4e73-bca8-84a4fbd83bf8/image.png" />
벨만 포드 알고리즘.
<img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/dabdf8ca-bc06-44d4-b4e5-cee4d11bb522/image.png" /></p>
<p>벨만 포드 방정식은 위의 것을 풀려고 한다.
<img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/d67ebb26-3b42-4638-b1ae-f819d18a653a/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/0f593634-7a80-4716-ad7e-6956aa0a31dd/image.png" /></p>
<p>X에서 Y로 가는  cost를 소유.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/8637fafe-c68c-44a3-9d8a-de01d3297199/image.png" /></p>
<p>이웃이 업데이트 되면 정보를 업데이트를 하고 주변도 업데이트 해주고</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/5322d45d-eec5-4509-8eb3-6bc4f3ac4169/image.png" /></p>
<p>각각의 노드가 이웃들에게 자기의 distance vector을 보낸다. 그럼 x는 처음에 정보가 없다가 업데이트 하게 된다.</p>
<p>x에서 y로 가는 호스트는 x-&gt;y-&gt;y, x-&gt;z-&gt;y 두개를 모두 계산한다.
x-&gt;z-&gt;z, x-&gt;y-&gt;z 를 모두 계산한다.
<img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/2dc8406a-c38b-40a3-8bce-e90ea430fddc/image.png" /></p>
<p>똑같이 모두 업데이트 해준다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/23b47a02-55e8-4e77-85ce-e0206376c314/image.png" />
<img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/ecbabd6f-af21-48c2-8723-34792a8eb976/image.png" /></p>
<p>그러다가 링크 코스트가 바뀌었다고 하자. 한쪽이 너무 커지면 무한 iteration 하게 될 수도 있다.</p>
<p>결국 라우팅에 loop가 생기는 문제점이 있는 것이다.</p>
<p>그래서 이를 해결하기 위해 바뀐 경로에 대해 무한대로 표시해버리는 것이다. 그러면 더 이상의 반복이 일어나지 않을 것이다.</p>
<hr />
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/4e90e146-7853-428c-ad65-94e136cf799b/image.png" /></p>
<p>두개를 비교해보면
LS : O(nE)
DV : 이웃과 테이블을 교환하기 때문에 상황에 따라 달라질 수 있다.</p>
<p>수렴속도
LS : O(n^2)
DV : 바뀔 수 있다.</p>
<p>robustness
LS : 
DV : </p>
<hr />
<h1 id="53-intra-as-routing-in-the-internet-ospf">5.3 intra-AS routing in the Internet: OSPF</h1>
<p>네트워크 전체를 계층적으로 본다. 네트워크들은 서브넷으로 구성되어 있다. 그래서 서브넷 안에서 라우팅하거나 서브넷 끼리 라우팅된다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/029863a4-aec4-4233-be67-a3c5b4b44b1c/image.png" /></p>
<p>intra-AS routing : ISP 안에서 라우팅</p>
<ul>
<li>하나의 AS에서는 같은 라우팅 프로토콜을 돌리어야 한다.</li>
<li>다른 AS 간에는 다른 라우팅 프로토콜 돌리어도 된다.</li>
<li>게이트웨이 라우터는 다른 AS와 연결된 edge에 있는 라우터를 게이트웨이 라우터라고 부른다.</li>
</ul>
<p>inter-AS routing : ISP 간의 라우팅</p>
<ul>
<li>AS 들 간의 라우팅</li>
<li>게이트웨이가 inter 도메인간의 라우팅 주도</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/722bea5d-3374-4859-a389-868269859701/image.png" /></p>
<p>각각의 라우터에 forwarding table이 만들어질텐데 이건 intra-AS와 inter-AS 두개를 이용해서 결정이 되어진다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/97aee629-fc58-4bf3-835d-3e6d6f9dd810/image.png" /></p>
<p>inter-AS가 하는일</p>
<p>AS1에서는 1b, 1c가 누구와 연결할지를 결정한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/4bb8c98c-20b8-4d8c-82ae-ba5af3f1b8ba/image.png" />
intra-AS routing == IGP
RIP, OSPF, IGRP</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/0989acdb-5277-4669-9be5-498dc61fec02/image.png" />
OSPF(Open, link-state, dijkstra algorithm)</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/7fc4a669-8955-44e3-90d6-3f3e373bc946/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/e42b10bc-b688-4d4c-94e5-a79aa3984817/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/51f3f6d7-20f9-4178-b74a-7015b64e00c3/image.png" />
link-state는 area 안에서만, 각 노드는 area topology를 가지고 있다. 다른 area에 있는 것들은 direction만 알고 있다.
area border routers : 자기 area를 요약해서 다른 지역에 보낸다.
backbone router : 백본에서만 돌아가는 OSPF를 돌린다.
boundary routers는 다른 AS와 연결되는 것을 의미</p>
<h1 id="54-routing-among-the-isps-bgp">5.4 routing among the ISPs BGP</h1>
<p>ISP 간의 라우팅 알고리즘</p>
<p>BGP = inter-domain routing protocol</p>
<ul>
<li>eBGP = 이웃한 AS로 부터 reachability information 받기</li>
<li>iBGP = AS 안에서 internal routers로 부터 reachability information을 받는다.</li>
</ul>
<p>좋은 경로는 reachability information와 policy에 의해서 결정된다.
<img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/3a1a7e68-f298-475b-954f-99a3863ca883/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/78fddb87-882e-42b7-8fe3-7ae1a6787786/image.png" /></p>
<p>BGP sesstion은 TCP 연결이 열리어 있어서 reachability information을 계속 주고 받는다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/d330c229-ad00-4e6d-bc66-c8e25d9dd669/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/3f81b59a-2ac7-4b0f-a566-963f99302677/image.png" /></p>
<p>AS-PATH
NEXT-HOP</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/6d8aec64-09e6-4877-b52f-178cbb5275f0/image.png" /></p>
<p>AS3,X를 먼저 보내고 이 정보들이 iBGP에 의해 뿌려지고
AS1에게는 AS2,AS3,X정보가 통과된다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/ae3b0339-6d68-4154-ac8d-8b5708672eca/image.png" />
network policy에 의해서 하나만 선택해서 보낼 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/290c47c3-03e6-4a6e-9b76-8fbdb4cca859/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/c9cedace-c216-4e0f-b40d-371fb335f907/image.png" />
forwarding table</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/2ce8f848-78cb-4262-8d91-db84bd0be362/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/0ce0d80b-6eeb-43c2-bb66-1b4e667156bc/image.png" />
BGP에서 경로 선택은</p>
<ol>
<li>policy</li>
<li>AS-PATH</li>
<li>NEXT-HOP router</li>
<li>추가적인 기준</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/d2c81e2c-68e9-452f-a90a-e63735b2db79/image.png" /></p>
<p>Hot Potato Routing은 가장 빨리 나를 빠져나갈 수 있는 놈으로 선택해준다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/75adf0d9-0276-412f-b74c-4f600bf167ba/image.png" /></p>
<p>A가 B와 C한테 Aw를 홍보했다. 즉 w는 A를 통해 forwarding 된다.
BAw를 C에게 광고한다.
C는 w로 가는 트래픽을 CAw로 forwarding 한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/40701e06-d8c6-4057-a2d5-0147e4411527/image.png" /></p>
<p>정책을 만들어서 패킷 포워딩을 막을 수도 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/513c0879-a210-4f6b-8b48-2920b2e88bd9/image.png" /></p>
<p>전체 그림을 보면 계층적으로 라우팅이 되어 있다.</p>
<h1 id="55-the-sdn-control-plane">5.5 The SDN control plane</h1>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/d0a88ad0-512a-4d07-8a9f-6d98ef05ae6e/image.png" /></p>
<p>네트워크의 router에 구현이 되어 있는 control plane이 업데이트하기 아주 까다로운 형태. 라우터가 스위칭 하드웨어하고 internet standard인(IP, RIP, IS-IS, OSPF, BGP) 프로토콜들.</p>
<p>인터넷에서 아무리 좋은 알고리즘이 나와도 라우터를 업데이트하기 어려웠다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/6c49c703-7237-41cd-8ab6-592c25ef5463/image.png" /></p>
<p>새로운 라우팅 프로토콜을 적응하려면 이게 쉽지 않았다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/467fe6c7-02cd-464c-8b0e-acd1adbef73f/image.png" /></p>
<p>SDN에서는 logically centralized control plane이 있어서 얘가 전체를 다 계산해서 각각의 라우터들에 업데이트를 해준다. 그래서 control plane이 centralized 된 형태이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/116e90ce-118a-4223-9658-36e26d0b8e26/image.png" /></p>
<p>왜 logically centralized control plane을 선택 하는가</p>
<ul>
<li>nertwork management가 쉽다(avoid router misconfigurations, greater flexibility of traffic flows)</li>
<li>table-based forwarding allows programming routers</li>
<li>open implementation of control plane</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/bf8a9276-e94e-463c-8da2-d9c07ea02e9a/image.png" /></p>
<p>SDN이 되면 위와같은 topology에서 </p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/5332ede3-ab0b-46cd-8dd0-49fa0f568956/image.png" /></p>
<p>traditional routing은 힘들다가 결론임</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/d36d6473-4bd8-4ce6-973b-408f0c300a84/image.png" /></p>
<p>왜냐하면 그때그때 spliting이 힘들기 때문이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/b15b9b25-3e99-495a-9f92-7f018beee1b4/image.png" />
destination forwarding에서는 불가능하지만 SDN에서는 가능하다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/2f686919-bb13-483b-b8fa-dff3d4847c1a/image.png" /></p>
<p>핵심은 generalized forwarding, programmable 이다.</p>
<p>그리고 control과 data plane을 완전히 분리시킨다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/b17be464-39e6-466a-9cd3-d2628259ef2a/image.png" /></p>
<p>data plane switch는 하드웨어라고 보면 된다. fast, simple, commodity이고 generalized data-plane을 구현한 것이다.</p>
<p>flow talbe은 centralized controller에 의해서 관리 반영된다.</p>
<p>table-based switch control을 위한 API를 제공한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/1a085f8f-bcae-4883-ae7a-06c38207f86b/image.png" /></p>
<p>SDN controller는 network OS이다. 하드웨어와 소프트웨어를 연결하는 네트워크 OS이다. network state information을 가지고 API와 하드웨어를 연결해주어 interaction 해준다.</p>
<p>performance, scalability, fault-tolerance, robustness를 통해 분산화된 시스템을 구현한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/efb75068-5cf3-4534-baca-cbe07e5829bb/image.png" /></p>
<p>서드 파티에 의해서 새로운 서비스가 나올 수 있다. </p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/5859781a-09f8-4897-b2d9-2778cc33dc02/image.png" /></p>
<p>SDN 컨트롤러는 위와같이 생기었다.</p>
<p>openflow는 data plane과 control plane을 연결해준다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/adfa3710-1fa7-4b49-85b9-3b145663a6e2/image.png" /></p>
<p>openflow는 컨트롤러와 스위치 사이에 컨트롤 정보나 스위치의 상태등을 컨트롤러로 보낼때 사용하게 된다. TCP, encryption을 사용할 수 있고</p>
<p>3가지로 사용가능하다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/f6615be6-b2dd-4299-ab87-2e40fc6929ae/image.png" /></p>
<p>controller과 switch간의 연결과 통신을 어떻게 하는지.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/b9e0adf7-a204-4bc8-bebc-f03469ed3d84/image.png" /></p>
<ol>
<li><p>스위치가 link failure를 겪고 있을때 </p>
</li>
<li><p>s1은 openflow를 이용해서 포트의 상태를 controller에 알려준다.</p>
</li>
<li><p>SDN 컨트롤러가 그 정보를 받고 link-state info 업데이트</p>
</li>
<li><p>다익스트라 link-state 라우팅 알고리즘에게 정보를 알려준다.</p>
</li>
<li><p>다익스트라 알고리즘은 link-state info를 통해 바뀐 그래프를 받게 되고 새로운 경로를 계산해서 보내게 된다.
<img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/5ad7e759-256e-4403-9775-b8f3cbd4b60e/image.png" /></p>
</li>
<li><p>link state routing app이 flow-table-computation으로 경로를 계산해서 openflow를 이용해서 내려보낸다.</p>
</li>
<li><p>그리고 업데이트 된다.</p>
</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/47306a86-c5ad-42da-8b7f-1f50111556a8/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/e3e05c55-9d75-4400-9a71-f991988ee3eb/image.png" /></p>
<p>SDN이 얼마나 잘 구현될지는 모르지만 계속 이쪽으로 개발이 진행되고 있다.</p>
<p>failure에 얼마나 강인하게 반응할 것인지? logically centralized 이지만 여러개의 서버들에 컨트롤러가 구현되어 있다. robustness라던지 seculity 문제등</p>
<p>SDN을 통해서 real-time, ultra-reliable, ultra-secure 등의 문제를 해결하려고 한다.</p>
<h1 id="56-icmp--internet-control-message-protocol">5.6 ICMP : Internet control message protocol</h1>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/62c5bfee-4d90-4177-a24f-45d8b5523fd1/image.png" /></p>
<p>icmp는 호스트와 라우터간의 error reporting. 호스트에 도달할 수 없다 등.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/c4212a32-7005-4799-a677-ce3ede4a40a2/image.png" /></p>
<p>3 probes를 보내서 RTT를 측정하는 등</p>
<h1 id="57-network-management-and-snmp">5.7 Network Management and SNMP</h1>
<p>network management는 autonomous system이라면 수천 ~ 수백 네트워크/하드웨어 컴포넌트로 구성되어 있다.</p>
<p>network management라는 것은 하드웨어/소프트웨어가 네트워크 리소스들을 관리하기 위해 설치, 통합, 관리하는 것을 이야기 한다.</p>
<p>network management를 하려면 상태 정보를 모아야 한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/0033b80a-2c7d-4afa-802c-ee14b32473db/image.png" /></p>
<p>관리대상이 되는 agent가 되고 managing entity가 되고 제어 정보가 될 수 있다.</p>
<p>MIB(Management Information Base)에 정보가 모두 모아진다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/c12e097c-62b4-4dd6-b03a-4fb585e8c77c/image.png" /></p>
<p>request를 보내면 response를 전달해주고 trap msg는 request 안해도 보내주는 메시지이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/a9d1c895-b8c8-4ac1-8433-c25fc7149c0a/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/deb8ac88-4d71-491b-b181-3d31736c56c1/image.png" /></p>
<p>뭐 이런게 있구나</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/b3f2ad54-b7ba-4455-a489-2bb3ca2bcce1/image.png" /></p>
<p>네트워크 레이어를 데이터 플레인(하드웨어)과 컨트롤 플레인(소프트웨어)으로 나누어 볼 수 있다.</p>