<h1 id="link-layer">Link layer</h1>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/768d1f95-7e91-4ee0-9fb7-f4e489ad1d93/image.png" /></p>
<p>host, router = node
이웃한 노드를 연결하는 것을 link</p>
<p>layer-2 packet : frame</p>
<p>link-layer는 물리적으로 직접연결된 reliable transfer을 책임진다.</p>
<p>각각의 링크들에서 잘 전달되는지</p>
<h2 id="link-layer-context">link layer: context</h2>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/e5dcd41e-e263-4935-af6f-2e3dd194e68a/image.png" /></p>
<p>어떤 데이터가 n to n으로 지날때 서로 다른 링크를 지날 수 있다.</p>
<p>각각의 링크 레이어 프로토콜은 다른 서비스를 이용한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/2e26bd29-d0c1-4f7c-a76c-5654b70565a7/image.png" /></p>
<p>framing : 데이터그램을 frame으로 encapsulation 하는 것이다. shared meduim이면 channel access control도 link layer이 결정한다.
MAC 주소도 이용해서 src, dest를 구분한다.</p>
<p>인접 노드사이의 data delivery를 책임진다. 에러를 확인하고 에러를 고치는 것이 link layer에 들어가 있다.</p>
<p>bit-error가 거의 일어나지 않는 fiber(광케이블), twisted pair에서는 거의 사용되지 않는다.</p>
<p>질문은 왜 link-level과 end-end reliability가 필요한가?</p>
<ul>
<li>link layer는 전달만해준다. 그럼 queing 이 일어날텐데 패킷 드랍이 link layer 문제가 아니기 때문에 n to n reliability가 필요해진 것이다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/30b2ed58-e336-46b1-ac38-452e4b9ab067/image.png" /></p>
<ul>
<li>flow control</li>
<li>error detection</li>
<li>error correction</li>
<li>half-duplex and full-duplex</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/2707cc88-2152-4af3-ba15-1b415502e8ea/image.png" /></p>
<p>link layer는 NIC에 구현되어 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/c6a779a7-f8c5-4288-b929-7aa12cce6539/image.png" /></p>
<p>LAN 카드가 받은 프레임을 전달하고 receiving host에서 헤더를 제거하고 데이터만 받게 된다.</p>
<h1 id="62-error-detection-correction">6.2 error detection, correction</h1>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/2665eee0-400a-4b5e-ad2d-aa57c8d1401f/image.png" /></p>
<p>EDC = error detection and correction bits
D = data protected by error checking</p>
<p>에러는 100% 믿을만 하지 않다. 100% detection 하는 것은 아니다.</p>
<p>EDC field가 크면 detection, correction을 보다 잘할 수 있지만 over head가 크다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/10160ddd-76fa-4d9b-89d4-3bb4c3f829b5/image.png" /></p>
<p>single bit parity는 한 비티를 검사하는 것이다.
single bit parity는 odd parity check와 even parity check가 존재한다.</p>
<p>odd면 1의 갯수가 홀수가 되도록 채워넣는 것이다.</p>
<p>한 비트만 에러 났으면 detect 가능하지만 두 비트가 났으면 불가능하다.</p>
<p>이 차원 비트 패리티에서는 row parity, column parity로 2차원으로 처리해버리는 것이다.</p>
<p>문제능 이렇게 하더라도 어디에서 에러가 났는지는 모른다. 그리고 overhead가 크다는 단점이 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/faa04367-89a1-48d2-8c07-dc90e5535d19/image.png" /></p>
<p>인터넷 체크썸</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/244c7576-ba3d-4052-a442-882fcb8ddf0a/image.png" /></p>
<p>CRC
data bit = D, binary number
G = r + 1
목표 : r개의 CRC bit = R을 &lt;D, R&gt;</p>
<ol start="2">
<li>CRC</li>
<li>multiple access protocols - p2p, broadcast, MAC protocols(taxonomy), TDMA, FDMA, ALOHA, CSMA, CSMA/CA, CSMA/CD</li>
<li>ARP, ethernet, switches, vlan</li>
<li>MPLS</li>
<li>data center networking</li>
<li></li>
</ol>