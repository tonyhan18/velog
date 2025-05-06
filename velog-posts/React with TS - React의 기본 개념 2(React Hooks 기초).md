<h1 id="usereducer">useReducer</h1>
<p>스테이트 관리 훅스, 스테이트 형태가 복잡할 때 또는 업데이트하는 로직을 분리하여 한 곳에 모으고 싶을 때 주로 사용</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/874eefbc-9ca9-472b-80d9-ccc4023082de/image.png" /></p>
<p>위와 같이 function이 많아지면 update 로직을 파악하기 힘들어진다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/17900a92-d5bc-410a-8928-9f045249cfae/image.png" /></p>
<p>그래서 위와같이 reducer를 이용해서 type에 따라 어떠한 action을 할지를 모아놓을 수 있다.</p>
<h1 id="context-api">Context API</h1>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/735e33f1-066b-41c2-afc6-9fe9d59ec985/image.png" /></p>
<p>필요한 컴포넌트로 데이터를 전달하기 위해 계속 전달에 전달을 해주는 문제점이 있다.</p>
<p>이를 해결하기 위해 Context를 사용하는 방법이 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/4cdc559b-348a-47cb-ac41-6e9cd38a9e59/image.png" /></p>
<p>처음에는 null로 createContext를 초기화 해주는데 Provider가 있으면 이 null은 무시될 수 있다.
provider는 context에서 데이터를 공유하는 역할을 한다</p>
<p>provider를 이용해서 컴포넌트를 감싸준다.</p>
<p>useContext를 사용해서 데이터를 사용한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/b2244100-cf5e-48ab-88eb-0f66f7c0c7c8/image.png" /></p>
<p>사용시에는 컴포넌트를 Provider로 감싸주면 사용 가능해진다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/e7155fda-c58a-40a0-acf5-5bb2193a6f53/image.png" /></p>
<p>또 다른 예시로 context 안에 state를 사용해서 상태를 관리할 수도 있다.</p>
<h1 id="useref">useRef</h1>
<p>useRef는 동요소를 조작할 때 값을 저장하지만 렌더링이 다시 필요하지 않을 때 사용한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/63bc3e72-8807-44eb-91a3-908f08f874d8/image.png" /></p>
<p>useRef는 단순히 current 속성을 읽고 수정할 수 있는 단순한 객체이다. 단, 이 값을 변경한다고 해도 컴포넌트가 변경되지 않는다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/b52c151a-bc73-4b60-bf45-2aeee6c9593a/image.png" /></p>
<p>위와 같은 방식으로 setInterval을 이용해 1초 간격마다 값을 증가시키는 방법이 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/eb192d86-649a-4ffa-b640-53c6903bad66/image.png" /></p>
<p>돔 요소에 접근하는 방법도 있다.
Ref를 사용하면 상태가 변경되지 않기 때문에 focus 상태를 유지할 수 있다.</p>
<h1 id="useeffect">useEffect</h1>
<p>리액트 컴포넌트가 리랜더링된 이후 사이드 이펙트를 조작하기 위해서 사용한다.</p>
<p>사이드 이펙트 =&gt; 데이터 패칭, DOM 조작, 렌더링 외부에서 일어나는 모든 작업을 말한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/479be05e-df88-4b87-989f-4c946702e32f/image.png" /></p>
<p>사이드 이펙트가 일어나는 함수와 의존성 배열을 인자로 받는다.
의존성 배열이 빈 배열일 때는 컴포넌트가 마운트될 때만 발생한다. 마운트란 컴포넌트가 처음 DOM에 삽입될 때를 이야기한다.</p>
<p>그냥 하면 로그가 두 번 뜨는데 이는 strict 모드로 React를 실행시켜서 그렇다.
strict 모드란 애플리케이션의 잠재적인 문제를 알아내는 도구이다. 이걸 잠시만 비활성화시키면 안된다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/98ad5bb8-71ad-442a-a88a-bf096bdcf620/image.png" /></p>
<p>특정한 상태나 props가 변결될때 동작하게 하려면 빈배열에 전달해야 한다.</p>
<p>위의 경우 state가 변경될 경우 log를 띄어달라는 코드다.</p>
<p>useEffect의 특징으로 props와 state에 대해서만 반응한다. 왜냐하면 리렌더링이 이루어지기 때문이다. 반대로 useRef를 사용하면 반응하지 않는다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/7f6af468-9679-47c1-b34f-e00c147d8664/image.png" /></p>
<p>위와같이 timer를 설정해서 값을 증가시키고 컴포넌트가 종료(unmount)되면 자동으로 종료시킬 수 있도록 return으로 처리하는 방법이 있다.</p>
<h1 id="virutal-dom과-react-reconciliation재조정">virutal dom과 react reconciliation(재조정)</h1>
<p>virtual dom은 ui를 메모리에 저장하고 react dom과 같은 라이브러리에 실제 DOM과 동기화 시킨다.</p>
<p>리액트는 상태 변화 발생시 새로운 virtual dom을 생성해서 변경된 부분만 반영한다.</p>
<p>다만 비교 연산은 매우 비싸기 때문에 휴리스틱 알고리즘으로 이를 계산한다.</p>
<ul>
<li>다른 태그가 나오면 다른 트리로 간주하고 새 DOM을 만든다.</li>
<li>동일한 태그면 속성과 자식을 비교해서 변경된 부분만 반영한다.</li>
<li>같은 타입의 컴포넌트가 생성됐을 경우 useState는 유지하고 props만 렌더링한다.</li>
</ul>