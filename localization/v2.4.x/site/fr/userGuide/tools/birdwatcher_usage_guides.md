---
id: birdwatcher_usage_guides.md
summary: Apprenez à utiliser Birdwatch pour déboguer Milvus.
title: Utiliser Birdwatcher
---
<h1 id="Use-Birdwatcher" class="common-anchor-header">Utiliser Birdwatcher<button data-href="#Use-Birdwatcher" class="anchor-icon" translate="no">
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
    </button></h1><p>Ce guide vous explique comment utiliser Birdwatcher pour vérifier l'état de votre Milvus et le configurer à la volée.</p>
<h2 id="Start-Birdwatcher" class="common-anchor-header">Démarrer Birdwatcher<button data-href="#Start-Birdwatcher" class="anchor-icon" translate="no">
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
    </button></h2><p>Birdwatcher est un outil de ligne de commande, vous pouvez le démarrer comme suit :</p>
<pre><code translate="no" class="language-shell">./birdwatcher
<button class="copy-code-btn"></button></code></pre>
<p>Vous serez alors accueilli par l'invite suivante :</p>
<pre><code translate="no" class="language-shell">Offline &gt;
<button class="copy-code-btn"></button></code></pre>
<h2 id="Connect-to-etcd" class="common-anchor-header">Se connecter à etcd<button data-href="#Connect-to-etcd" class="anchor-icon" translate="no">
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
    </button></h2><p>Vous devez utiliser Birdwatcher pour vous connecter à etcd avant toute autre opération.</p>
<ul>
<li><p>Se connecter avec les paramètres par défaut</p>
<pre><code translate="no" class="language-shell">Offline &gt; connect
<span class="hljs-title function_">Milvus</span><span class="hljs-params">(by-dev)</span> &gt;
<button class="copy-code-btn"></button></code></pre></li>
<li><p>Se connecter depuis Birdwatcher dans un pod</p>
<p>Si vous choisissez d'exécuter Birdwatcher dans un pod Kubernetes, vous devez d'abord obtenir l'adresse IP d'etcd comme suit :</p>
<pre><code translate="no" class="language-shell">kubectl <span class="hljs-keyword">get</span> pod my-release-etcd<span class="hljs-number">-0</span> -o <span class="hljs-string">&#x27;jsonpath={.status.podIP}&#x27;</span>
<button class="copy-code-btn"></button></code></pre>
<p>Accédez ensuite au shell du pod.</p>
<pre><code translate="no" class="language-shell">kubectl <span class="hljs-built_in">exec</span> --stdin --<span class="hljs-built_in">tty</span> birdwatcher-7f48547ddc-zcbxj -- /bin/sh
<button class="copy-code-btn"></button></code></pre>
<p>Enfin, utilisez l'adresse IP renvoyée pour vous connecter à etcd comme suit :</p>
<pre><code translate="no" class="language-shell">Offline &gt; connect --etcd <span class="hljs-variable">${ETCD_IP_ADDR}</span>:2379
Milvus(by-dev)
<button class="copy-code-btn"></button></code></pre></li>
<li><p>Se connecter avec un chemin racine différent</p>
<p>Si le chemin d'accès à la racine de votre Milvus est différent de <code translate="no">by-dev</code> et qu'un message d'erreur vous signale un chemin d'accès à la racine incorrect, vous pouvez vous connecter à etcd comme suit :</p>
<pre><code translate="no" class="language-shell">Offline &gt; connect --rootPath my-release
<span class="hljs-title function_">Milvus</span><span class="hljs-params">(my-release)</span> &gt;
<button class="copy-code-btn"></button></code></pre>
<p>Si vous ne connaissez pas le chemin racine de votre Milvus, connectez-vous à etcd comme suit :</p>
<pre><code translate="no" class="language-shell">Offline &gt; connect --dry
using dry mode, ignore rootPath and metaPath
<span class="hljs-title function_">Etcd</span><span class="hljs-params">(<span class="hljs-number">127.0</span><span class="hljs-number">.0</span><span class="hljs-number">.1</span>:<span class="hljs-number">2379</span>)</span> &gt; find-milvus
<span class="hljs-number">1</span> candidates found:
my-release
<span class="hljs-title function_">Etcd</span><span class="hljs-params">(<span class="hljs-number">127.0</span><span class="hljs-number">.0</span><span class="hljs-number">.1</span>:<span class="hljs-number">2379</span>)</span> &gt; use my-release
<span class="hljs-title function_">Milvus</span><span class="hljs-params">(my-release)</span> &gt;
<button class="copy-code-btn"></button></code></pre></li>
</ul>
<h2 id="Check-Milvus-status" class="common-anchor-header">Vérifier l'état de Milvus<button data-href="#Check-Milvus-status" class="anchor-icon" translate="no">
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
    </button></h2><p>Vous pouvez utiliser les commandes <code translate="no">show</code> pour vérifier l'état du Milvus.</p>
