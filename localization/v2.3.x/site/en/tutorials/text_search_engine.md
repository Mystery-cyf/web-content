---
id: text_search_engine.md
summary: Build a text search engine with Milvus.
title: Text Search Engine
---
<h1 id="Text-Search-Engine" class="common-anchor-header">Text Search Engine<button data-href="#Text-Search-Engine" class="anchor-icon" translate="no">
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
    </button></h1><p>In this tutorial, you will learn how to use Milvus, the open-source vector database, to build a text search engine.</p>
<ul>
<li><a href="https://github.com/towhee-io/examples/tree/main/nlp/text_search">Open Jupyter notebook</a></li>
</ul>
<p>The ML model and third-party software used include:</p>
<ul>
<li>BERT</li>
<li>MySQL</li>
<li><a href="https://towhee.io/">Towhee</a></li>
</ul>
<p><br/></p>
<p>One major application of Milvus in the field of natural language processing (NLP) is text search engine. It is a great tool that can help users find the information they are looking for. It can even surface information that is hard to find. Text search engines compare the keywords or semantics users input against a database of texts, and then return the results that meet certain criteria.</p>
<p><br/></p>
<p>In this tutorial, you will learn how to build a text search engine. This tutorial uses BERT to convert texts into fixed-length vectors. Milvus is used as a vector database for storage and vector similarity search. Then use MySQL to map the vector IDs generated by Milvus to the text data.</p>
<p><br/></p>
<p>
  <span class="img-wrapper">
    <img translate="no" src="/docs/v2.3.x/assets/text_search_engine.png" alt="text_search_engine" class="doc-image" id="text_search_engine" />
    <span>text_search_engine</span>
  </span>


  <span class="img-wrapper">
    <img translate="no" src="/docs/v2.3.x/assets/text_search_engine_demo.png" alt="text_search_engine" class="doc-image" id="text_search_engine" />
    <span>text_search_engine</span>
  </span>
</p>