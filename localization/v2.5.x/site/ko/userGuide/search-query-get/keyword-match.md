---
id: keyword-match.md
summary: >-
  Milvus의 키워드 검색은 특정 용어를 기반으로 정확한 문서 검색을 가능하게 합니다. 이 기능은 주로 특정 조건을 충족하는 필터링 검색에
  사용되며, 스칼라 필터링을 통합하여 쿼리 결과를 구체화함으로써 스칼라 기준을 충족하는 벡터 내에서 유사성 검색을 할 수 있습니다.
title: 키워드 검색
---
<h1 id="Keyword-Match​" class="common-anchor-header">키워드 검색<button data-href="#Keyword-Match​" class="anchor-icon" translate="no">
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
    </button></h1><p>Milvus의 키워드 검색은 특정 용어를 기반으로 정확한 문서 검색을 가능하게 합니다. 이 기능은 주로 특정 조건을 충족하는 필터링 검색에 사용되며, 스칼라 필터링을 통합하여 쿼리 결과를 구체화함으로써 스칼라 기준을 충족하는 벡터 내에서 유사성 검색을 할 수 있습니다.</p>
<div class="alert note">
<p>키워드 검색은 일치하는 문서의 관련성을 점수화하지 않고 쿼리 용어가 정확히 일치하는 것을 찾는 데 중점을 둡니다. 쿼리 용어의 의미론적 의미와 중요도에 따라 가장 관련성이 높은 문서를 검색하려면 <a href="/docs/ko/full-text-search.md">전체 텍스트 검색을</a> 사용하는 것이 좋습니다.</p>
</div>
<h2 id="Overview" class="common-anchor-header">개요<button data-href="#Overview" class="anchor-icon" translate="no">
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
    </button></h2><p>Milvus는 기본 반전 색인 및 키워드 검색을 강화하기 위해 <a href="https://github.com/quickwit-oss/tantivy">Tantivy를</a> 통합합니다. 각 텍스트 항목에 대해 Milvus는 절차에 따라 색인을 생성합니다.</p>
<ol>
<li><p><a href="/docs/ko/analyzer-overview.md">분석기</a>: 분석기는 입력 텍스트를 개별 단어 또는 토큰으로 토큰화한 다음 필요에 따라 필터를 적용하여 처리합니다. 이를 통해 Milvus는 이러한 토큰을 기반으로 색인을 구축할 수 있습니다.</p></li>
<li><p><a href="/docs/ko/index-scalar-fields.md">인덱싱</a>: 텍스트 분석 후, Milvus는 각 고유 토큰을 해당 토큰이 포함된 문서에 매핑하는 역 인덱스를 생성합니다.</p></li>
</ol>
<p>사용자가 키워드 검색을 수행하면 반전된 색인을 사용해 해당 키워드가 포함된 모든 문서를 빠르게 검색합니다. 이는 각 문서를 개별적으로 스캔하는 것보다 훨씬 빠릅니다.</p>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/keyword-match.png" alt="Keyword Match" class="doc-image" id="keyword-match" />
   </span> <span class="img-wrapper"> <span>키워드 검색</span> </span></p>
<h2 id="Enable-keyword-match" class="common-anchor-header">키워드 검색 사용<button data-href="#Enable-keyword-match" class="anchor-icon" translate="no">
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
    </button></h2><p>키워드 검색은 기본적으로 Milvus의 문자열 데이터 유형인 <code translate="no">VARCHAR</code> 필드 유형에서 작동합니다. 키워드 검색을 활성화하려면 <code translate="no">enable_analyzer</code> 및 <code translate="no">enable_match</code> 을 모두 <code translate="no">True</code> 로 설정한 다음 수집 스키마를 정의할 때 텍스트 분석을 위한 분석기를 선택적으로 구성하세요.</p>
<h3 id="Set-enableanalyzer-and-enablematch​" class="common-anchor-header"><code translate="no">enable_analyzer</code> 및 <code translate="no">enable_match</code>설정</h3><p>특정 <code translate="no">VARCHAR</code> 필드에 대해 키워드 검색을 사용하려면 필드 스키마를 정의할 때 <code translate="no">enable_analyzer</code> 및 <code translate="no">enable_match</code> 매개 변수를 모두 <code translate="no">True</code> 으로 설정합니다. 이렇게 하면 Milvus가 텍스트를 토큰화하고 지정된 필드에 대한 반전 인덱스를 생성하도록 지시하여 빠르고 효율적인 키워드 매칭을 가능하게 합니다.</p>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> MilvusClient, DataType​
​
schema = MilvusClient.create_schema(auto_id=<span class="hljs-literal">True</span>, enable_dynamic_field=<span class="hljs-literal">False</span>)​
​
schema.add_field(​
    field_name=<span class="hljs-string">&#x27;text&#x27;</span>, ​
    datatype=DataType.VARCHAR, ​
    max_length=<span class="hljs-number">1000</span>, ​
    enable_analyzer=<span class="hljs-literal">True</span>, <span class="hljs-comment"># Whether to enable text analysis for this field​</span>
    enable_match=<span class="hljs-literal">True</span> <span class="hljs-comment"># Whether to enable text match​</span>
)​