<pre><code translate="no" class="language-shell">Milvus(my-release) &gt; show -h
Usage:
   show [command]

Available Commands:
  alias               <span class="hljs-built_in">list</span> alias meta info
  channel-watch       display channel watching info <span class="hljs-keyword">from</span> data coord meta store
  checkpoint          <span class="hljs-built_in">list</span> checkpoint collection vchannels
  collection-history  display collection change history
  collection-loaded   display information of loaded collection <span class="hljs-keyword">from</span> querycoord
  collections         <span class="hljs-built_in">list</span> current available collection <span class="hljs-keyword">from</span> RootCoord
  config-etcd         <span class="hljs-built_in">list</span> configuations <span class="hljs-built_in">set</span> by etcd source
  configurations      iterate <span class="hljs-built_in">all</span> online components <span class="hljs-keyword">and</span> inspect configuration
  current-version     
  database            display Database info <span class="hljs-keyword">from</span> rootcoord meta
  index               
  partition           <span class="hljs-built_in">list</span> partitions of provided collection
  querycoord-channel  display querynode information <span class="hljs-keyword">from</span> querycoord cluster
  querycoord-cluster  display querynode information <span class="hljs-keyword">from</span> querycoord cluster
  querycoord-task     display task information <span class="hljs-keyword">from</span> querycoord
  replica             <span class="hljs-built_in">list</span> current replica information <span class="hljs-keyword">from</span> QueryCoord
  segment             display segment information <span class="hljs-keyword">from</span> data coord meta store
  segment-index       display segment index information
  segment-loaded      display segment information <span class="hljs-keyword">from</span> querycoordv1 meta
  segment-loaded-grpc <span class="hljs-built_in">list</span> segments loaded information
  session             <span class="hljs-built_in">list</span> online milvus components

Flags:
  -h, --<span class="hljs-built_in">help</span>   <span class="hljs-built_in">help</span> <span class="hljs-keyword">for</span> show

Use <span class="hljs-string">&quot; show [command] --help&quot;</span> <span class="hljs-keyword">for</span> more information about a command.
<button class="copy-code-btn"></button></code></pre>
<h3 id="List-sessions" class="common-anchor-header">Répertorier les sessions</h3><p>Pour répertorier les sessions associées à différents composants dans Milvus :</p>
<pre><code translate="no" class="language-shell">Milvus(<span class="hljs-keyword">by</span>-dev) &gt; show session
Session:datacoord, ServerID: <span class="hljs-number">3</span>, Version: <span class="hljs-number">2.2</span><span class="hljs-number">.11</span>, Address: <span class="hljs-number">10.244</span><span class="hljs-number">.0</span><span class="hljs-number">.8</span>:<span class="hljs-number">13333</span>
Session:datanode, ServerID: <span class="hljs-number">6</span>, Version: <span class="hljs-number">2.2</span><span class="hljs-number">.11</span>, Address: <span class="hljs-number">10.244</span><span class="hljs-number">.0</span><span class="hljs-number">.8</span>:<span class="hljs-number">21124</span>
Session:indexcoord, ServerID: <span class="hljs-number">4</span>, Version: <span class="hljs-number">2.2</span><span class="hljs-number">.11</span>, Address: <span class="hljs-number">10.244</span><span class="hljs-number">.0</span><span class="hljs-number">.8</span>:<span class="hljs-number">31000</span>
Session:indexnode, ServerID: <span class="hljs-number">5</span>, Version: <span class="hljs-number">2.2</span><span class="hljs-number">.11</span>, Address: <span class="hljs-number">10.244</span><span class="hljs-number">.0</span><span class="hljs-number">.8</span>:<span class="hljs-number">21121</span>
Session:proxy, ServerID: <span class="hljs-number">8</span>, Version: <span class="hljs-number">2.2</span><span class="hljs-number">.11</span>, Address: <span class="hljs-number">10.244</span><span class="hljs-number">.0</span><span class="hljs-number">.8</span>:<span class="hljs-number">19529</span>
Session:querycoord, ServerID: <span class="hljs-number">7</span>, Version: <span class="hljs-number">2.2</span><span class="hljs-number">.11</span>, Address: <span class="hljs-number">10.244</span><span class="hljs-number">.0</span><span class="hljs-number">.8</span>:<span class="hljs-number">19531</span>
Session:querynode, ServerID: <span class="hljs-number">2</span>, Version: <span class="hljs-number">2.2</span><span class="hljs-number">.11</span>, Address: <span class="hljs-number">10.244</span><span class="hljs-number">.0</span><span class="hljs-number">.8</span>:<span class="hljs-number">21123</span>
Session:rootcoord, ServerID: <span class="hljs-number">1</span>, Version: <span class="hljs-number">2.2</span><span class="hljs-number">.11</span>, Address: <span class="hljs-number">10.244</span><span class="hljs-number">.0</span><span class="hljs-number">.8</span>:<span class="hljs-number">53100</span>
<button class="copy-code-btn"></button></code></pre>
<p>Dans la sortie de la commande, chaque entrée de session répertoriée par <code translate="no">show session</code> correspond à un nœud ou à un service actuellement actif et enregistré dans <strong>etcd.</strong></p>
<h3 id="Check-databases-and-collections" class="common-anchor-header">Vérifier les bases de données et les collections</h3><p>Vous pouvez répertorier toutes les bases de données et collections.</p>
<ul>
<li><p>Lister les bases de données</p>
<p>Dans la sortie de la commande, vous trouverez des informations sur chaque base de données.</p>
<pre><code translate="no" class="language-shell">Milvus(by-dev) &gt; show database
=============================
ID: <span class="hljs-number">1</span>   Name: <span class="hljs-keyword">default</span>
TenantID:        State: DatabaseCreated
--- Total <span class="hljs-title function_">Database</span><span class="hljs-params">(s)</span>: <span class="hljs-number">1</span>
<button class="copy-code-btn"></button></code></pre></li>
<li><p>Lister les collections</p>
<p>Dans la sortie de la commande, vous trouverez des informations détaillées sur chaque collection.</p>
<pre><code translate="no" class="language-shell">Milvus(by-dev) &gt; show collections
================================================================================
DBID: <span class="hljs-number">1</span>
Collection ID: <span class="hljs-number">443407225551410746</span>       Collection Name: medium_articles_2020
Collection State: CollectionCreated     Create Time: <span class="hljs-number">2023</span>-08-08 09:<span class="hljs-number">27</span>:08
Fields:
- Field ID: <span class="hljs-number">0</span>   Field Name: RowID       Field <span class="hljs-type">Type</span>: Int64
- Field ID: <span class="hljs-number">1</span>   Field Name: Timestamp   Field <span class="hljs-type">Type</span>: Int64
- Field ID: <span class="hljs-number">100</span>         Field Name: <span class="hljs-built_in">id</span>          Field <span class="hljs-type">Type</span>: Int64
        - Primary Key: true, AutoID: false
