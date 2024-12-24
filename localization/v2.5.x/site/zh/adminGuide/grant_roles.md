---
id: grant_roles.md
related_key: enable RBAC
summary: >-
  创建角色并授予角色权限后，就可以将角色授予用户，这样用户就可以访问资源并执行角色所定义的操作。可以向一个用户授予多个角色，也可以向多个用户授予一个角色。本指南将介绍如何向用户授予角色。
title: 向用户授予角色
---
<h1 id="Grant-Roles-to-Users​" class="common-anchor-header">向用户授予角色<button data-href="#Grant-Roles-to-Users​" class="anchor-icon" translate="no">
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
    </button></h1><p>创建角色并授予角色权限后，就可以将角色授予用户，这样用户就可以访问资源并执行角色所定义的操作。可以向一个用户授予多个角色，也可以向多个用户授予一个角色。本指南将介绍如何向用户授予角色。</p>
<p>milvus 中的内置用户<code translate="no">root</code> 已被授予<code translate="no">admin</code> 角色，该角色拥有所有权限。您不需要为其分配任何其他角色。</p>
<h2 id="Grant-a-role-to-a-user​" class="common-anchor-header">向用户授予角色<button data-href="#Grant-a-role-to-a-user​" class="anchor-icon" translate="no">
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
    </button></h2><p>下面的示例演示了如何向用户<code translate="no">user_1</code> 授予<code translate="no">role_a</code> 角色。</p>
<div class="multipleCode">
 <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#shell">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> <span class="hljs-title class_">MilvusClient</span>​
​
client = <span class="hljs-title class_">MilvusClient</span>(​
    uri=<span class="hljs-string">&quot;http://localhost:19530&quot;</span>,​
    token=<span class="hljs-string">&quot;root:Milvus&quot;</span>​
)​
​
client.<span class="hljs-title function_">grant_role</span>(user_name=<span class="hljs-string">&quot;user_1&quot;</span>, role_name=<span class="hljs-string">&quot;role_a&quot;</span>)​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.client.ConnectConfig;​
<span class="hljs-keyword">import</span> io.milvus.v2.client.MilvusClientV2;​
<span class="hljs-keyword">import</span> io.milvus.v2.service.rbac.request.GrantRoleReq;​
​
<span class="hljs-type">String</span> <span class="hljs-variable">CLUSTER_ENDPOINT</span> <span class="hljs-operator">=</span> <span class="hljs-string">&quot;http://localhost:19530&quot;</span>;​
<span class="hljs-type">String</span> <span class="hljs-variable">TOKEN</span> <span class="hljs-operator">=</span> <span class="hljs-string">&quot;root:Milvus&quot;</span>;​
​
​
<span class="hljs-type">ConnectConfig</span> <span class="hljs-variable">connectConfig</span> <span class="hljs-operator">=</span> ConnectConfig.builder()​
    .uri(CLUSTER_ENDPOINT)​
    .token(TOKEN)​
    .build();​
    ​
<span class="hljs-type">MilvusClientV2</span> <span class="hljs-variable">client</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">MilvusClientV2</span>(connectConfig);​
​
<span class="hljs-type">GrantRoleReq</span> <span class="hljs-variable">grantRoleReq</span> <span class="hljs-operator">=</span> GrantRoleReq.builder()​
        .roleName(<span class="hljs-string">&quot;role_a&quot;</span>)​
        .userName(<span class="hljs-string">&quot;user_1&quot;</span>)​
        .build();​
client.grantRole(grantRoleReq);​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> { <span class="hljs-title class_">MilvusClient</span>, <span class="hljs-title class_">DataType</span> } = <span class="hljs-built_in">require</span>(<span class="hljs-string">&quot;@zilliz/milvus2-sdk-node&quot;</span>)​
​
<span class="hljs-keyword">const</span> address = <span class="hljs-string">&quot;http://localhost:19530&quot;</span>;​
<span class="hljs-keyword">const</span> token = <span class="hljs-string">&quot;root:Milvus&quot;</span>;​
<span class="hljs-keyword">const</span> client = <span class="hljs-keyword">new</span> <span class="hljs-title class_">MilvusClient</span>({address, token});​
​
milvusClient.<span class="hljs-title function_">grantRole</span>({​
   <span class="hljs-attr">username</span>: <span class="hljs-string">&#x27;user_1&#x27;</span>,​
   <span class="hljs-attr">roleName</span>: <span class="hljs-string">&#x27;role_a&#x27;</span>​
 })​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell"><span class="hljs-built_in">export</span> CLUSTER_ENDPOINT=<span class="hljs-string">&quot;http://localhost:19530&quot;</span>​
