<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/b335154e-91f7-4a74-bee0-9cd960bab238/image.JPG" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/4a67b0fe-659e-45a9-a286-eaae8da80b08/image.JPG" /></p>
<p>두 호스트가 링크하나를 공유해서 서버로 데이터를 보내고 있다.</p>
<p>이때 가정은 infinite buffer
output link capacity : R</p>
<p>Iin(밀어넣는 속도), Iout(내보내는 속도)
throughput은 R/2까지는 선형으로 증가하지만
딜레이는 기하급수적으로 증가한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/61ce1f06-c715-4ecf-862b-35067ef8ecec/image.JPG" /></p>
<p>이번에는 finite buffer이기에 packet loss가 발생할 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/30a1f421-fe93-4281-9c64-9d0758432289/image.JPG" /></p>
<p>이때는 공간이 있을때만 보내기 때문에 R/2를 넘지 않을 것이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/356f0cb5-f265-45f0-975f-b506abfe8200/image.JPG" /></p>
<p>패킷 loss가 발생할 수 있는데 내가 그걸 알고 잃어버린 패킷만 다시 보내는 방식이다. 그래서 duplicated packet이 안간다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/34b1feb5-ad28-4880-a874-c71bc39028dc/image.JPG" /></p>
<p>이렇게 된다면 throughput은 R/2가 아닐 수도 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/eedae189-8388-4895-8b99-a855bfc7618a/image.JPG" /></p>
<p>실재로는 duplicated packet을 보낼 수 밖에 없다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/0afcb0b7-b5e8-4289-866e-09e588bea8d6/image.JPG" /></p>
<p>congestion의 댓가는 goodput 에 대한 방법들이 필요함.
재전송이 필요없어질 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/400f9dcb-091f-442d-9c1e-908f0e2795da/image.JPG" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/99e78e01-0690-4149-9448-48bacc4e0fd8/image.JPG" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/48eab16f-4b17-42d9-9b53-f34d7efa6ee1/image.JPG" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/5ad14c69-bf1e-4980-8fe8-22225a52e99e/image.JPG" /></p>
<p>sender는 transmission rate를 증가(윈도우 사이즈를 제어해서 컨트롤한다), 조금씩 올리다가 loss가 오면 줄이는 것이다. =&gt; 이걸로 usable bandwidth를 알아보기</p>
<ul>
<li>additive increase : lose 전까지 cwnd를 1 MSS(Maximum Segment Size)만큼 증가시키기</li>
<li>multiplicative decreate : loss 발생하면 절반으로 줄여버림</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/24e60bfd-eef9-487d-bde4-733e47e9eae7/image.JPG" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/e253b461-3967-4e74-a3b3-afd7cc53679d/image.JPG" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/c4d280b4-0adc-41d7-b69b-434f711f39c6/image.JPG" /></p>
<p>loss가 발생한경우 cwnd를 1 MSS로 바꾸어버리기
ACK 가 중복 3개가 온 경우</p>
<ul>
<li>RENO : cwnd를 절반으로 줄이기, 선형 증가</li>
<li>Tahoe : cwnd를 1로 바꾸고 지수 증가, ssthresh부터는 선형증가</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/a969989b-14b7-4118-a8e6-9e184a91348d/image.JPG" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/196c4055-4ff7-42ff-b015-1940a3095321/image.JPG" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/fd6b5aae-aa79-4206-82a3-91273469877c/image.JPG" /></p>
<p>avg window size가 3/4 <code>*</code> W 정도된다면
avg TCP thruput = 3/4 <code>*</code> W/RTT bytes/sec
될거라고 예상할 수 있다.</p>
<p>congestion avoidance phase가 일정하게 진행</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/734de0c7-f718-47dc-a01f-b602d1004bad/image.JPG" /></p>
<p>segment loss probability에서 throughput을 표현해보면 아래와 같은 공식을 쓰게 된다.</p>
<p>TCP throughput = 1.22 <code>*</code> MSS / (RTT <code>*</code> root(L))</p>
<p>세그먼트 loss probability가 작을 수록 window 사이즈가 더 커질 수 밖에 없는 공식이다.</p>
<p>이것도 AIMD를 가정하고 작성한 공식이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/7c66dd76-c9b0-47d4-86de-2d79c6a59d1c/image.JPG" /></p>
<p>TCP Fairness문제
fairness goal : 같은 bottleneck router을 공유하는 k개의 TCP 세션이 존재할때 각각의 average는 R/K로 가저가야한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/a3eebe30-6f25-443b-ae2b-322da1c40dd0/image.JPG" /></p>
<p>이것도 계속 진행하다보면 위와같이 언제가 loss가 발생하는 시점에서 둘다 절반으로 줄이게 된다.</p>
<p>그러다보면 결국 equal bandwidth share에 도달한다는 것이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/8db80718-075c-4b04-a187-c76d88dc812d/image.JPG" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/32b9e664-a102-4226-9c1c-847980dddd7b/image.JPG" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/60118aa3-2099-462e-94da-05f4b9d91479/image.JPG" /></p>