- Field ID: <span class="hljs-number">101</span>         Field Name: title       Field <span class="hljs-type">Type</span>: VarChar
        - <span class="hljs-type">Type</span> Param max_length: <span class="hljs-number">512</span>
- Field ID: <span class="hljs-number">102</span>         Field Name: title_vector        Field <span class="hljs-type">Type</span>: FloatVector
        - <span class="hljs-type">Type</span> Param dim: <span class="hljs-number">768</span>
- Field ID: <span class="hljs-number">103</span>         Field Name: link        Field <span class="hljs-type">Type</span>: VarChar
        - <span class="hljs-type">Type</span> Param max_length: <span class="hljs-number">512</span>
- Field ID: <span class="hljs-number">104</span>         Field Name: reading_time        Field <span class="hljs-type">Type</span>: Int64
- Field ID: <span class="hljs-number">105</span>         Field Name: publication         Field <span class="hljs-type">Type</span>: VarChar
        - <span class="hljs-type">Type</span> Param max_length: <span class="hljs-number">512</span>
- Field ID: <span class="hljs-number">106</span>         Field Name: claps       Field <span class="hljs-type">Type</span>: Int64
- Field ID: <span class="hljs-number">107</span>         Field Name: responses   Field <span class="hljs-type">Type</span>: Int64
Enable Dynamic Schema: false
Consistency Level: Bounded
Start position <span class="hljs-keyword">for</span> channel by-dev-rootcoord-dml_0(by-dev-rootcoord-dml_0_443407225551410746v0): [<span class="hljs-number">1</span> <span class="hljs-number">0</span> <span class="hljs-number">28</span> <span class="hljs-number">175</span> <span class="hljs-number">133</span> <span class="hljs-number">76</span> <span class="hljs-number">39</span> <span class="hljs-number">6</span>]
--- Total collections:  <span class="hljs-number">1</span>        Matched collections:  <span class="hljs-number">1</span>
--- Total channel: <span class="hljs-number">1</span>     Healthy collections: <span class="hljs-number">1</span>
================================================================================
<button class="copy-code-btn"></button></code></pre></li>
<li><p>Afficher une collection spécifique</p>
<p>Vous pouvez afficher une collection spécifique en spécifiant son identifiant.</p>
<pre><code translate="no" class="language-shell">Milvus(by-dev) &gt; show collection-history --<span class="hljs-built_in">id</span> <span class="hljs-number">443407225551410746</span>
================================================================================
DBID: <span class="hljs-number">1</span>
Collection ID: <span class="hljs-number">443407225551410746</span>       Collection Name: medium_articles_2020
Collection State: CollectionCreated     Create Time: <span class="hljs-number">2023</span>-08-08 09:<span class="hljs-number">27</span>:08
Fields:
- Field ID: <span class="hljs-number">0</span>   Field Name: RowID       Field <span class="hljs-type">Type</span>: Int64
- Field ID: <span class="hljs-number">1</span>   Field Name: Timestamp   Field <span class="hljs-type">Type</span>: Int64
- Field ID: <span class="hljs-number">100</span>         Field Name: <span class="hljs-built_in">id</span>          Field <span class="hljs-type">Type</span>: Int64
        - Primary Key: true, AutoID: false