<button class="copy-code-btn"></button></code></pre>
<h3 id="Optional-Configure-an-analyzer​" class="common-anchor-header">선택 사항입니다: 분석기 구성</h3><p>키워드 매칭의 성능과 정확도는 선택한 분석기에 따라 달라집니다. 다양한 분석기는 다양한 언어와 텍스트 구조에 맞춰져 있으므로 올바른 분석기를 선택하면 특정 사용 사례에 대한 검색 결과에 큰 영향을 미칠 수 있습니다.</p>
<p>기본적으로 Milvus는 공백과 구두점을 기준으로 텍스트를 토큰화하고, 40자 이상의 토큰을 제거하며, 텍스트를 소문자로 변환하는 <code translate="no">standard</code> 분석기를 사용합니다. 이 기본 설정을 적용하는 데는 추가 매개변수가 필요하지 않습니다. 자세한 내용은 <a href="/docs/ko/standard-analyzer.md">표준을</a> 참조하세요.</p>
<p>다른 분석기가 필요한 경우에는 <code translate="no">analyzer_params</code> 매개변수를 사용하여 분석기를 구성할 수 있습니다. 예를 들어, 영어 텍스트 처리를 위해 <code translate="no">english</code> 분석기를 적용하는 것입니다.</p>
<pre><code translate="no" class="language-python">analyzer_params={​
    <span class="hljs-string">&quot;type&quot;</span>: <span class="hljs-string">&quot;english&quot;</span>​
}​
​
schema.add_field(​
    field_name=<span class="hljs-string">&#x27;text&#x27;</span>, ​
    datatype=DataType.VARCHAR, ​
    max_length=<span class="hljs-number">200</span>, ​
    enable_analyzer=<span class="hljs-literal">True</span>，​
    analyzer_params=analyzer_params,​
    enable_match=<span class="hljs-literal">True</span>, ​
)​

<button class="copy-code-btn"></button></code></pre>
<p>Milvus는 다른 언어 및 시나리오에 적합한 다양한 분석기도 제공합니다. 자세한 내용은 <a href="/docs/ko/analyzer-overview.md">개요를</a> 참조하세요.</p>
<h2 id="Use-keyword-match" class="common-anchor-header">키워드 검색 사용<button data-href="#Use-keyword-match" class="anchor-icon" translate="no">
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
    </button></h2><p>컬렉션 스키마에서 VARCHAR 필드에 대해 키워드 일치를 활성화한 후에는 <code translate="no">TEXT_MATCH</code> 표현식을 사용하여 키워드 일치를 수행할 수 있습니다.</p>
<h3 id="TEXTMATCH-expression-syntax​" class="common-anchor-header">TEXT_MATCH 표현식 구문</h3><p><code translate="no">TEXT_MATCH</code> 표현식은 검색할 필드와 키워드를 지정하는 데 사용됩니다. 구문은 다음과 같습니다.</p>
<pre><code translate="no" class="language-python">TEXT_MATCH(field_name, text)​

