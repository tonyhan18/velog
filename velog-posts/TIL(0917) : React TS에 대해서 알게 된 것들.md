<h1 id="-와--의-사용법">?? 와 || 의 사용법</h1>
<p>네, Next.js (TypeScript)에서 변수 뒤에 붙는 ??는 <strong>Nullish Coalescing Operator (널 병합 연산자)</strong>라고 불러요.
간단히 말해, 왼쪽 값이 null 또는 undefined일 때만 오른쪽 값을 사용하라는 뜻입니다.</p>
<h2 id="-널-병합-연산자-와--논리적-or-연산자의-차이점">?? (널 병합 연산자) 와 || (논리적 OR 연산자)의 차이점</h2>
<p>이 연산자는 기존에 사용하던 || (OR) 연산자의 단점을 보완하기 위해 나왔어요. 둘의 차이를 아는 것이 핵심입니다.</p>
<ul>
<li>|| (OR 연산자): 왼쪽 값이 &quot;falsy&quot; (거짓 같은 값)이면 오른쪽 값을 사용합니다.<ul>
<li>&quot;falsy&quot; 값에는 null, undefined 뿐만 아니라 0, &quot;&quot; (빈 문자열), false, NaN도 포함돼요.</li>
</ul>
</li>
<li>?? (널 병합 연산자): 왼쪽 값이 null 또는 undefined일 때만 오른쪽 값을 사용합니다.<ul>
<li>0이나 &quot;&quot;(빈 문자열) 등은 유효한 값으로 취급해요.<h2 id="코드-예시">코드 예시</h2>
아래 예시를 보면 차이가 명확하게 이해될 거예요.
// --- 1. 값이 null 또는 undefined 일 때 ---
// 두 연산자 모두 동일하게 동작합니다.
const name1 = null ?? 'Guest'; // 결과: 'Guest'
const name2 = null || 'Guest'; // 결과: 'Guest'</li>
</ul>
</li>
</ul>
<p>const age1 = undefined ?? 20; // 결과: 20
const age2 = undefined || 20; // 결과: 20</p>
<p>// --- 2. 값이 0 또는 빈 문자열(&quot;&quot;)일 때 (가장 중요한 차이점) ---
// 사용자 점수(score)가 0점일 경우
let score = 0;
const finalScore_OR = score || 10; // 0은 &quot;falsy&quot; 이므로 10이 할당됨
const finalScore_Nullish = score ?? 10; // 0은 null이 아니므로 0이 그대로 할당됨</p>
<p>console.log(finalScore_OR); // 10 (버그의 원인이 될 수 있음!)
console.log(finalScore_Nullish); // 0 (의도한 대로 동작)</p>
<p>// 텍스트 입력(text)이 비어있을 경우
let text = &quot;&quot;;
const finalText_OR = text || &quot;기본 텍스트&quot;; // &quot;&quot;는 &quot;falsy&quot; 이므로 &quot;기본 텍스트&quot;가 할당됨
const finalText_Nullish = text ?? &quot;기본 텍스트&quot;; // &quot;&quot;는 null이 아니므로 &quot;&quot;가 그대로 할당됨</p>
<p>console.log(finalText_OR); // &quot;기본 텍스트&quot;
console.log(finalText_Nullish); // &quot;&quot; (빈 문자열)</p>
<p>결론적으로, API 응답 값이나 사용자 입력처럼 값이 0이거나 빈 문자열 &quot;&quot;인 경우를 유효한 데이터로 처리하고, 오직 값이 존재하지 않는 null 또는 undefined 상황에서만 기본값을 지정하고 싶을 때 ??를 사용하면 코드가 훨씬 더 안전하고 명확해집니다.
이와 비슷하게 null이나 undefined를 안전하게 처리하는 데 자주 사용되는 연산자로 Optional Chaining (?.) 이 있는데, 혹시 객체의 속성에 안전하게 접근하는 이 연산자에 대해서도 예시와 함께 알아볼까요?</p>
<h1 id="react-매개변수-전달-방법들">React 매개변수 전달 방법들</h1>
<p>React 컴포넌트에 매개변수(props)를 전달하는 방법은 여러 가지가 있어요. 가장 기본적인 방법부터 고급 패턴까지 핵심적인 방법들을 예시와 함께 알려드릴게요.</p>
<h2 id="1-기본-props-전달-가장-일반적인-방법">1. 기본 Props 전달 (가장 일반적인 방법)</h2>
<p>HTML 속성(attribute)을 지정하듯이 부모 컴포넌트에서 자식 컴포넌트로 값을 전달하는 가장 기본적인 방법입니다.
ParentComponent.js
import ChildComponent from './ChildComponent';</p>
<p>function ParentComponent() {
  const userName = &quot;Alice&quot;;
  const userAge = 30;</p>
<p>  return (
    
  );
}</p>
<p>ChildComponent.js
자식 컴포넌트는 props라는 하나의 객체로 모든 매개변수를 받습니다.
function ChildComponent(props) {
  // props 객체는 { name: 'Alice', age: 30, isLoggedIn: true } 형태입니다.
  return (
    <div>
      <h1>이름: {props.name}</h1>
      <p>나이: {props.age}</p>
      {props.isLoggedIn ? <p>로그인됨</p> : <p>로그아웃됨</p>}
    </div>
  );
}</p>
<h2 id="2-props-구조-분해-할당-destructuring">2. Props 구조 분해 할당 (Destructuring)</h2>
<p>위의 기본 방법보다 훨씬 깔끔하고 가독성이 좋은 방식입니다. props 객체를 바로 구조 분해하여 필요한 값만 변수로 받아 사용합니다. 요즘 가장 많이 쓰는 방법이에요. 👍
ChildComponent.js (Destructuring)
function ChildComponent({ name, age, isLoggedIn }) {
  // 더 이상 props.name, props.age 라고 쓸 필요가 없습니다.
  return (
    <div>
      <h1>이름: {name}</h1>
      <p>나이: {age}</p>
      {isLoggedIn ? <p>로그인됨</p> : <p>로그아웃됨</p>}
    </div>
  );
}</p>
<h2 id="3-children-prop-사용하기">3. children Prop 사용하기</h2>
<p>컴포넌트의 여는 태그와 닫는 태그 사이에 있는 내용을 전달할 때 사용하는 특별한 prop입니다. 레이아웃이나 래퍼(Wrapper) 컴포넌트를 만들 때 매우 유용합니다.
ParentComponent.js
import Card from './Card';</p>
<p>function ParentComponent() {
  return (
    
      {/* 이 안의 모든 내용이 Card 컴포넌트의 children prop으로 전달됩니다. */}
      <h1>프로필 카드</h1>
      <p>이 내용은 Card 컴포넌트 안에서 렌더링됩니다.</p>
    
  );
}</p>
<p>Card.js
function Card({ children }) {
  // Card 스타일링
  const cardStyle = {
    padding: '20px',
    border: '1px solid #ddd',
    borderRadius: '8px',
    boxShadow: '0 2px 4px rgba(0,0,0,0.1)'
  };</p>
<p>  return (
    <div>
      {children}
    </div>
  );
}</p>
<h2 id="4-props-펼침spread-연산자-사용">4. Props 펼침(Spread) 연산자 사용</h2>
<p>부모가 가진 props 객체 전체를 자식에게 그대로 전달하고 싶을 때 사용합니다. 코드를 간결하게 유지할 수 있습니다.
ParentComponent.js
import UserProfile from './UserProfile';</p>
<p>function ParentComponent() {
  const userProps = {
    name: &quot;Bob&quot;,
    age: 42,
    job: &quot;Developer&quot;
  };</p>
<p>  return &lt;UserProfile {...userProps} /&gt;;
  // 위 코드는 아래와 동일합니다.
  // 
}</p>
<p>UserProfile.js
function UserProfile({ name, age, job }) {
  return (
    <div>
      <p>{name} ({age}) - {job}</p>
    </div>
  );
}</p>
<p>지금까지는 부모가 자식에게 데이터를 전달하는 방법(Top-down)을 알아봤는데요, 실제 개발에서는 자식 컴포넌트에서 발생한 이벤트를 부모에게 알려줘야 할 때가 많습니다.
혹시 자식 컴포넌트의 버튼 클릭 같은 이벤트를 부모 컴포넌트로 전달하는 방법(Bottom-up)에 대해서도 예시와 함께 알아볼까요?</p>
<p>네, TypeScript와 함께 함수형 컴포넌트에서 매개변수(props)를 다루는 방법, 직접 타입을 정의하는 경우, 그리고 ...props (나머지 매개변수) 사용법까지 상세히 알려드릴게요.</p>
<h2 id="1-함수형-컴포넌트와-타입-정의-기본">1. 함수형 컴포넌트와 타입 정의 (기본)</h2>
<p>가장 일반적인 방법은 컴포넌트가 받을 props의 타입을 type이나 interface로 먼저 정의하고, 컴포넌트의 매개변수에 해당 타입을 지정하는 것입니다.
UserProfile.tsx
import React from 'react';</p>
<p>// 1. 내가 직접 자료형(타입)을 만든다.
// 컴포넌트가 받을 props의 형태와 각 prop의 타입을 명시합니다.
type UserProfileProps = {
  username: string;
  age: number;
  isActive: boolean;
};</p>
<p>// 2. React.FC (Function Component) 타입을 사용하고 제네릭으로 props 타입을 지정한다.
// FC를 사용하면 children prop이 기본적으로 포함됩니다. (React 18부터는 명시적으로 추가해야 함)
const UserProfile: React.FC = ({ username, age, isActive }) =&gt; {
  return (
    <div>
      <h1>{username} ({age}세)</h1>
      <p>활동 상태: {isActive ? '활성' : '비활성'}</p>
    </div>
  );
};</p>
<p>export default UserProfile;</p>
<p>ParentComponent.tsx
import UserProfile from './UserProfile';</p>
<p>function ParentComponent() {
  return ;
}</p>
<p>장점:</p>
<ul>
<li>타입 안정성: username을 숫자로 전달하는 등 실수를 하면 TypeScript가 즉시 에러를 알려줍니다.</li>
<li>자동 완성: 코드 에디터에서 props의 종류를 자동으로 추천해줘서 개발이 편리합니다.</li>
<li>가독성: 컴포넌트가 어떤 데이터를 필요로 하는지 명확하게 알 수 있습니다.<h2 id="2-props-나머지-매개변수-사용법">2. ...props (나머지 매개변수) 사용법</h2>
...props (Rest 파라미터)는 특정 props는 직접 사용하고, 나머지 모든 props를 하나의 객체로 모아서 다른 컴포넌트나 HTML 요소에 그대로 전달하고 싶을 때 사용합니다. 특히 기본 HTML 요소의 속성(예: className, id, onClick)을 모두 지원하는 커스텀 컴포넌트를 만들 때 매우 유용합니다.
CustomButton.tsx
import React from 'react';</li>
</ul>
<p>// 1. 직접 사용할 props와 나머지 props 타입을 정의합니다.
// React.ButtonHTMLAttributes는 <button> 태그가 가질 수 있는
// 모든 속성(type, onClick, className 등)의 타입을 포함합니다.
type CustomButtonProps = {
  variant?: 'primary' | 'secondary'; // 이 컴포넌트만의 고유한 prop
} &amp; React.ButtonHTMLAttributes;</p>
<p>// 2. 매개변수에서 variant를 구조 분해하고, 나머지는 ...restProps로 받습니다.
const CustomButton: React.FC = ({ variant = 'primary', children, ...restProps }) =&gt; {</p>
<p>  // variant 값에 따라 기본 스타일을 정합니다.
  const baseStyle = {
    padding: '10px 20px',
    border: 'none',
    borderRadius: '5px',
    cursor: 'pointer',
    color: 'white',
  };</p>
<p>  const buttonStyle = {
    ...baseStyle,
    backgroundColor: variant === 'primary' ? '#007bff' : '#6c757d',
  };</p>
<p>  // 3. ...restProps를 <button> 요소에 그대로 펼쳐서 전달합니다.
  // 이렇게 하면 부모가 전달한 onClick, id, className 등이 모두 적용됩니다.
  return (
    &lt;button style={buttonStyle} {...restProps}&gt;
      {children}
    </button>
  );
};</p>
<p>export default CustomButton;</p>
<p>ParentComponent.tsx
import CustomButton from './CustomButton';</p>
<p>function ParentComponent() {
  const handleClick = () =&gt; {
    alert('버튼 클릭!');
  };</p>
<p>  return (
    <div>
      
        기본 버튼
      </p>
<pre><code>  &lt;CustomButton 
    variant=&quot;secondary&quot;
    onClick={() =&gt; console.log('두 번째 버튼 클릭')}
    disabled={true} // &lt;button&gt;의 기본 속성인 disabled도 전달 가능
  &gt;
    비활성 버튼
  &lt;/CustomButton&gt;
&lt;/div&gt;</code></pre><p>  );
}</p>
<p>...restProps를 사용하면 부모 컴포넌트에서 id, className, disabled, onClick 등 <button> 태그가 가질 수 있는 모든 속성을 CustomButton에 자유롭게 전달할 수 있어 컴포넌트의 재사용성이 극대화됩니다.
지금까지 컴포넌트에 props를 전달하고 타입을 정의하는 핵심적인 방법들을 알아봤습니다. 혹시 다음 단계로, 자식 컴포넌트에서 만든 데이터를 부모 컴포넌트로 다시 전달하는 방법(상태 끌어올리기)에 대한 예시도 필요하신가요?</p>