- Field ID: <span class="hljs-number">101</span>         Field Name: title       Field <span class="hljs-type">Type</span>: VarChar
        - <span class="hljs-type">Type</span> Param max_length: <span class="hljs-number">512</span>
- Field ID: <span class="hljs-number">102</span>         Field Name: title_vector        Field <span class="hljs-type">Type</span>: FloatVector
        - <span class="hljs-type">Type</span> Param dim: <span class="hljs-number">768</span>
- Field ID: <span class="hljs-number">103</span>         Field Name: link        Field <span class="hljs-type">Type</span>: VarChar
        - <span class="hljs-type">Type</span> Param max_length: <span class="hljs-number">512</span>
- Field ID: <span class="hljs-number">104</span>         Field Name: reading_time        Field <span class="hljs-type">Type</span>: Int64
- Field ID: <span class="hljs-number">105</span>         Field Name: publication         Field <span class="hljs-type">Type</span>: VarChar
        - <span class="hljs-type">Type</span> Param max_length: <span class="hljs-number">512</span>
- Field ID: <span class="hljs-number">106</span>         Field Name: claps       Field <span class="hljs-type">Type</span>: Int64
- Field ID: <span class="hljs-number">107</span>         Field Name: responses   Field <span class="hljs-type">Type</span>: Int64
Enable Dynamic Schema: false
Consistency Level: Bounded
Start position <span class="hljs-keyword">for</span> channel by-dev-rootcoord-dml_0(by-dev-rootcoord-dml_0_443407225551410746v0): [<span class="hljs-number">1</span> <span class="hljs-number">0</span> <span class="hljs-number">28</span> <span class="hljs-number">175</span> <span class="hljs-number">133</span> <span class="hljs-number">76</span> <span class="hljs-number">39</span> <span class="hljs-number">6</span>]
<button class="copy-code-btn"></button></code></pre></li>
<li><p>Afficher toutes les collections chargées</p>
<p>Vous pouvez demander à Birdwatcher de filtrer toutes les collections chargées.</p>
<pre><code translate="no" class="language-shell">Milvus(<span class="hljs-keyword">by</span>-dev) &gt; show collection-loaded
Version: [&gt;= <span class="hljs-number">2.2</span><span class="hljs-number">.0</span>]     CollectionID: <span class="hljs-number">443407225551410746</span>
ReplicaNumber: <span class="hljs-number">1</span>        LoadStatus: Loaded
--- Collections Loaded: <span class="hljs-number">1</span>
<button class="copy-code-btn"></button></code></pre></li>
<li><p>Lister tous les points de contrôle d'une collection</p>
<p>Vous pouvez demander à Birdwatcher de lister tous les points de contrôle d'une collection spécifique.</p>
<pre><code translate="no" class="language-shell">Milvus(<span class="hljs-keyword">by</span>-dev) &gt; show checkpoint --collection <span class="hljs-number">443407225551410746</span>
vchannel <span class="hljs-keyword">by</span>-dev-rootcoord-dml_0_443407225551410746v0 seek to <span class="hljs-number">2023</span><span class="hljs-number">-08</span><span class="hljs-number">-08</span> <span class="hljs-number">09</span>:<span class="hljs-number">36</span>:<span class="hljs-number">09.54</span> +<span class="hljs-number">0000</span> UTC, cp channel: <span class="hljs-keyword">by</span>-dev-rootcoord-dml_0_443407225551410746v0, Source: Channel Checkpoint
<button class="copy-code-btn"></button></code></pre></li>
</ul>
<h3 id="Check-index-details" class="common-anchor-header">Vérifier les détails de l'index</h3><p>Exécutez la commande suivante pour lister tous les fichiers d'index en détail.</p>
<pre><code translate="no" class="language-shell">Milvus(by-dev) &gt; show index
*************<span class="hljs-number">2.1</span>.x***************
*************<span class="hljs-number">2.2</span>.x***************
==================================================================
Index ID: <span class="hljs-number">443407225551410801</span>    Index Name: _default_idx_102    CollectionID:<span class="hljs-number">443407225551410746</span>
Create Time: <span class="hljs-number">2023</span>-08-08 09:<span class="hljs-number">27</span>:<span class="hljs-number">19.139</span> +<span class="hljs-number">0000</span>      Deleted: false
Index <span class="hljs-type">Type</span>: HNSW        Metric <span class="hljs-type">Type</span>: L2
Index Params: 
==================================================================
<button class="copy-code-btn"></button></code></pre>
<h3 id="List-partitions" class="common-anchor-header">Lister les partitions</h3><p>Exécutez la commande suivante pour lister toutes les partitions d'une collection spécifique.</p>
<pre><code translate="no" class="language-shell">Milvus(by-dev) &gt; show partition --collection <span class="hljs-number">443407225551410746</span>
Parition ID: <span class="hljs-number">443407225551410747</span> Name: _default  State: PartitionCreated
--- Total <span class="hljs-title function_">Database</span><span class="hljs-params">(s)</span>: <span class="hljs-number">1</span>
<button class="copy-code-btn"></button></code></pre>
<h3 id="Check-channel-status" class="common-anchor-header">Vérifier l'état des canaux</h3><p>Exécutez la commande suivante pour afficher l'état des canaux</p>
<pre><code translate="no" class="language-shell">Milvus(<span class="hljs-keyword">by</span>-dev) &gt; show channel-watch
=============================
key: <span class="hljs-keyword">by</span>-dev/meta/channelwatch/<span class="hljs-number">6</span>/<span class="hljs-keyword">by</span>-dev-rootcoord-dml_0_443407225551410746v0
Channel Name:<span class="hljs-keyword">by</span>-dev-rootcoord-dml_0_443407225551410746v0         WatchState: WatchSuccess
Channel Watch start <span class="hljs-keyword">from</span>: <span class="hljs-number">2023</span><span class="hljs-number">-08</span><span class="hljs-number">-08</span> <span class="hljs-number">09</span>:<span class="hljs-number">27</span>:<span class="hljs-number">09</span> +<span class="hljs-number">0000</span>, timeout at: <span class="hljs-number">1970</span><span class="hljs-number">-01</span><span class="hljs-number">-01</span> <span class="hljs-number">00</span>:<span class="hljs-number">00</span>:<span class="hljs-number">00</span> +<span class="hljs-number">0000</span>
Start Position ID: [<span class="hljs-number">1</span> <span class="hljs-number">0</span> <span class="hljs-number">28</span> <span class="hljs-number">175</span> <span class="hljs-number">133</span> <span class="hljs-number">76</span> <span class="hljs-number">39</span> <span class="hljs-number">6</span>], time: <span class="hljs-number">1970</span><span class="hljs-number">-01</span><span class="hljs-number">-01</span> <span class="hljs-number">00</span>:<span class="hljs-number">00</span>:<span class="hljs-number">00</span> +<span class="hljs-number">0000</span>
Unflushed segments: []
Flushed segments: []
Dropped segments: []
--- Total Channels: <span class="hljs-number">1</span>
<button class="copy-code-btn"></button></code></pre>
<h3 id="List-all-replicas-and-segments" class="common-anchor-header">Répertorier toutes les répliques et tous les segments</h3><ul>
<li><p>Répertorier toutes les répliques</p>
<p>Exécutez la commande suivante pour répertorier toutes les répliques et les collections correspondantes.</p>
<pre><code translate="no" class="language-shell">Milvus(<span class="hljs-keyword">by</span>-dev) &gt; show replica
================================================================================
ReplicaID: <span class="hljs-number">443407225685278721</span> CollectionID: <span class="hljs-number">443407225551410746</span> version:&gt;=<span class="hljs-number">2.2</span><span class="hljs-number">.0</span>
All Nodes:[<span class="hljs-number">2</span>]
<button class="copy-code-btn"></button></code></pre></li>
<li><p>Liste de tous les segments</p>
<p>Exécutez la commande suivante pour afficher la liste de tous les segments et leur état</p>
<pre><code translate="no" class="language-shell">SegmentID: 443407225551610865 State: Flushed, Row Count:5979
--- Growing: 0, Sealed: 0, Flushed: 1
--- Total Segments: 1, row count: 5979
<button class="copy-code-btn"></button></code></pre>
<p>Exécuter la commande suivante pour lister en détail tous les segments chargés. Pour Milvus 2.1.x, utilisez plutôt <code translate="no">show segment-loaded</code>.</p>
<pre><code translate="no" class="language-shell">Milvus(<span class="hljs-keyword">by</span>-dev) &gt; show segment-loaded-grpc
===========
ServerID <span class="hljs-number">2</span>
Channel <span class="hljs-keyword">by</span>-dev-rootcoord-dml_0_443407225551410746v0, collection: <span class="hljs-number">443407225551410746</span>, version <span class="hljs-number">1691486840680656937</span>
Leader view <span class="hljs-keyword">for</span> channel: <span class="hljs-keyword">by</span>-dev-rootcoord-dml_0_443407225551410746v0
Growing segments number: <span class="hljs-number">0</span> , ids: []
SegmentID: <span class="hljs-number">443407225551610865</span> CollectionID: <span class="hljs-number">443407225551410746</span> Channel: <span class="hljs-keyword">by</span>-dev-rootcoord-dml_0_443407225551410746v0
Sealed segments number: <span class="hljs-number">1</span>    
<button class="copy-code-btn"></button></code></pre></li>
</ul>
<h3 id="List-configurations" class="common-anchor-header">Lister les configurations</h3><p>Vous pouvez demander à Birdwatcher de lister les configurations actuelles de chaque composant Milvus.</p>
<pre><code translate="no" class="language-shell">Milvus(by-dev) &gt; show configurations
client <span class="hljs-literal">nil</span> Session:proxy, ServerID: <span class="hljs-number">8</span>, Version: <span class="hljs-number">2.2</span><span class="hljs-number">.11</span>, Address: <span class="hljs-number">10.244</span><span class="hljs-number">.0</span><span class="hljs-number">.8</span>:<span class="hljs-number">19529</span>
Component rootcoord<span class="hljs-number">-1</span>
rootcoord.importtaskexpiration: <span class="hljs-number">900</span>
rootcoord.enableactivestandby: <span class="hljs-literal">false</span>
rootcoord.importtaskretention: <span class="hljs-number">86400</span>
rootcoord.maxpartitionnum: <span class="hljs-number">4096</span>
rootcoord.dmlchannelnum: <span class="hljs-number">16</span>
rootcoord.minsegmentsizetoenableindex: <span class="hljs-number">1024</span>
rootcoord.port: <span class="hljs-number">53100</span>
rootcoord.address: localhost
rootcoord.maxdatabasenum: <span class="hljs-number">64</span>
Component datacoord<span class="hljs-number">-3</span>
...
querynode.gracefulstoptimeout: <span class="hljs-number">30</span>
querynode.cache.enabled: <span class="hljs-literal">true</span>
querynode.cache.memorylimit: <span class="hljs-number">2147483648</span>
querynode.scheduler.maxreadconcurrentratio: <span class="hljs-number">2</span>
<button class="copy-code-btn"></button></code></pre>
<p>Vous pouvez également visiter chaque composant Milvus pour trouver sa configuration. L'exemple suivant montre comment lister la configuration du QueryCoord avec l'ID 7.</p>
<pre><code translate="no" class="language-shell">Milvus(<span class="hljs-keyword">by</span>-dev) &gt; show session
Session:datacoord, ServerID: <span class="hljs-number">3</span>, Version: <span class="hljs-number">2.2</span><span class="hljs-number">.11</span>, Address: <span class="hljs-number">10.244</span><span class="hljs-number">.0</span><span class="hljs-number">.8</span>:<span class="hljs-number">13333</span>
Session:datanode, ServerID: <span class="hljs-number">6</span>, Version: <span class="hljs-number">2.2</span><span class="hljs-number">.11</span>, Address: <span class="hljs-number">10.244</span><span class="hljs-number">.0</span><span class="hljs-number">.8</span>:<span class="hljs-number">21124</span>
Session:indexcoord, ServerID: <span class="hljs-number">4</span>, Version: <span class="hljs-number">2.2</span><span class="hljs-number">.11</span>, Address: <span class="hljs-number">10.244</span><span class="hljs-number">.0</span><span class="hljs-number">.8</span>:<span class="hljs-number">31000</span>
Session:indexnode, ServerID: <span class="hljs-number">5</span>, Version: <span class="hljs-number">2.2</span><span class="hljs-number">.11</span>, Address: <span class="hljs-number">10.244</span><span class="hljs-number">.0</span><span class="hljs-number">.8</span>:<span class="hljs-number">21121</span>
Session:proxy, ServerID: <span class="hljs-number">8</span>, Version: <span class="hljs-number">2.2</span><span class="hljs-number">.11</span>, Address: <span class="hljs-number">10.244</span><span class="hljs-number">.0</span><span class="hljs-number">.8</span>:<span class="hljs-number">19529</span>
Session:querycoord, ServerID: <span class="hljs-number">7</span>, Version: <span class="hljs-number">2.2</span><span class="hljs-number">.11</span>, Address: <span class="hljs-number">10.244</span><span class="hljs-number">.0</span><span class="hljs-number">.8</span>:<span class="hljs-number">19531</span>
Session:querynode, ServerID: <span class="hljs-number">2</span>, Version: <span class="hljs-number">2.2</span><span class="hljs-number">.11</span>, Address: <span class="hljs-number">10.244</span><span class="hljs-number">.0</span><span class="hljs-number">.8</span>:<span class="hljs-number">21123</span>
Session:rootcoord, ServerID: <span class="hljs-number">1</span>, Version: <span class="hljs-number">2.2</span><span class="hljs-number">.11</span>, Address: <span class="hljs-number">10.244</span><span class="hljs-number">.0</span><span class="hljs-number">.8</span>:<span class="hljs-number">53100</span>

