---
id: embed-with-jina.md
order: 8
summary: >-
  Este artículo describe cómo utilizar JinaEmbeddingFunction para codificar
  documentos y consultas utilizando el modelo de incrustación de Jina AI.
title: Jina AI - Integrar
---
<h1 id="Jina-AI" class="common-anchor-header">Jina AI<button data-href="#Jina-AI" class="anchor-icon" translate="no">
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
    </button></h1><p>Los modelos de incrustación de Jina AI son modelos de incrustación de texto de alto rendimiento que pueden traducir entradas textuales en representaciones numéricas, capturando la semántica del texto. Estos modelos destacan en aplicaciones como la recuperación densa, la similitud semántica textual y la comprensión multilingüe.</p>
<p>Milvus se integra con los modelos de incrustación de Jina AI a través de la clase <code translate="no">JinaEmbeddingFunction</code>. Esta clase proporciona métodos para codificar documentos y consultas utilizando los modelos de incrustación de Jina AI y devolviendo las incrustaciones como vectores densos compatibles con la indexación de Milvus. Para utilizar esta funcionalidad, obtenga una clave API de <a href="https://jina.ai/embeddings/">Jina AI</a>.</p>
<p>Para utilizar esta función, instale las dependencias necesarias:</p>
<pre><code translate="no" class="language-bash">pip install --upgrade pymilvus
pip install <span class="hljs-string">&quot;pymilvus[model]&quot;</span>
<button class="copy-code-btn"></button></code></pre>
<p>A continuación, instancie <code translate="no">JinaEmbeddingFunction</code>:</p>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus.model.dense <span class="hljs-keyword">import</span> JinaEmbeddingFunction

jina_ef = JinaEmbeddingFunction(
    model_name=<span class="hljs-string">&quot;jina-embeddings-v2-base-en&quot;</span>, <span class="hljs-comment"># Defaults to `jina-embeddings-v2-base-en`</span>
    api_key=JINAAI_API_KEY <span class="hljs-comment"># Provide your Jina AI API key</span>
)
<button class="copy-code-btn"></button></code></pre>
<p><strong>Parámetros</strong>:</p>
<ul>
<li><p><code translate="no">model_name</code> <em>(cadena</em>)</p>
<p>Nombre del modelo de incrustación de Jina AI que se utilizará para la codificación. Puede especificar cualquiera de los nombres de modelo de incrustación de Jina AI disponibles, por ejemplo, <code translate="no">jina-embeddings-v2-base-en</code>, <code translate="no">jina-embeddings-v2-small-en</code>, etc. Si deja este parámetro sin especificar, se utilizará <code translate="no">jina-embeddings-v2-base-en</code>. Para obtener una lista de los modelos disponibles, consulte <a href="https://jina.ai/embeddings">Jina Embeddings</a>.</p></li>
<li><p><code translate="no">api_key</code> <em>(cadena</em>)</p>
<p>La clave API para acceder a la API de Jina AI.</p></li>
</ul>
<p>Para crear incrustaciones para documentos, utilice el método <code translate="no">encode_documents()</code>:</p>
<pre><code translate="no" class="language-python">docs = [
    <span class="hljs-string">&quot;Artificial intelligence was founded as an academic discipline in 1956.&quot;</span>,
    <span class="hljs-string">&quot;Alan Turing was the first person to conduct substantial research in AI.&quot;</span>,
    <span class="hljs-string">&quot;Born in Maida Vale, London, Turing was raised in southern England.&quot;</span>,
]

docs_embeddings = jina_ef.encode_documents(docs)

<span class="hljs-comment"># Print embeddings</span>
<span class="hljs-built_in">print</span>(<span class="hljs-string">&quot;Embeddings:&quot;</span>, docs_embeddings)
<span class="hljs-comment"># Print dimension and shape of embeddings</span>
<span class="hljs-built_in">print</span>(<span class="hljs-string">&quot;Dim:&quot;</span>, jina_ef.dim, docs_embeddings[<span class="hljs-number">0</span>].shape)
<button class="copy-code-btn"></button></code></pre>
<p>El resultado esperado es similar al siguiente:</p>
<pre><code translate="no" class="language-python">Embeddings: [array([-4.88487840e-01, -4.28095880e-01,  4.90086500e-01, -1.63274320e-01,
        3.43437800e-01,  3.21476880e-01,  2.83173790e-02, -3.10403670e-01,
        4.76985040e-01, -1.77410420e-01, -3.84803180e-01, -2.19224200e-01,
       -2.52898000e-01,  6.62411900e-02, -8.58173100e-01,  1.05221800e+00,
...
       -2.04462400e-01,  7.14229800e-01, -1.66823000e-01,  8.72551440e-01,
        5.53560140e-01,  8.92506300e-01, -2.39408610e-01, -4.22413560e-01,
       -3.19551350e-01,  5.59153850e-01,  2.44338100e-01, -8.60452100e-01])]
Dim: 768 (768,)
<button class="copy-code-btn"></button></code></pre>
<p>Para crear incrustaciones para consultas, utilice el método <code translate="no">encode_queries()</code>:</p>
<pre><code translate="no" class="language-python">queries = [<span class="hljs-string">&quot;When was artificial intelligence founded&quot;</span>, 
           <span class="hljs-string">&quot;Where was Alan Turing born?&quot;</span>]

query_embeddings = jina_ef.encode_queries(queries)

<span class="hljs-built_in">print</span>(<span class="hljs-string">&quot;Embeddings:&quot;</span>, query_embeddings)
<span class="hljs-built_in">print</span>(<span class="hljs-string">&quot;Dim&quot;</span>, jina_ef.dim, query_embeddings[<span class="hljs-number">0</span>].shape)
<button class="copy-code-btn"></button></code></pre>
<p>El resultado esperado es similar al siguiente:</p>
<pre><code translate="no" class="language-python">Embeddings: [array([-5.99164660e-01, -3.49827350e-01,  8.22405160e-01, -1.18632730e-01,
        5.78107540e-01,  1.09789170e-01,  2.91604200e-01, -3.29306450e-01,
        2.93779640e-01, -2.17880800e-01, -6.84535440e-01, -3.79752000e-01,
       -3.47541800e-01,  9.20846100e-02, -6.13804400e-01,  6.31312800e-01,
...
       -1.84993740e-02,  9.38629150e-01,  2.74858470e-02,  1.09396360e+00,
        3.96270750e-01,  7.44445800e-01, -1.95404050e-01, -6.08383200e-01,
       -3.75076300e-01,  3.87512200e-01,  8.11889650e-01, -3.76407620e-01])]
Dim 768 (768,)
<button class="copy-code-btn"></button></code></pre>