<p>React FC는 FunctionComponent의 줄임말로, 타입스크립트 환경에서 함수형 컴포넌트의 타입을 정의할 때 사용하던 타입입니다.
과거에는 children prop을 자동으로 포함시켜주는 등 몇 가지 편의 기능 때문에 많이 사용되었지만, 현재는 몇 가지 단점 때문에 사용을 권장하지 않는 추세입니다.</p>
<p>React.FC는 과거에 children prop의 타입을 자동으로 포함시켜주었기 때문에 주로 사용됐습니다.</p>
<h2 id="reactfc를-사용했던-이유">React.FC를 사용했던 이유</h2>
<ul>
<li>children 타입의 자동 포함 (가장 큰 이유)
과거에는 children을 props 타입에 일일이 children: React.ReactNode와 같이 추가하는 것이 번거롭다고 여겨졌습니다. React.FC를 사용하면 props 타입에 children을 정의하지 않아도 자동으로 children을 받을 수 있도록 만들어주어 코드 작성이 편리했습니다.
과거 코드<pre><code class="language-js">import React, { FC } from 'react';
</code></pre>
</li>
</ul>
<p>interface MyButtonProps {
  onClick: () =&gt; void;
}</p>
<p>// MyButtonProps에 children이 없지만, FC 덕분에 children을 사용할 수 있음
const MyButton: FC = ({ onClick, children }) to&gt; {
  return <button>{children}</button>;
};</p>
<pre><code>
 * 정적 프로퍼티 타입 제공
   displayName, propTypes, defaultProps와 같은 컴포넌트의 정적(static) 프로퍼티에 대한 타입 추론을 지원했습니다.
 * 함수형 컴포넌트라는 명시적 표현
   FC를 타입으로 지정함으로써 &quot;이것은 React 함수형 컴포넌트다&quot;라는 것을 코드상에서 명확하게 나타내는 역할을 했습니다.
하지만 지금은 props는 사용하는 것만 명시적으로 선언하는 것이 좋다는 원칙에 따라, children을 암시적으로 포함하는 React.FC의 사용을 더 이상 권장하지 않습니다.


## React.FC의 역할과 특징
React.FC를 사용하면 컴포넌트의 props 타입을 명시적으로 지정할 수 있습니다.
과거 방식 (React.FC 사용)

```js
import React, { FC } from 'react';

// Props 타입을 정의
interface GreetingProps {
  name: string;
}

// FC를 사용해 컴포넌트 타입을 지정
const Greeting: FC&lt;GreetingProps&gt; = ({ name, children }) =&gt; {
  return (
    &lt;div&gt;
      &lt;h1&gt;Hello, {name}!&lt;/h1&gt;
      {children}
    &lt;/div&gt;
  );
};</code></pre><p>React.FC는 다음과 같은 특징이 있었습니다.</p>
<ul>
<li>children을 암시적으로 포함: GreetingProps에 children을 정의하지 않아도, FC가 자동으로 children prop의 타입을 포함시켜주었습니다.</li>
<li>displayName, defaultProps 등 정적 프로퍼티 타입 제공: 컴포넌트의 displayName 같은 속성에 대한 타입 검사를 지원했습니다.</li>
</ul>
<h2 id="현재-reactfc-사용을-권장하지-않는-이유-👎">현재 React.FC 사용을 권장하지 않는 이유 👎</h2>
<p>React 커뮤니티와 주요 템플릿(Create React App 등)에서 FC 사용을 지양하는 이유는 명확합니다.</p>
<ul>
<li>암시적인 children은 좋지 않다: 컴포넌트가 children을 받지 않는 경우가 더 많습니다. FC는 사용하지도 않는 children prop을 항상 포함시켜 코드의 명확성을 떨어뜨립니다. <strong>&quot;컴포넌트의 props는 사용하는 것만 명시적으로 정의하는 것이 좋다&quot;</strong>는 원칙에 위배됩니다.</li>
<li>defaultProps와의 호환성 문제: defaultProps 기능이 React.FC와 함께 사용할 때 제대로 작동하지 않는 문제가 있었습니다.</li>
<li>코드의 장황함: FC를 쓰지 않는 것이 코드가 더 간결하고 직관적입니다.</li>
</ul>
<h2 id="현재-권장되는-방식-👍">현재 권장되는 방식 👍</h2>
<p>현재는 React.FC를 사용하지 않고, props 객체의 타입을 직접 컴포넌트에 적용하는 방식을 권장합니다. children이 필요할 경우, props 타입에 명시적으로 추가합니다.
현재 권장 방식 (직접 타입 적용)</p>
<pre><code class="language-js">import React, { PropsWithChildren } from 'react';

// Props 타입을 정의
interface GreetingProps {
  name: string;
}

// 1. children이 필요 없는 경우
const Greeting = ({ name }: GreetingProps) =&gt; {
  return &lt;h1&gt;Hello, {name}!&lt;/h1&gt;;
};


// 2. children이 필요한 경우 (PropsWithChildren 사용)
type GreetingWithChildrenProps = PropsWithChildren&lt;GreetingProps&gt;;

const GreetingWithChildren = ({ name, children }: GreetingWithChildrenProps) =&gt; {
  return (
    &lt;div&gt;
      &lt;h1&gt;Hello, {name}!&lt;/h1&gt;
      {children}
    &lt;/div&gt;
  );
};</code></pre>
<p>이 방식은 컴포넌트가 받는 props를 명확하게 보여주고, 불필요한 타입을 제거하여 더 깔끔하고 예측 가능한 코드를 작성하게 해줍니다.</p>