<p>네, React의 useCallback 훅은 <strong>함수를 재사용(메모이제이션)</strong>하기 위해 사용됩니다. 주로 자식 컴포넌트의 불필요한 리렌더링을 방지하여 성능을 최적화할 때 React.memo와 함께 쓰입니다.</p>
<h2 id="왜-usecallback이-필요한가요-문제점-🔄">왜 useCallback이 필요한가요? (문제점) 🔄</h2>
<p>React의 함수 컴포넌트는 렌더링될 때마다 내부에 선언된 함수들이 새롭게 생성됩니다.
문제 상황:</p>
<ul>
<li>부모 컴포넌트가 리렌더링됩니다.</li>
<li>부모 안에 있던 함수가 새로운 함수로 다시 만들어집니다. (내용은 같지만 메모리 주소는 다름)</li>
<li>이 함수를 prop으로 받는 자식 컴포넌트는 React.memo로 감싸져 있더라도, &quot;새로운 함수가 들어왔네!&quot;라고 인식하여 불필요하게 리렌더링됩니다.
예시 코드 (문제 상황)
import React, { useState } from 'react';</li>
</ul>
<p>// React.memo: props가 변경되지 않으면 리렌더링을 건너뜀
const ChildComponent = React.memo(({ onClick }: { onClick: () =&gt; void }) =&gt; {
  console.log(&quot;자식 컴포넌트가 렌더링되었습니다!&quot;);
  return <button>Click me</button>;
});</p>
<p>function ParentComponent() {
  const [count, setCount] = useState(0);</p>
<p>  // ParentComponent가 리렌더링될 때마다 이 함수는 새로 생성됩니다.
  const handleClick = () =&gt; {
    console.log(&quot;버튼 클릭!&quot;);
  };</p>
<p>  return (
    <div>
      &lt;button onClick={() =&gt; setCount(count + 1)}&gt;
        부모 리렌더링 시키기: {count}
      </button>
      {/* 새로운 handleClick 함수가 전달되어 자식이 계속 리렌더링됩니다. */}
      
    </div>
  );
}</p>
<p>위 코드에서 &quot;부모 리렌더링 시키기&quot; 버튼을 누르면, 콘솔에 &quot;자식 컴포넌트가 렌더링되었습니다!&quot;가 계속 찍히는 것을 볼 수 있습니다.</p>
<h2 id="사용법-usecallback으로-함수-감싸기-✅">사용법: useCallback으로 함수 감싸기 ✅</h2>
<p>useCallback은 함수와 의존성 배열을 인자로 받습니다. 의존성 배열의 값이 변경될 때만 함수를 새로 생성하고, 그렇지 않으면 이전에 생성했던 함수를 그대로 반환합니다.
useCallback(콜백_함수, [의존성_배열]);
예시 코드 (해결)
import React, { useState, useCallback } from 'react';</p>
<p>const ChildComponent = React.memo(({ onClick }: { onClick: () =&gt; void }) =&gt; {
  console.log(&quot;자식 컴포넌트가 렌더링되었습니다!&quot;);
  return <button>Click me</button>;
});</p>
<p>function ParentComponent() {
  const [count, setCount] = useState(0);</p>
<p>  // useCallback으로 함수를 감싸줍니다.
  // 의존성 배열이 비어 있으므로, 이 함수는 최초 렌더링 시 1번만 생성됩니다.
  const handleClick = useCallback(() =&gt; {
    console.log(&quot;버튼 클릭!&quot;);
  }, []);</p>
<p>  return (
    <div>
      &lt;button onClick={() =&gt; setCount(count + 1)}&gt;
        부모 리렌더링 시키기: {count}
      </button>
      {/* 리렌더링 되어도 동일한 함수가 전달되므로 자식은 리렌더링되지 않습니다. */}
      
    </div>
  );
}</p>
<p>이제 &quot;부모 리렌더링 시키기&quot; 버튼을 눌러도, 자식 컴포넌트는 더 이상 리렌더링되지 않고 콘솔에 아무것도 찍히지 않습니다. 성능 최적화에 성공한 것입니다.</p>
<h2 id="의존성-배열-deps의-역할-🧠">의존성 배열 deps의 역할 🧠</h2>
<p>만약 함수 안에서 state나 props를 사용한다면, 반드시 의존성 배열에 해당 값을 넣어주어야 합니다. 그렇지 않으면 함수는 오래된 값(stale state)을 기억하게 됩니다.
const [name, setName] = useState('홍길동');</p>
<p>// name 상태를 사용하므로, 의존성 배열에 name을 추가합니다.
// 이렇게 하면 name이 변경될 때만 함수가 새로 생성됩니다.
const showName = useCallback(() =&gt; {
  alert(<code>현재 이름: ${name}</code>);
}, [name]); </p>
<h2 id="⚠️-주의사항-언제-사용해야-할까">⚠️ 주의사항: 언제 사용해야 할까?</h2>
<p>useCallback은 공짜가 아닙니다. 함수를 기억하기 위해 메모리를 사용하고, 의존성을 비교하는 비용이 발생합니다. 따라서 모든 함수에 사용하는 것은 비효율적입니다.
useCallback은 아래와 같은 경우에 사용하는 것이 가장 효과적입니다.</p>
<ul>
<li>React.memo로 감싸진 자식 컴포넌트에 함수를 prop으로 전달할 때</li>
<li>커스텀 훅(Custom Hook)에서 반환하는 함수가 있을 때</li>
<li>useEffect의 의존성 배열에 함수를 넣어야 할 때</li>
</ul>