Milvus(<span class="hljs-keyword">by</span>-dev) &gt; visit querycoord <span class="hljs-number">7</span>
QueryCoord<span class="hljs-number">-7</span>(<span class="hljs-number">10.244</span><span class="hljs-number">.0</span><span class="hljs-number">.8</span>:<span class="hljs-number">19531</span>) &gt; configuration
Key: querycoord.enableactivestandby, Value: <span class="hljs-literal">false</span>
Key: querycoord.channeltasktimeout, Value: <span class="hljs-number">60000</span>
Key: querycoord.overloadedmemorythresholdpercentage, Value: <span class="hljs-number">90</span>
Key: querycoord.distpullinterval, Value: <span class="hljs-number">500</span>
Key: querycoord.checkinterval, Value: <span class="hljs-number">10000</span>
Key: querycoord.checkhandoffinterval, Value: <span class="hljs-number">5000</span>
Key: querycoord.taskexecutioncap, Value: <span class="hljs-number">256</span>
Key: querycoord.taskmergecap, Value: <span class="hljs-number">8</span>
Key: querycoord.autohandoff, Value: <span class="hljs-literal">true</span>
Key: querycoord.address, Value: localhost
Key: querycoord.port, Value: <span class="hljs-number">19531</span>
Key: querycoord.memoryusagemaxdifferencepercentage, Value: <span class="hljs-number">30</span>
Key: querycoord.refreshtargetsintervalseconds, Value: <span class="hljs-number">300</span>
Key: querycoord.balanceintervalseconds, Value: <span class="hljs-number">60</span>
Key: querycoord.loadtimeoutseconds, Value: <span class="hljs-number">1800</span>
Key: querycoord.globalrowcountfactor, Value: <span class="hljs-number">0.1</span>
Key: querycoord.scoreunbalancetolerationfactor, Value: <span class="hljs-number">0.05</span>
Key: querycoord.reverseunbalancetolerationfactor, Value: <span class="hljs-number">1.3</span>
Key: querycoord.balancer, Value: ScoreBasedBalancer
Key: querycoord.autobalance, Value: <span class="hljs-literal">true</span>
Key: querycoord.segmenttasktimeout, Value: <span class="hljs-number">120000</span>
<button class="copy-code-btn"></button></code></pre>
<h2 id="Backup-metrics" class="common-anchor-header">Sauvegarde des métriques<button data-href="#Backup-metrics" class="anchor-icon" translate="no">
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
    </button></h2><p>Vous pouvez demander à Birdwatcher de sauvegarder les métriques de tous les composants</p>
