---
id: basic-operators.md
summary: >-
  Milvus는 데이터를 효율적으로 필터링하고 쿼리하는 데 도움이 되는 다양한 기본 연산자 세트를 제공합니다. 이러한 연산자를 사용하면 스칼라
  필드, 숫자 계산, 논리적 조건 등을 기반으로 검색 조건을 세분화할 수 있습니다. 이러한 연산자를 사용하는 방법을 이해하는 것은 정확한
  쿼리를 작성하고 검색의 효율성을 극대화하는 데 매우 중요합니다.
title: 기본 연산자
---
<h1 id="Basic-Operators​" class="common-anchor-header">기본 연산자<button data-href="#Basic-Operators​" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h1><p>Milvus는 데이터를 효율적으로 필터링하고 쿼리하는 데 도움이 되는 다양한 기본 연산자 세트를 제공합니다. 이러한 연산자를 사용하면 스칼라 필드, 숫자 계산, 논리적 조건 등을 기반으로 검색 조건을 세분화할 수 있습니다. 이러한 연산자를 사용하는 방법을 이해하는 것은 정확한 쿼리를 작성하고 검색의 효율성을 극대화하는 데 매우 중요합니다.</p>
<h2 id="Comparison-operators​" class="common-anchor-header">비교 연산자<button data-href="#Comparison-operators​" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>비교 연산자는 같음, 같지 않음 또는 크기에 따라 데이터를 필터링하는 데 사용됩니다. 숫자, 텍스트, 날짜 필드에 적용할 수 있습니다.</p>
<h3 id="Supported-Comparison-Operators​" class="common-anchor-header">지원되는 비교 연산자</h3><ul>
<li><p><code translate="no">==</code> (같음)</p></li>
<li><p><code translate="no">!=</code> (같지 않음)</p></li>
<li><p><code translate="no">&gt;</code> (보다 큼)</p></li>
<li><p><code translate="no">&lt;</code> (보다 작음)</p></li>
<li><p><code translate="no">&gt;=</code> (보다 크거나 같음)</p></li>
<li><p><code translate="no">&lt;=</code> (다음보다 작거나 같음)</p></li>
</ul>
<h3 id="Example-1-Filtering-with-Equal-To-​" class="common-anchor-header">예 1: 같음(<code translate="no">==</code>)으로 필터링</h3><p><code translate="no">status</code> 이라는 필드가 있고 <code translate="no">status</code> 이 &quot;활성&quot;인 모든 엔터티를 찾고자 한다고 가정합니다. 같음 연산자 <code translate="no">==</code> 를 사용할 수 있습니다.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;status == &quot;active&quot;&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h3 id="Example-2-Filtering-with-Not-Equal-To-​" class="common-anchor-header">예 2: 같지 않음 (<code translate="no">!=</code>)으로 필터링하기</h3><p><code translate="no">status</code> 이 &quot;비활성&quot;이 아닌 엔터티를 찾으려는 경우.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;status != &quot;inactive&quot;&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h3 id="Example-3-Filtering-with-Greater-Than-​" class="common-anchor-header">예 3: Greater Than (<code translate="no">&gt;</code>)으로 필터링하기</h3><p><code translate="no">age</code> 이 30보다 큰 모든 엔터티를 찾으려는 경우.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;age &gt; 30&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h3 id="Example-4-Filtering-with-Less-Than-​" class="common-anchor-header">예 4: 미만 (<code translate="no">&lt;</code>)으로 필터링하기</h3><p><code translate="no">price</code> 이 100 미만인 엔터티를 찾으려면 다음과 같이 하세요.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;price &lt; 100&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h3 id="Example-5-Filtering-with-Greater-Than-or-Equal-To-​" class="common-anchor-header">예 5: 보다 크거나 같음(<code translate="no">&gt;=</code>)으로 필터링하기</h3><p><code translate="no">rating</code> 이 4보다 크거나 같은 모든 엔터티를 찾으려는 경우.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;rating &gt;= 4&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h3 id="Example-6-Filtering-with-Less-Than-or-Equal-To-​" class="common-anchor-header">예 6: 보다 작거나 같음(<code translate="no">&lt;=</code>)으로 필터링하기</h3><p><code translate="no">discount</code> 이 10% 이하인 엔터티를 찾으려면.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;discount &lt;= 10&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h2 id="Range-operators​" class="common-anchor-header">범위 연산자<button data-href="#Range-operators​" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>범위 연산자는 특정 집합 또는 값 범위를 기준으로 데이터를 필터링하는 데 도움이 됩니다.</p>
<h3 id="Supported-Range-Operators​" class="common-anchor-header">지원되는 범위 연산자</h3><ul>
<li><p><code translate="no">IN</code>: 특정 집합 또는 범위 내의 값을 일치시키는 데 사용됩니다.</p></li>
<li><p><code translate="no">LIKE</code>: 패턴을 일치시키는 데 사용됩니다(주로 텍스트 필드에 사용).</p></li>
</ul>
<h3 id="Example-1-Using-IN-to-Match-Multiple-Values​" class="common-anchor-header">예 1: <code translate="no">IN</code> 사용하여 여러 값 일치시키기</h3><p><code translate="no">color</code> 이 &quot;빨간색&quot;, &quot;녹색&quot; 또는 &quot;파란색&quot;인 모든 엔티티를 찾고자 하는 경우.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;color in [&quot;red&quot;, &quot;green&quot;, &quot;blue&quot;]&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<p>이 방법은 값 목록에서 멤버십 여부를 확인하려는 경우에 유용합니다.</p>
<h3 id="Example-2-Using-LIKE-for-Pattern-Matching​" class="common-anchor-header">예 2: 패턴 일치에 <code translate="no">LIKE</code> 사용</h3><p><code translate="no">LIKE</code> 연산자는 문자열 필드에서 패턴 일치에 사용됩니다. 이 연산자는 텍스트 내에서 <strong>접두사</strong>, <strong>접두사</strong> 또는 <strong>접미사</strong> 등 다양한 위치의 하위 문자열을 일치시킬 수 있습니다. <code translate="no">LIKE</code> 연산자는 <code translate="no">%</code> 기호를 와일드카드로 사용하며, 0을 포함하여 원하는 수의 문자를 일치시킬 수 있습니다.</p>
<h4 id="Prefix-Match-Starts-With​" class="common-anchor-header">접두사 일치(다음으로 시작)</h4><p>문자열이 지정된 패턴으로 시작하는 <strong>접두사</strong> 일치를 수행하려면 패턴을 처음에 배치하고 <code translate="no">%</code> 을 사용하여 그 뒤에 오는 모든 문자를 일치시킬 수 있습니다. 예를 들어 <code translate="no">name</code> 가 &quot;Prod&quot;로 시작하는 모든 제품을 찾으려면.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;name LIKE &quot;Prod%&quot;&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<p>이렇게 하면 &quot;제품 A&quot;, &quot;제품 B&quot; 등과 같이 이름이 &quot;Prod&quot;로 시작하는 모든 제품이 일치합니다.</p>
<h4 id="Suffix-Match-Ends-With​" class="common-anchor-header">접미사 일치(끝으로 끝남)</h4><p>문자열이 지정된 패턴으로 끝나는 <strong>접미사</strong> 일치의 경우, 패턴의 시작 부분에 <code translate="no">%</code> 기호를 배치합니다. 예를 들어 <code translate="no">name</code> 이 &quot;XYZ&quot;로 끝나는 모든 제품을 찾으려면.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;name LIKE &quot;%XYZ&quot;&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<p>이렇게 하면 이름이 &quot;XYZ&quot;로 끝나는 모든 제품(예: &quot;ProductXYZ&quot;, &quot;SampleXYZ&quot; 등)이 일치합니다.</p>
<h4 id="Infix-Match-Contains​" class="common-anchor-header">접두사 일치(포함)</h4><p>문자열의 어느 위치에나 패턴이 나타날 수 있는 <strong>접두사</strong> 일치를 수행하려면 패턴의 시작과 끝 모두에 <code translate="no">%</code> 기호를 배치하면 됩니다. 예를 들어 <code translate="no">name</code> 에 &quot;Pro&quot;라는 단어가 포함된 모든 제품을 찾습니다.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;name LIKE &quot;%Pro%&quot;&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<p>이렇게 하면 이름에 &quot;Pro&quot;가 포함된 모든 제품(예: &quot;Product&quot;, &quot;ProLine&quot; 또는 &quot;SuperPro&quot;)이 일치합니다.</p>
<h2 id="Arithmetic-Operators​" class="common-anchor-header">산술 연산자<button data-href="#Arithmetic-Operators​" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>산술 연산자를 사용하면 숫자 필드와 관련된 계산을 기반으로 조건을 생성할 수 있습니다.</p>
<h3 id="Supported-Arithmetic-Operators​" class="common-anchor-header">지원되는 산술 연산자.</h3><ul>
<li><p><code translate="no">+</code> (더하기)</p></li>
<li><p><code translate="no">-</code> (빼기)</p></li>
<li><p><code translate="no">*</code> (곱셈)</p></li>
<li><p><code translate="no">/</code> (나누기)</p></li>
<li><p><code translate="no">%</code> (모듈러스)</p></li>
<li><p><code translate="no">**</code> (지수)</p></li>
</ul>
<h3 id="Example-1-Using-Addition-+​" class="common-anchor-header">예 1: 더하기(<code translate="no">+</code>) 사용</h3><p><code translate="no">total</code> 가격이 <code translate="no">base_price</code> 과 <code translate="no">tax</code> 의 합계인 엔티티를 찾으려면.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;total == base_price + tax&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h3 id="Example-2-Using-Subtraction--​" class="common-anchor-header">예 2: 빼기 사용 (<code translate="no">-</code>)</h3><p><code translate="no">quantity</code> 이 50보다 크고 <code translate="no">quantity_sold</code> 이 30보다 작은 엔티티를 찾으려면.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;quantity - quantity_sold &gt; 50&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h3 id="Example-3-Using-Multiplication-​" class="common-anchor-header">예 3: 곱하기 사용 (<code translate="no">*</code>)</h3><p><code translate="no">price</code> 가 100보다 크고 <code translate="no">quantity</code> 가 10보다 큰 엔터티를 찾으려면 곱하기.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;price * quantity &gt; 1000&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h3 id="Example-4-Using-Division-​" class="common-anchor-header">예 4: 나누기 사용 (<code translate="no">/</code>)</h3><p><code translate="no">total_price</code> 를 <code translate="no">quantity</code> 로 나눈 값이 50보다 작은 제품을 찾으려면.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;total_price / quantity &lt; 50&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h3 id="Example-5-Using-Modulus-​" class="common-anchor-header">예 5: 모듈러스 사용 (<code translate="no">%</code>)</h3><p><code translate="no">id</code> 이 짝수(즉, 2로 나눌 수 있는)인 엔티티를 찾으려면 다음과 같이 하세요.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;id % 2 == 0&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h3 id="Example-6-Using-Exponentiation-​" class="common-anchor-header">예 6: 지수 사용(<code translate="no">**</code>)</h3><p><code translate="no">price</code> 를 2의 거듭 제곱한 값이 1000보다 큰 엔터티를 찾으려면 다음과 같이 하세요.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;price ** 2 &gt; 1000&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h2 id="Logical-Operators​" class="common-anchor-header">논리 연산자<button data-href="#Logical-Operators​" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>논리 연산자는 여러 조건을 보다 복잡한 필터 표현식으로 결합하는 데 사용됩니다. 여기에는 <code translate="no">AND</code>, <code translate="no">OR</code>, <code translate="no">NOT</code> 등이 포함됩니다.</p>
<h3 id="Supported-Logical-Operators​" class="common-anchor-header">지원되는 논리 연산자</h3><ul>
<li><p><code translate="no">AND</code>: 모두 참이어야 하는 여러 조건을 결합합니다.</p></li>
<li><p><code translate="no">OR</code>: 하나 이상의 조건이 참이어야 하는 조건을 결합합니다.</p></li>
<li><p><code translate="no">NOT</code>: 조건을 무효화합니다.</p></li>
</ul>
<h3 id="Example-1-Using-AND-to-Combine-Conditions​" class="common-anchor-header">예 1: <code translate="no">AND</code> 사용하여 조건 결합하기</h3><p><code translate="no">price</code> 가 100보다 크고 <code translate="no">stock</code> 가 50보다 큰 모든 제품을 찾습니다.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;price &gt; 100 AND stock &gt; 50&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h3 id="Example-2-Using-OR-to-Combine-Conditions​" class="common-anchor-header">예 2: <code translate="no">OR</code> 사용하여 조건 결합하기</h3><p><code translate="no">color</code> 이 &quot;빨간색&quot; 또는 &quot;파란색&quot;인 모든 제품을 찾으려면.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;color == &quot;red&quot; OR color == &quot;blue&quot;&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h3 id="Example-3-Using-NOT-to-Exclude-a-Condition​" class="common-anchor-header">예 3: <code translate="no">NOT</code> 사용하여 조건 제외하기</h3><p><code translate="no">color</code> 이 &quot;녹색&quot;이 아닌 모든 제품을 찾으려면.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;NOT color == &quot;green&quot;&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h2 id="Tips-on-Using-Basic-Operators-with-JSON-and-ARRAY-Fields​" class="common-anchor-header">JSON 및 배열 필드에서 기본 연산자 사용에 대한 팁<button data-href="#Tips-on-Using-Basic-Operators-with-JSON-and-ARRAY-Fields​" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>Milvus의 기본 연산자는 다목적이며 스칼라 필드에 적용할 수 있지만, JSON 및 ARRAY 필드의 키와 인덱스에도 효과적으로 사용할 수 있습니다.</p>
<p>예를 들어 <code translate="no">price</code>, <code translate="no">model</code>, <code translate="no">tags</code> 과 같은 여러 개의 키가 포함된 <code translate="no">product</code> 필드가 있는 경우 항상 키를 직접 참조하세요.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;product[&quot;price&quot;] &gt; 1000&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<p>기록된 온도 배열에서 첫 번째 온도가 특정 값을 초과하는 기록을 찾으려면 다음을 사용합니다.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&#x27;history_temperatures[0] &gt; 30&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h2 id="Conclusion​" class="common-anchor-header">결론<button data-href="#Conclusion​" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>Milvus는 데이터를 유연하게 필터링하고 쿼리할 수 있는 다양한 기본 연산자를 제공합니다. 비교, 범위, 산술 및 논리 연산자를 결합하여 강력한 필터 표현식을 만들어 검색 결과의 범위를 좁히고 필요한 데이터를 효율적으로 검색할 수 있습니다.</p>