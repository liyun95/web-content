---
id: alphanumonly-filter.md
title: Filtro solo alfanumerico
summary: >-
  Il filtro `alphanumonly` rimuove i token che contengono caratteri non ASCII,
  mantenendo solo i termini alfanumerici. Questo filtro è utile per elaborare
  testi in cui sono rilevanti solo lettere e numeri di base, escludendo
  caratteri speciali o simboli.
---
<h1 id="Alphanumonly​" class="common-anchor-header">Solo alfanumerico<button data-href="#Alphanumonly​" class="anchor-icon" translate="no">
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
    </button></h1><p>Il filtro <code translate="no">alphanumonly</code> rimuove i token che contengono caratteri non ASCII, mantenendo solo i termini alfanumerici. Questo filtro è utile per l'elaborazione di testi in cui sono rilevanti solo lettere e numeri di base, escludendo caratteri speciali o simboli.</p>
<h2 id="Configuration​" class="common-anchor-header">Configurazione<button data-href="#Configuration​" class="anchor-icon" translate="no">
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
    </button></h2><p>Il filtro <code translate="no">alphanumonly</code> è integrato in Milvus. Per utilizzarlo, è sufficiente specificarne il nome nella sezione <code translate="no">filter</code> all'interno di <code translate="no">analyzer_params</code>.</p>
<pre><code translate="no" class="language-python">analyzer_params = {​
    <span class="hljs-string">&quot;tokenizer&quot;</span>: <span class="hljs-string">&quot;standard&quot;</span>,​
    <span class="hljs-string">&quot;filter&quot;</span>: [<span class="hljs-string">&quot;alphanumonly&quot;</span>],​
}​
<button class="copy-code-btn"></button></code></pre>
<p>Il filtro <code translate="no">alphanumonly</code> opera sui termini generati dal tokenizer, quindi deve essere usato in combinazione con un tokenizer.</p>
<p>Dopo aver definito <code translate="no">analyzer_params</code>, è possibile applicarli a un campo <code translate="no">VARCHAR</code> quando si definisce uno schema di raccolta. Ciò consente a Milvus di elaborare il testo in quel campo utilizzando l'analizzatore specificato per una tokenizzazione e un filtraggio efficienti. Per i dettagli, vedere <a href="/docs/it/analyzer-overview.md#Example-use">Esempio di utilizzo</a>.</p>
<h2 id="Example-output​" class="common-anchor-header">Esempio di output<button data-href="#Example-output​" class="anchor-icon" translate="no">
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
    </button></h2><p>Ecco un esempio di come il filtro <code translate="no">alphanumonly</code> elabora il testo.</p>
<p><strong>Testo originale</strong>.</p>
<pre><code translate="no" class="language-python"><span class="hljs-string">&quot;Milvus 2.0 @ Scale! #AI #Vector_Databasé&quot;</span>​
<button class="copy-code-btn"></button></code></pre>
<p><strong>Risultato atteso</strong>.</p>
<pre><code translate="no" class="language-python">[<span class="hljs-string">&quot;Milvus&quot;</span>, <span class="hljs-string">&quot;2&quot;</span>, <span class="hljs-string">&quot;0&quot;</span>, <span class="hljs-string">&quot;Scale&quot;</span>, <span class="hljs-string">&quot;AI&quot;</span>, <span class="hljs-string">&quot;Vector&quot;</span>]​
<button class="copy-code-btn"></button></code></pre>