<pre><code translate="no" class="language-shell">Milvus(my-release) &gt; backup
Backing up ... 100%(2452/2451)
backup etcd <span class="hljs-keyword">for</span> prefix  <span class="hljs-keyword">done</span>
http://10.244.0.10:9091/metrics
http://10.244.0.10:9091/metrics
http://10.244.0.10:9091/metrics
http://10.244.0.10:9091/metrics
http://10.244.0.10:9091/metrics
http://10.244.0.10:9091/metrics
http://10.244.0.10:9091/metrics
http://10.244.0.10:9091/metrics
backup <span class="hljs-keyword">for</span> prefix <span class="hljs-keyword">done</span>, stored <span class="hljs-keyword">in</span> file: bw_etcd_ALL.230810-075211.bak.gz
<button class="copy-code-btn"></button></code></pre>
<p>Vous pouvez ensuite vérifier le fichier dans le répertoire où vous démarrez Birdwatcher.</p>
<h2 id="Probe-collections" class="common-anchor-header">Sonder les collections<button data-href="#Probe-collections" class="anchor-icon" translate="no">
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
    </button></h2><p>Vous pouvez demander à Birdwatcher de sonder l'état des collections chargées avec des clés primaires spécifiées ou des requêtes fictives.</p>
<h3 id="Probe-collection-with-known-primary-key" class="common-anchor-header">Sonder une collection avec une clé primaire connue</h3><p>Dans la commande <code translate="no">probe</code>, vous devez spécifier la clé primaire en utilisant le drapeau <code translate="no">pk</code> et l'identifiant de la collection en utilisant le drapeau <code translate="no">collection</code>.</p>
<pre><code translate="no" class="language-shell">Milvus(<span class="hljs-keyword">by</span>-dev) &gt; probe pk --pk <span class="hljs-number">110</span> --collection <span class="hljs-number">442844725212299747</span>
PK <span class="hljs-number">110</span> found <span class="hljs-keyword">on</span> segment <span class="hljs-number">442844725212299830</span>
Field id, <span class="hljs-keyword">value</span>: &amp;{long_data:&lt;data:<span class="hljs-number">110</span> &gt; }
Field title, <span class="hljs-keyword">value</span>: &amp;{string_data:&lt;data:<span class="hljs-string">&quot;Human Resources Datafication&quot;</span> &gt; }
Field title_vector, <span class="hljs-keyword">value</span>: &amp;{dim:<span class="hljs-number">768</span> float_vector:&lt;data:<span class="hljs-number">0.022454707</span> data:<span class="hljs-number">0.007861045</span> data:<span class="hljs-number">0.0063843643</span> data:<span class="hljs-number">0.024065714</span> data:<span class="hljs-number">0.013782166</span> data:<span class="hljs-number">0.018483251</span> data:<span class="hljs-number">-0.026526336</span> ... data:<span class="hljs-number">-0.06579628</span> data:<span class="hljs-number">0.00033906146</span> data:<span class="hljs-number">0.030992996</span> data:<span class="hljs-number">-0.028134001</span> data:<span class="hljs-number">-0.01311325</span> data:<span class="hljs-number">0.012471594</span> &gt; }
Field article_meta, <span class="hljs-keyword">value</span>: &amp;{json_data:&lt;data:<span class="hljs-string">&quot;{\&quot;link\&quot;:\&quot;https:\\/\\/towardsdatascience.com\\/human-resources-datafication-d44c8f7cb365\&quot;,\&quot;reading_time\&quot;:6,\&quot;publication\&quot;:\&quot;Towards Data Science\&quot;,\&quot;claps\&quot;:256,\&quot;responses\&quot;:0}&quot;</span> &gt; }
<button class="copy-code-btn"></button></code></pre>
<h3 id="Probe-all-collections-with-mock-queries" class="common-anchor-header">Sonder toutes les collections avec des requêtes fictives</h3><p>Vous pouvez également demander à Birdwatcher de sonder toutes les collections avec des requêtes fictives.</p>
<pre><code translate="no" class="language-shell">Milvus(by-dev) &gt; probe query
probing collection <span class="hljs-number">442682158191982314</span>
Found vector field vector(<span class="hljs-number">103</span>) <span class="hljs-keyword">with</span> dim[<span class="hljs-number">384</span>], indexID: <span class="hljs-number">442682158191990455</span>
failed to generated mock request probing index <span class="hljs-built_in">type</span> IVF_FLAT <span class="hljs-keyword">not</span> supported yet
probing collection <span class="hljs-number">442844725212086932</span>
Found vector field title_vector(<span class="hljs-number">102</span>) <span class="hljs-keyword">with</span> dim[<span class="hljs-number">768</span>], indexID: <span class="hljs-number">442844725212086936</span>
Shard my-release-rootcoord-dml_1_442844725212086932v0 leader[<span class="hljs-number">298</span>] probe <span class="hljs-keyword">with</span> search success.
probing collection <span class="hljs-number">442844725212299747</span>
Found vector field title_vector(<span class="hljs-number">102</span>) <span class="hljs-keyword">with</span> dim[<span class="hljs-number">768</span>], indexID: <span class="hljs-number">442844725212299751</span>
Shard my-release-rootcoord-dml_4_442844725212299747v0 leader[<span class="hljs-number">298</span>] probe <span class="hljs-keyword">with</span> search success.
probing collection <span class="hljs-number">443294505839900248</span>
Found vector field vector(<span class="hljs-number">101</span>) <span class="hljs-keyword">with</span> dim[<span class="hljs-number">256</span>], indexID: <span class="hljs-number">443294505839900251</span>
Shard my-release-rootcoord-dml_5_443294505839900248v0 leader[<span class="hljs-number">298</span>] probe <span class="hljs-keyword">with</span> search success.
<button class="copy-code-btn"></button></code></pre>