<p>useCallback과 useMemo는 불필요한 연산과 렌더링을 방지하여 React 애플리케이션의 성능을 최적화하는 것이 가장 큰 장점입니다.</p>
<h2 id="usecallback-함수를-재사용한다">useCallback: 함수를 재사용한다</h2>
<p>useCallback은 특정 함수를 메모리에 저장해두고(메모이제이션), 의존성 배열(deps)의 값이 변경되지 않는 한 이전에 생성된 함수를 계속해서 재사용합니다.</p>
<ul>
<li>장점: 자식 컴포넌트에 prop으로 함수를 전달할 때, 부모가 리렌더링되어도 함수가 재생성되지 않습니다. 이로 인해 React.memo로 최적화된 자식 컴포넌트의 불필요한 리렌더링을 막을 수 있습니다.
const handleLogin = useCallback(() =&gt; {
// 로그인 관련 로직
}, []); // 의존성이 없으므로 이 함수는 최초 1번만 생성됨</li>
</ul>
<h2 id="usememo-값을-재사용한다">useMemo: 값을 재사용한다</h2>
<p>useMemo는 복잡한 연산의 결과값을 메모리에 저장해두고, 의존성 배열(deps)의 값이 변경되지 않는 한 저장된 값을 재사용합니다.</p>
<ul>
<li>장점: 매 렌더링마다 반복될 필요 없는 무거운 계산(예: 큰 배열 필터링, 복잡한 데이터 가공)을 건너뛸 수 있어 렌더링 속도를 향상시킵니다.
const processedData = useMemo(() =&gt; {
return largeArray.filter(item =&gt; item.id &gt; 100);
}, [largeArray]); // largeArray가 변경될 때만 이 연산을 수행함</li>
</ul>
<h2 id="핵심-요약-🔑">핵심 요약 🔑</h2>
<ul>
<li><strong>useCallback</strong>은 함수 자체를 기억해서 불필요한 함수 생성을 막습니다.</li>
<li><strong>useMemo</strong>는 함수의 결과값을 기억해서 불필요한 연산을 막습니다.
두 훅 모두 무분별하게 사용하면 오히려 메모리 소비를 늘릴 수 있으므로, 성능 저하가 실제로 발생하는 구간에 전략적으로 사용하는 것이 중요합니다.
이 두 훅의 차이점에 대해 더 자세한 코드 예제를 보여드릴까요?</li>
</ul>