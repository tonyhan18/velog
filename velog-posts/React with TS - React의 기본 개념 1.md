<h1 id="개발-환경-설정">개발 환경 설정</h1>
<pre><code class="language-js">npm create vite@latest</code></pre>
<pre><code class="language-js">npm install
npm run dev</code></pre>
<h1 id="react의-기본-개념">React의 기본 개념</h1>
<h2 id="01-컴포넌트-만들기jsx문법">01. 컴포넌트 만들기(JSX문법)</h2>
<p>React 컴포넌트는 무조건 대문자로 시작해야한다</p>
<p>쓸때 없는 태그를 때기 위해서</p>
<pre><code class="language-js">&lt;&gt;&lt;/&gt;
&lt;Fragment&gt;&lt;/Fragment&gt;</code></pre>
<p>jsx는 무조건 닫아줘야 한다</p>
<p>jsx의 기능에서는 Camel로 해주어야 한다</p>
<pre><code class="language-js">className
onClick</code></pre>
<ol>
<li><p>function 컴포넌트, input 버튼
if나 for문을 tag에서 사용할 수 없음</p>
</li>
<li><p>컴포넌트 만들기(Props 전달하기)
배열 보내기</p>
</li>
</ol>
<p>스프레드 문법 사용하기</p>
<pre><code class="language-js">{...destinations[0]}</code></pre>
<p>하우 컴포넌트로 children 보내기
<img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/97ba464a-81b4-4d96-8f4f-0f018efab406/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/cf76f0a1-1813-405e-aaa8-9997e2b492e7/image.png" /></p>
<h2 id="3-컴포넌트-만들기조건부-렌더링">3. 컴포넌트 만들기(조건부 렌더링)</h2>
<p>조건에 따라 렌더링할지 말지를 결정하는 것</p>
<p>숫자로 렌더링 하는 경우 </p>
<p>안티패턴
조건문을 컴포넌트 안에 작성하면 실재로 어떻게 동작하는지 알아보기 어렵다. 그래서 조건문은 가급적 컴포넌트 내부가 아닌 곳에 작성해야 한다</p>
<h2 id="4-목록-렌더링">4. 목록 렌더링</h2>
<p>배열을 렌더링 할때 각 요소에 key 요소를 넣어주어야 한다.</p>
<p>key는 고유한 값이어야 한다.
key는 안정적인 값이어야 한다.
=&gt; 성분으로 index를 보낸 경우 사용하면 안된다.</p>
<pre><code class="language-js">export const FilteredList = () =&gt; {
    const items = [
      {
          id: 1,
        text: &quot;learn react&quot;,
        completed: true,
      },
      {
          id: 2
        text: &quot;build ui&quot;,
        completed: false,
      },
      {
          id: 3
        text: &quot;fetch API&quot;,
        completed: true,
      }
    ];
  return &lt;ul&gt;
    {
  items.filter(i=&gt;i.completed === false).map(i=&gt;&lt;li key={i}&gt;{i.text}&lt;/li&gt;)         
                                             }
    &lt;/ul&gt;

};
                                             export default List;</code></pre>
<h2 id="5-컴포넌트-만들기이벤트-처리하기">5. 컴포넌트 만들기(이벤트 처리하기)</h2>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/7a56735d-c1df-4c53-be6c-228d667ed827/image.png" /></p>
<p>직전 onClick으로 이벤트를 묶을 수도 있고 아래와 같이 인자로 보낼 수도 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/8a6544c1-b538-47fa-87b1-56f5428cf891/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/b976b562-f834-418c-a011-10480d8ac279/image.png" /></p>
<p>input에 있었던 값을 위와 같은 형태로 해서 받을 수 있다.</p>
<p>이때 그냥 값을 받아오면 입력값이 사라진다. 이렇게 되는 이유는 onSubmit시 브라우저에서 기본적으로 일어나는 동작이 발생했기 때문이다.</p>
<p>그래서 event.preventDefault()로 이 동작을 막아주어야 한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/69231fe0-e8f4-4c65-b0c0-ea9e05c532a7/image.png" /></p>
<p>이벤트가 상위 태그로 전파하는 것이 있다. 이벤트가 트리를 통해서 부모로 전달되는 경우가 있다.</p>
<p>이를 막기 위해서 위와 같이 작성해야한다.</p>
<h2 id="6-컴포넌트-만들기">6. 컴포넌트 만들기</h2>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/ad65f5e2-f1b7-44ea-9615-5aaa6b78a3fb/image.png" /></p>
<p>state는 현재 컴포넌트의 데이터를 말한다</p>
<p>useState를 사용해서 값을 유지시킬 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/4cd5c242-a825-42c8-ae87-86098675b0e5/image.png" /></p>
<p>setCount를 세 번 불렀어도 값을 한 번 증가한다. state는 스냅샷 처럼 고정된 값을 가지기 때문에 3이 되지 않는다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tonyhan18/post/e445c14e-6c91-413b-a87c-4cae4027e1b9/image.png" /></p>
<p>이를 해결해가 위해서 업데이트 값을 넘겨주어야 한다.</p>