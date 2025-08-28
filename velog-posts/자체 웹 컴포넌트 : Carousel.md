<p>네, Next.js 기반의 Headless 웹 컴포넌트 라이브러리에 포함될 Carousel 기능 정의서를 작성해 드릴게요. Radix와 Shadcn의 철학을 반영하여, 조합(Composition)을 통해 유연성과 확장성을 극대화하는 방향으로 정의했습니다.
🎠 Carousel Component 기능 정의서
이 문서는 내부 NPM 라이브러리로 제공될 Carousel 컴포넌트의 기능과 명세를 정의합니다. Headless를 지향하여 로직과 상태 관리에 집중하며, UI는 사용자가 자유롭게 커스터마이징할 수 있도록 설계합니다.</p>
<h2 id="1-ui-설명">1. UI 설명</h2>
<p><strong>캐러셀(Carousel)</strong>은 한정된 공간 안에 여러 개의 콘텐츠(이미지, 카드 등)를 순환하며 보여주는 UI 컴포넌트입니다. 사용자는 좌우(또는 상하) 탐색 버튼, 하단 인디케이터, 또는 직접적인 스와이프/드래그 동작을 통해 콘텐츠를 탐색할 수 있습니다.
주요 기능:</p>
<ul>
<li>수평 및 수직 스크롤 방향 지원</li>
<li>무한 루프(Loop) 기능</li>
<li>자동 재생(Autoplay) 및 상호작용 시 일시 정지 기능</li>
<li>버튼, 인디케이터 등 탐색 요소 커스터마이징</li>
<li>터치 및 드래그 스크롤 지원</li>
<li>WAI-ARIA 표준을 준수한 웹 접근성<h2 id="2-컴포넌트-구조-composition">2. 컴포넌트 구조 (Composition)</h2>
Shadcn/UI와 같이 단일 컴포넌트가 아닌, 여러 개의 컴포넌트를 조합하여 캐러셀을 완성하는 Compound Component Pattern을 따릅니다. 이를 통해 높은 자유도와 시맨틱한 마크업 구조를 보장합니다.
import {
Carousel,
CarouselContent,
CarouselItem,
CarouselNextButton,
CarouselPrevButton,
CarouselIndicators,
CarouselIndicatorItem
} from '@/components/ui/carousel';</li>
</ul>
<p>function MyCarousel() {
  return (
    &lt;Carousel
      orientation=&quot;horizontal&quot;
      options={{ loop: true }}
      autoplayDelay={3000}
      onSlideChange={(index) =&gt; console.log(<code>Current Slide: ${index}</code>)}
    &gt;
      
        ...
        ...
        ...
      
      
      
      
        
        
        
      
    
  );
}</p>
<ul>
<li>Carousel: 모든 상태와 로직을 관리하는 최상위 컨테이너 (Provider 역할)</li>
<li>CarouselContent: 슬라이드 아이템들을 감싸는 스크롤 영역</li>
<li>CarouselItem: 개별 슬라이드 아이템</li>
<li>CarouselNextButton, CarouselPrevButton: 탐색 버튼</li>
<li>CarouselIndicators: 인디케이터(점)들을 감싸는 컨테이너</li>
<li>CarouselIndicatorItem: 개별 인디케이터(점)<h2 id="3-props-정의">3. Props 정의</h2>
Props는 주로 최상위  컴포넌트에 전달하여 전체 동작을 제어합니다.</li>
</ul>
<table>
<thead>
<tr>
<th>Prop 이름</th>
<th>타입</th>
<th>필수 여부</th>
<th>설명</th>
<th>DefaultValue</th>
<th>사용자 인터랙션 유즈케이스</th>
</tr>
</thead>
<tbody><tr>
<td>orientation</td>
<td>'horizontal'</td>
<td>'vertical'</td>
<td>아님</td>
<td>캐러셀의 스크롤 방향을 설정합니다.</td>
<td>'horizontal'</td>
</tr>
<tr>
<td>options</td>
<td>object</td>
<td>아님</td>
<td>Embla Carousel (내부 로직 라이브러리)의 세부 옵션을 설정합니다.</td>
<td>{}</td>
<td>{ align: 'center', loop: true, slidesToScroll: 2 } 와 같이 중앙 정렬, 무한 루프, 2칸씩 스크롤 등을 설정할 때 사용합니다.</td>
</tr>
<tr>
<td>autoplayDelay</td>
<td>number</td>
<td>아님</td>
<td>자동 재생 딜레이 시간(ms)을 설정합니다. 0 또는 undefined일 경우 비활성화됩니다.</td>
<td>undefined</td>
<td>3000으로 설정 시, 3초마다 자동으로 다음 슬라이드로 넘어가는 배너를 만듭니다.</td>
</tr>
<tr>
<td>stopAutoplayOnInteraction</td>
<td>boolean</td>
<td>아님</td>
<td>사용자가 캐러셀과 상호작용(클릭, 드래그 등)할 때 자동 재생을 멈출지 여부를 결정합니다.</td>
<td>true</td>
<td>false로 설정하면, 사용자가 버튼을 눌러도 자동 재생 타이머가 초기화되고 계속 진행됩니다.</td>
</tr>
<tr>
<td>initialIndex</td>
<td>number</td>
<td>아님</td>
<td>캐러셀이 처음 렌더링될 때 보여줄 슬라이드의 인덱스를 설정합니다.</td>
<td>0</td>
<td>특정 상품 상세 페이지에서 해당 상품이 포함된 캐러셀을 보여줄 때, 그 상품부터 시작하게 합니다.</td>
</tr>
<tr>
<td>className</td>
<td>string</td>
<td>아님</td>
<td>컴포넌트의 최상위 요소에 적용할 CSS 클래스를 추가합니다.</td>
<td>undefined</td>
<td>Tailwind CSS 등을 사용하여 w-full max-w-lg 와 같이 컴포넌트의 스타일을 지정합니다.</td>
</tr>
<tr>
<td>asChild</td>
<td>boolean</td>
<td>아님</td>
<td>자식 요소에 Props를 전달하고 렌더링을 위임합니다. (Radix의 Slot 기능)</td>
<td>false</td>
<td>CarouselNextButton 안에 커스텀 아이콘이 포함된 <button>을 직접 넣어 스타일링할 때 사용합니다.</td>
</tr>
</tbody></table>
<h2 id="4-이벤트-events-정의">4. 이벤트 (Events) 정의</h2>
<p>이벤트 역시 최상위  컴포넌트에 콜백 함수 형태로 전달합니다.</p>
<table>
<thead>
<tr>
<th>이벤트 이름</th>
<th>타입</th>
<th>필수 여부</th>
<th>설명</th>
<th>DefaultValue</th>
<th>유즈케이스</th>
</tr>
</thead>
<tbody><tr>
<td>onSlideChange</td>
<td>(index: number) =&gt; void</td>
<td>아님</td>
<td>슬라이드 전환이 완료된 후 호출되는 콜백 함수입니다. 현재 활성화된 슬라이드의 인덱스를 인자로 받습니다.</td>
<td>undefined</td>
<td>- &quot;3 / 10&quot; 과 같이 현재 슬라이드 번호를 UI에 표시합니다.<br />- 특정 슬라이드가 보였을 때 Google Analytics 등으로 이벤트를 전송합니다.</td>
</tr>
<tr>
<td>onInteraction</td>
<td>(type: 'drag'</td>
<td>'click') =&gt; void</td>
<td>아님</td>
<td>사용자가 캐러셀과 상호작용(드래그 시작, 버튼 클릭 등)을 시작할 때 호출됩니다.</td>
<td>undefined</td>
</tr>
<tr>
<td>onInit</td>
<td>(api: CarouselApi) =&gt; void</td>
<td>아님</td>
<td>캐러셀이 초기화된 직후 한 번 호출됩니다. 캐러셀을 제어할 수 있는 API 객체를 인자로 받습니다.</td>
<td>undefined</td>
<td>외부 버튼 클릭 시 api.scrollTo(3) 와 같이 캐러셀을 프로그래밍 방식으로 제어해야 할 때 API 객체를 저장해두고 사용합니다.</td>
</tr>
<tr>
<td>onResize</td>
<td>() =&gt; void</td>
<td>아님</td>
<td>브라우저 창 크기가 변경되어 캐러셀의 크기가 재계산될 때 호출됩니다.</td>
<td>undefined</td>
<td>반응형 디자인에서 캐러셀 크기 변경에 따라 특정 레이아웃을 다시 계산해야 할 경우 사용합니다.</td>
</tr>
</tbody></table>