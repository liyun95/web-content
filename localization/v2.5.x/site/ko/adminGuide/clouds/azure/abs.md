---
id: abs.md
title: 워크로드 아이덴티티로 블롭 스토리지 액세스 구성하기
related_key: 'blob storage, workload identity, iam'
summary: 워크로드 아이덴티티로 Blob 스토리지를 구성하는 방법을 알아보세요.
---
<h1 id="Configure-Blob-Storage-Access-by-Workload-Identity" class="common-anchor-header">워크로드 아이덴티티로 블롭 스토리지 액세스 구성하기<button data-href="#Configure-Blob-Storage-Access-by-Workload-Identity" class="anchor-icon" translate="no">
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
    </button></h1><p>이 항목에서는 헬름과 함께 Milvus를 설치할 때 Workload Identity를 통해 Azure Blob Storage 액세스를 구성하는 방법을 소개합니다. 자세한 내용은 <a href="https://azure.github.io/azure-workload-identity/docs/introduction.html">Workload Identity를</a> 참조하세요.</p>
<h2 id="Configure-applications-to-use-Workload-Identity" class="common-anchor-header">워크로드 아이덴티티를 사용하도록 애플리케이션 구성<button data-href="#Configure-applications-to-use-Workload-Identity" class="anchor-icon" translate="no">
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
<li>환경 설정.</li>
</ul>
<pre><code translate="no" class="language-bash"><span class="hljs-keyword">export</span> <span class="hljs-variable constant_">RESOURCE_GROUP</span>=<span class="hljs-string">&quot;&lt;your resource group&gt;&quot;</span>
<span class="hljs-keyword">export</span> <span class="hljs-variable constant_">AKS_CLUSTER</span>=<span class="hljs-string">&quot;&lt;your aks cluster name&gt;&quot;</span> 
<span class="hljs-keyword">export</span> <span class="hljs-variable constant_">SUB_ID</span>=<span class="hljs-string">&quot;&lt;your Subscription ID&gt;&quot;</span>
<span class="hljs-keyword">export</span> <span class="hljs-variable constant_">USER_ASSIGNED_IDENTITY_NAME</span>=<span class="hljs-string">&quot;workload-identity&quot;</span>
<span class="hljs-keyword">export</span> <span class="hljs-variable constant_">SERVICE_ACCOUNT_NAME</span>=<span class="hljs-string">&quot;milvus-abs-access-sa&quot;</span>
<span class="hljs-keyword">export</span> <span class="hljs-variable constant_">STORAGE_ACCOUNT_NAME</span>=<span class="hljs-string">&quot;milvustesting1&quot;</span>
<span class="hljs-keyword">export</span> <span class="hljs-variable constant_">CONTAINER_NAME</span>=<span class="hljs-string">&quot;testmilvus&quot;</span>
<span class="hljs-keyword">export</span> <span class="hljs-variable constant_">LOCATION</span>=<span class="hljs-string">&quot;&lt;your location&gt;&quot;</span>
<span class="hljs-keyword">export</span> <span class="hljs-variable constant_">SERVICE_ACCOUNT_NAMESPACE</span>=<span class="hljs-string">&quot;default&quot;</span>
<button class="copy-code-btn"></button></code></pre>
<ul>
<li>OIDC 발급자 및 워크로드 아이덴티티로 AKS 클러스터를 업데이트합니다.</li>
</ul>
<pre><code translate="no" class="language-bash">az aks update -g <span class="hljs-variable">${RESOURCE_GROUP}</span> -n <span class="hljs-variable">${AKS_CLUSTER}</span> --enable-oidc-issuer --enable-workload-identity
<button class="copy-code-btn"></button></code></pre>
<ul>
<li>OIDC 발급자 URL을 가져옵니다.</li>
</ul>
<pre><code translate="no" class="language-bash"><span class="hljs-built_in">export</span> SERVICE_ACCOUNT_ISSUER=<span class="hljs-string">&quot;<span class="hljs-subst">$(az aks show --resource-group ${RESOURCE_GROUP} --name ${AKS_CLUSTER} --query &#x27;oidcIssuerProfile.issuerUrl&#x27; -otsv)</span>&quot;</span>
<button class="copy-code-btn"></button></code></pre>
<ul>
<li>스토리지 계정 및 컨테이너를 생성합니다.</li>
</ul>
<pre><code translate="no" class="language-bash">az storage account create -n <span class="hljs-variable">${STORAGE_ACCOUNT_NAME}</span> -g <span class="hljs-variable">${RESOURCE_GROUP}</span> -l <span class="hljs-variable">$LOCATION</span> --sku Standard_LRS --min-tls-version TLS1_2
az storage container create -n <span class="hljs-variable">${CONTAINER_NAME}</span> --account-name <span class="hljs-variable">${STORAGE_ACCOUNT_NAME}</span>

<button class="copy-code-btn"></button></code></pre>
<ul>
<li>사용자 할당 관리 ID를 생성하고 역할을 할당합니다.</li>
</ul>
<pre><code translate="no" class="language-bash">az identity create --name <span class="hljs-string">&quot;<span class="hljs-variable">${USER_ASSIGNED_IDENTITY_NAME}</span>&quot;</span> --resource-group <span class="hljs-string">&quot;<span class="hljs-variable">${RESOURCE_GROUP}</span>&quot;</span>
<span class="hljs-built_in">export</span> USER_ASSIGNED_IDENTITY_CLIENT_ID=<span class="hljs-string">&quot;<span class="hljs-subst">$(az identity show --name <span class="hljs-string">&quot;<span class="hljs-variable">${USER_ASSIGNED_IDENTITY_NAME}</span>&quot;</span> --resource-group <span class="hljs-string">&quot;<span class="hljs-variable">${RESOURCE_GROUP}</span>&quot;</span> --query &#x27;clientId&#x27; -otsv)</span>&quot;</span>
<span class="hljs-built_in">export</span> USER_ASSIGNED_IDENTITY_OBJECT_ID=<span class="hljs-string">&quot;<span class="hljs-subst">$(az identity show --name <span class="hljs-string">&quot;<span class="hljs-variable">${USER_ASSIGNED_IDENTITY_NAME}</span>&quot;</span> --resource-group <span class="hljs-string">&quot;<span class="hljs-variable">${RESOURCE_GROUP}</span>&quot;</span> --query &#x27;principalId&#x27; -otsv)</span>&quot;</span>
az role assignment create --role <span class="hljs-string">&quot;Storage Blob Data Contributor&quot;</span> --assignee <span class="hljs-string">&quot;<span class="hljs-variable">${USER_ASSIGNED_IDENTITY_OBJECT_ID}</span>&quot;</span> --scope <span class="hljs-string">&quot;/subscriptions/<span class="hljs-variable">${SUB_ID}</span>/resourceGroups/<span class="hljs-variable">${RESOURCE_GROUP}</span>/providers/Microsoft.Storage/storageAccounts/<span class="hljs-variable">${STORAGE_ACCOUNT_NAME}</span>&quot;</span>

<button class="copy-code-btn"></button></code></pre>
<ul>
<li>서비스 계정을 생성합니다.</li>
</ul>
<pre><code translate="no" class="language-bash"><span class="hljs-built_in">cat</span> &lt;&lt;<span class="hljs-string">EOF | kubectl apply -f -
apiVersion: v1
kind: ServiceAccount
metadata:
  annotations:
    azure.workload.identity/client-id: ${USER_ASSIGNED_IDENTITY_CLIENT_ID}
  name: ${SERVICE_ACCOUNT_NAME}
EOF</span>
<button class="copy-code-btn"></button></code></pre>
<ul>
<li>ID와 서비스 계정 발급자 및 주체 간에 페더레이션된 ID 자격 증명을 설정합니다.</li>
</ul>
<pre><code translate="no" class="language-bash">az identity federated-credential create \
  --name <span class="hljs-string">&quot;kubernetes-federated-credential&quot;</span> \
  --identity-name <span class="hljs-string">&quot;<span class="hljs-variable">${USER_ASSIGNED_IDENTITY_NAME}</span>&quot;</span> \
  --resource-group <span class="hljs-string">&quot;<span class="hljs-variable">${RESOURCE_GROUP}</span>&quot;</span> \
  --issuer <span class="hljs-string">&quot;<span class="hljs-variable">${SERVICE_ACCOUNT_ISSUER}</span>&quot;</span> \
  --subject <span class="hljs-string">&quot;system:serviceaccount:<span class="hljs-variable">${SERVICE_ACCOUNT_NAMESPACE}</span>:<span class="hljs-variable">${SERVICE_ACCOUNT_NAME}</span>&quot;</span>
<button class="copy-code-btn"></button></code></pre>
<h2 id="Deploy-Milvus" class="common-anchor-header">Milvus 배포<button data-href="#Deploy-Milvus" class="anchor-icon" translate="no">
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
    </button></h2><pre><code translate="no" class="language-bash">helm install -f values.yaml my-release milvus/milvus
<button class="copy-code-btn"></button></code></pre>
<p>values.yaml 콘텐츠를 배포합니다:</p>
<pre><code translate="no" class="language-yaml">cluster:
  enabled: <span class="hljs-literal">true</span>

service:
  <span class="hljs-built_in">type</span>: LoadBalancer

extraConfigFiles:
  user.yaml: |+
    common:
      storageType: remote

minio:
  enabled: <span class="hljs-literal">false</span>

labels:
  azure.workload.identity/use: <span class="hljs-string">&quot;true&quot;</span>

serviceAccount:
  create: <span class="hljs-literal">false</span>
  name: milvus-abs-access-sa <span class="hljs-comment"># SERVICE_ACCOUNT_NAME</span>

externalS3:
  enabled: <span class="hljs-literal">true</span>
  host: core.windows.net
  port: 443
  rootPath: my-release
  bucketName: testmilvus <span class="hljs-comment"># CONTAINER_NAME</span>
  cloudProvider: azure
  useSSL: <span class="hljs-literal">true</span>
  useIAM: <span class="hljs-literal">true</span>
  accessKey: <span class="hljs-string">&quot;milvustesting1&quot;</span> <span class="hljs-comment"># STORAGE_ACCOUNT_NAME</span>
  secretKey: <span class="hljs-string">&quot;&quot;</span>
<button class="copy-code-btn"></button></code></pre>