<span class="hljs-built_in">export</span> TOKEN=<span class="hljs-string">&quot;root:Milvus&quot;</span>​
​
curl --request POST \​
--url <span class="hljs-string">&quot;<span class="hljs-variable">${CLUSTER_ENDPOINT}</span>/v2/vectordb/users/grant_role&quot;</span> \​
--header <span class="hljs-string">&quot;Authorization: Bearer <span class="hljs-variable">${TOKEN}</span>&quot;</span> \​
--header <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \​
-d <span class="hljs-string">&#x27;{​
    &quot;roleName&quot;: &quot;role_a&quot;,​
    &quot;userName&quot;: &quot;user_1&quot;​
}&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h2 id="Describe-user​" class="common-anchor-header">描述用户<button data-href="#Describe-user​" class="anchor-icon" translate="no">
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
    </button></h2><p>向用户授予角色后，可以通过<code translate="no">describe_user()</code> 方法检查授予操作是否成功。</p>
<p>下面的示例演示了如何检查用户<code translate="no">user_1</code> 的角色。</p>
<div class="multipleCode">
 <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#shell">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> <span class="hljs-title class_">MilvusClient</span>​
​
client.<span class="hljs-title function_">describe_user</span>(user_name=<span class="hljs-string">&quot;user_1&quot;</span>)​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.service.rbac.request.DescribeUserReq;​
<span class="hljs-keyword">import</span> io.milvus.v2.service.rbac.response.DescribeUserResp;​
​
<span class="hljs-type">DescribeUserReq</span> <span class="hljs-variable">describeUserReq</span> <span class="hljs-operator">=</span> DescribeUserReq.builder()​
        .userName(<span class="hljs-string">&quot;user_1&quot;</span>)​
        .build();​
<span class="hljs-type">DescribeUserResp</span> <span class="hljs-variable">describeUserResp</span> <span class="hljs-operator">=</span> client.describeUser(describeUserReq);​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> { <span class="hljs-title class_">MilvusClient</span>, <span class="hljs-title class_">DataType</span> } = <span class="hljs-built_in">require</span>(<span class="hljs-string">&quot;@zilliz/milvus2-sdk-node&quot;</span>)​
​
milvusClient.<span class="hljs-title function_">describeUser</span>({<span class="hljs-attr">username</span>: <span class="hljs-string">&#x27;user_1&#x27;</span>})​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell">curl --request POST \​
--url <span class="hljs-string">&quot;<span class="hljs-variable">${CLUSTER_ENDPOINT}</span>/v2/vectordb/users/describe&quot;</span> \​
--header <span class="hljs-string">&quot;Authorization: Bearer <span class="hljs-variable">${TOKEN}</span>&quot;</span> \​
--header <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \​
-d <span class="hljs-string">&#x27;{​
    &quot;userName&quot;: &quot;user_1&quot;​
}&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<p>下面是一个输出示例。</p>
<pre><code translate="no">{<span class="hljs-string">&#x27;user_name&#x27;</span>: <span class="hljs-string">&#x27;user_1&#x27;</span>, <span class="hljs-string">&#x27;roles&#x27;</span>: <span class="hljs-string">&#x27;role_a&#x27;</span>}​

<button class="copy-code-btn"></button></code></pre>
<h2 id="Revoke-a-role​" class="common-anchor-header">撤销角色<button data-href="#Revoke-a-role​" class="anchor-icon" translate="no">
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
    </button></h2><p>您还可以撤销已分配给用户的角色。</p>
<p>下面的示例演示了如何撤销分配给用户<code translate="no">role_a</code> 的角色<code translate="no">user_1</code> 。</p>
<div class="multipleCode">
 <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#shell">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> <span class="hljs-title class_">MilvusClient</span>​
​
client.<span class="hljs-title function_">revoke_role</span>(​
    user_name=<span class="hljs-string">&#x27;user_1&#x27;</span>,​
    role_name=<span class="hljs-string">&#x27;role_a&#x27;</span>​
)​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.<span class="hljs-property">milvus</span>.<span class="hljs-property">v2</span>.<span class="hljs-property">service</span>.<span class="hljs-property">rbac</span>.<span class="hljs-property">request</span>.<span class="hljs-property">RevokeRoleReq</span>;​
​
client.<span class="hljs-title function_">revokeRole</span>(<span class="hljs-title class_">RevokeRoleReq</span>.<span class="hljs-title function_">builder</span>()​
        .<span class="hljs-title function_">userName</span>(<span class="hljs-string">&quot;user_1&quot;</span>)​
        .<span class="hljs-title function_">roleName</span>(<span class="hljs-string">&quot;role_a&quot;</span>)​
        .<span class="hljs-title function_">build</span>());​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> { <span class="hljs-title class_">MilvusClient</span>, <span class="hljs-title class_">DataType</span> } = <span class="hljs-built_in">require</span>(<span class="hljs-string">&quot;@zilliz/milvus2-sdk-node&quot;</span>)​
​
​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell">curl --request POST \​
--url <span class="hljs-string">&quot;<span class="hljs-variable">${CLUSTER_ENDPOINT}</span>/v2/vectordb/users/revoke_role&quot;</span> \​
--header <span class="hljs-string">&quot;Authorization: Bearer <span class="hljs-variable">${TOKEN}</span>&quot;</span> \​
--header <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \​
-d <span class="hljs-string">&#x27;{​
    &quot;userName&quot;: &quot;user_1&quot;,​
    &quot;roleName&quot;: &quot;role_a&quot;​
}&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>