<button class="copy-code-btn"></button></code></pre>
<ul>
<li><p><code translate="no">field_name</code>: 검색할 VARCHAR 필드의 이름입니다.</p></li>
<li><p><code translate="no">text</code>: 검색할 키워드입니다. 여러 키워드는 언어 및 구성된 분석기에 따라 공백이나 기타 적절한 구분 기호로 구분할 수 있습니다.</p></li>
</ul>
<p>기본적으로 <code translate="no">TEXT_MATCH</code> 은 <strong>OR</strong> 일치 로직을 사용하므로 지정된 키워드가 포함된 문서를 반환합니다. 예를 들어 <code translate="no">text</code> 필드에 <code translate="no">machine</code> 또는 <code translate="no">deep</code> 키워드가 포함된 문서를 검색하려면 다음 표현식을 사용합니다.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&quot;TEXT_MATCH(text, &#x27;machine deep&#x27;)&quot;</span>​

<button class="copy-code-btn"></button></code></pre>
<p>논리 연산자를 사용하여 여러 개의 <code translate="no">TEXT_MATCH</code> 표현식을 결합하여 <strong>AND</strong> 일치를 수행할 수도 있습니다. 예를 들어 <code translate="no">text</code> 필드에 <code translate="no">machine</code> 및 <code translate="no">deep</code> 키워드가 모두 포함된 문서를 검색하려면 다음 표현식을 사용합니다.</p>
<pre><code translate="no" class="language-python"><span class="hljs-built_in">filter</span> = <span class="hljs-string">&quot;TEXT_MATCH(text, &#x27;machine&#x27;) and TEXT_MATCH(text, &#x27;deep&#x27;)&quot;</span>​

<button class="copy-code-btn"></button></code></pre>
<h3 id="Search-with-keyword-match​" class="common-anchor-header">키워드 일치로 검색</h3><p>키워드 일치를 벡터 유사도 검색과 함께 사용하면 검색 범위를 좁히고 검색 성능을 향상시킬 수 있습니다. 벡터 유사도 검색 전에 키워드 일치를 사용하여 컬렉션을 필터링하면 검색해야 하는 문서 수를 줄여 쿼리 시간을 단축할 수 있습니다.</p>
<p>이 예에서 <code translate="no">filter</code> 표현식은 지정된 키워드 <code translate="no">keyword1</code> 또는 <code translate="no">keyword2</code> 와 일치하는 문서만 포함하도록 검색 결과를 필터링합니다. 그런 다음 이 필터링된 문서 하위 집합에 대해 벡터 유사도 검색이 수행됩니다.</p>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># Match entities with `keyword1` or `keyword2`​</span>
<span class="hljs-built_in">filter</span> = <span class="hljs-string">&quot;TEXT_MATCH(text, &#x27;keyword1 keyword2&#x27;)&quot;</span>​
​
<span class="hljs-comment"># Assuming &#x27;embeddings&#x27; is the vector field and &#x27;text&#x27; is the VARCHAR field​</span>
result = MilvusClient.search(​
    collection_name=<span class="hljs-string">&quot;YOUR_COLLECTION_NAME&quot;</span>, <span class="hljs-comment"># Your collection name​</span>
    anns_field=<span class="hljs-string">&quot;embeddings&quot;</span>, <span class="hljs-comment"># Vector field name​</span>
    data=[query_vector], <span class="hljs-comment"># Query vector​</span>
    <span class="hljs-built_in">filter</span>=<span class="hljs-built_in">filter</span>,​
    search_params={<span class="hljs-string">&quot;params&quot;</span>: {<span class="hljs-string">&quot;nprobe&quot;</span>: <span class="hljs-number">10</span>}},​
    limit=<span class="hljs-number">10</span>, <span class="hljs-comment"># Max. number of results to return​</span>
    output_fields=[<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-string">&quot;text&quot;</span>] <span class="hljs-comment"># Fields to return​</span>
)​

<button class="copy-code-btn"></button></code></pre>
<h3 id="Query-with-keyword-match​" class="common-anchor-header">키워드 일치를 사용한 쿼리</h3><p>키워드 검색은 쿼리 작업에서 스칼라 필터링에도 사용할 수 있습니다. <code translate="no">query()</code> 메서드의 <code translate="no">expr</code> 파라미터에 <code translate="no">TEXT_MATCH</code> 표현식을 지정하면 주어진 키워드와 일치하는 문서를 검색할 수 있습니다.</p>
<p>아래 예는 <code translate="no">text</code> 필드에 <code translate="no">keyword1</code> 과 <code translate="no">keyword2</code> 키워드를 모두 포함하는 문서를 검색합니다.</p>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># Match entities with both `keyword1` and `keyword2`​</span>
<span class="hljs-built_in">filter</span> = <span class="hljs-string">&quot;TEXT_MATCH(text, &#x27;keyword1&#x27;) and TEXT_MATCH(text, &#x27;keyword2&#x27;)&quot;</span>​
​
result = MilvusClient.query(​
    collection_name=<span class="hljs-string">&quot;YOUR_COLLECTION_NAME&quot;</span>,​
    <span class="hljs-built_in">filter</span>=<span class="hljs-built_in">filter</span>, ​
    output_fields=[<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-string">&quot;text&quot;</span>]​
)​

<button class="copy-code-btn"></button></code></pre>
<h2 id="Considerations" class="common-anchor-header">고려 사항<button data-href="#Considerations" class="anchor-icon" translate="no">
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
    </button></h2><ul>
<li><p>필드에 키워드 검색을 사용하도록 설정하면 역 인덱스가 생성되어 스토리지 리소스를 소모합니다. 이 기능을 사용하도록 설정할 때는 텍스트 크기, 고유 토큰 및 사용되는 분석기에 따라 달라지므로 스토리지 영향을 고려하세요.</p></li>
<li><p>스키마에서 분석기를 정의하면 해당 컬렉션에 대해 해당 설정이 영구적으로 적용됩니다. 다른 분석기가 필요에 더 적합하다고 판단되면 기존 컬렉션을 삭제하고 원하는 분석기 구성으로 새 컬렉션을 만들 수 있습니다.</p></li>
</ul>