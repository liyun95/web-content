---
id: release_notes.md
summary: Notes de mise à jour de Milvus
title: Notes de mise à jour
---
<h1 id="Release-Notes" class="common-anchor-header">Notes de mise à jour<button data-href="#Release-Notes" class="anchor-icon" translate="no">
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
    </button></h1><p>Découvrez les nouveautés de Milvus ! Cette page résume les nouvelles fonctionnalités, les améliorations, les problèmes connus et les corrections de bogues de chaque version. Vous trouverez dans cette section les notes de version pour chaque version publiée après la v2.5.0. Nous vous conseillons de consulter régulièrement cette page pour prendre connaissance des mises à jour.</p>
<h2 id="v250-beta" class="common-anchor-header">v2.5.0-beta<button data-href="#v250-beta" class="anchor-icon" translate="no">
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
    </button></h2><p>Date de publication : 26 novembre 2024</p>
<table>
<thead>
<tr><th>Version de Milvus</th><th>Version du SDK Python</th><th>Version du SDK Node.js</th><th>Version du SDK Java</th></tr>
</thead>
<tbody>
<tr><td>2.5.0-beta</td><td>2.5.0</td><td>2.5.0</td><td>2.5.0</td></tr>
</tbody>
</table>
<p>Milvus 2.5.0-beta apporte des avancées significatives pour améliorer la convivialité, l'évolutivité et les performances pour les utilisateurs traitant de la recherche vectorielle et de la gestion de données à grande échelle. Avec cette version, Milvus intègre de nouvelles fonctionnalités puissantes telles que la recherche basée sur les termes, le compactage des clusters pour des requêtes optimisées et la prise en charge polyvalente des méthodes de recherche vectorielle dense et éparse. Les améliorations apportées à la gestion des clusters, à l'indexation et au traitement des données introduisent de nouveaux niveaux de flexibilité et de facilité d'utilisation, faisant de Milvus une base de données vectorielles encore plus robuste et conviviale.</p>
<h3 id="Key-Features" class="common-anchor-header">Caractéristiques principales</h3><h4 id="Full-Text-Search" class="common-anchor-header">Recherche en texte intégral</h4><p>Milvus 2.5 prend en charge la recherche plein texte mise en œuvre avec Sparse-BM25 ! Cette fonctionnalité est un complément important aux solides capacités de recherche sémantique de Milvus, en particulier dans les scénarios impliquant des mots rares ou des termes techniques. Dans les versions précédentes, Milvus prenait en charge les vecteurs épars pour faciliter les scénarios de recherche par mot-clé. Ces vecteurs épars étaient générés en dehors de Milvus par des modèles neuronaux tels que SPLADEv2/BGE-M3 ou des modèles statistiques tels que l'algorithme BM25.</p>
<p>Milvus 2.5 intègre la tokenisation et l'extraction de vecteurs épars, étendant l'API de la réception de vecteurs en entrée à l'acceptation directe de texte. Les informations statistiques BM25 sont mises à jour en temps réel au fur et à mesure que les données sont insérées, ce qui améliore la convivialité et la précision. En outre, les vecteurs épars basés sur les algorithmes de voisinage le plus proche (ANN) offrent des performances plus puissantes que les systèmes de recherche par mot-clé standard.</p>
<p>Pour plus d'informations, reportez-vous à la section <a href="/docs/fr/full-text-search.md">Recherche en texte intégral</a>.</p>
<h4 id="Cluster-Management-WebUI-Beta" class="common-anchor-header">Interface Web de gestion des clusters (Beta)</h4><p>Pour mieux prendre en charge les données massives et les fonctionnalités riches, la conception sophistiquée de Milvus inclut diverses dépendances, de nombreux rôles de nœuds, des structures de données complexes, etc. Ces aspects peuvent poser des problèmes d'utilisation et de maintenance.</p>
<p>Milvus 2.5 introduit une interface Web intégrée de gestion des clusters, qui réduit les difficultés de maintenance du système en visualisant les informations complexes de l'environnement d'exécution de Milvus. Il s'agit notamment des détails des bases de données et des collections, des segments, des canaux, des dépendances, de l'état de santé des nœuds, des informations sur les tâches, des requêtes lentes, etc.</p>
<h4 id="Text-Match" class="common-anchor-header">Correspondance de texte</h4><p>Milvus 2.5 exploite les analyseurs et l'indexation de Tantivy pour le prétraitement du texte et la construction de l'index, prenant en charge la correspondance précise en langage naturel des données textuelles basées sur des termes spécifiques. Cette fonctionnalité est principalement utilisée pour la recherche filtrée afin de satisfaire des conditions spécifiques et peut incorporer le filtrage scalaire pour affiner les résultats des requêtes, permettant des recherches de similarité dans les vecteurs qui répondent aux critères scalaires.</p>
<p>Pour plus d'informations, reportez-vous à la section <a href="/docs/fr/keyword-match.md">Correspondance par mot-clé</a>.</p>
<h4 id="Bitmap-Index" class="common-anchor-header">Index Bitmap</h4><p>Un nouvel index de données scalaires a été ajouté à la famille Milvus. L'index BitMap utilise un tableau de bits, d'une longueur égale au nombre de lignes, pour représenter l'existence de valeurs et accélérer les recherches.</p>
<p>Les index Bitmap sont traditionnellement efficaces pour les champs à faible cardinalité, qui présentent un nombre modeste de valeurs distinctes - par exemple, une colonne contenant des informations sur le sexe avec seulement deux valeurs possibles : homme et femme.</p>
<p>Pour plus de détails, voir <a href="/docs/fr/bitmap.md">Index bitmap</a>.</p>
<h4 id="Nullable--Default-Value" class="common-anchor-header">Valeur nulle et valeur par défaut</h4><p>Milvus prend désormais en charge la définition de propriétés nullables et de valeurs par défaut pour les champs scalaires autres que le champ de clé primaire. Pour les champs scalaires marqués comme <code translate="no">nullable=True</code>, les utilisateurs peuvent omettre le champ lors de l'insertion de données ; le système le traitera comme une valeur nulle ou une valeur par défaut (si elle est définie) sans générer d'erreur.</p>
<p>Les valeurs par défaut et les propriétés nullables offrent une plus grande flexibilité à Milvus. Les utilisateurs peuvent utiliser cette fonctionnalité pour les champs dont les valeurs sont incertaines lors de la création de collections. Elles simplifient également la migration des données d'autres systèmes de base de données vers Milvus, en permettant de traiter des ensembles de données contenant des valeurs nulles tout en préservant les paramètres de valeur par défaut d'origine.</p>
<p>Pour plus de détails, voir <a href="/docs/fr/nullable-and-default.md">Valeur nulle et valeur par défaut</a>.</p>
<h4 id="Faiss-based-HNSW-SQPQPRQ" class="common-anchor-header">SQ/PQ/PRQ de HNSW basé sur Faiss</h4><p>Grâce à une collaboration étroite avec la communauté Faiss, l'algorithme HNSW dans Faiss a connu des améliorations significatives à la fois en termes de fonctionnalité et de performance. Pour des raisons de stabilité et de maintenabilité, Milvus 2.5 a officiellement migré sa prise en charge de HNSW de hnswlib vers Faiss.</p>
<p>Basé sur Faiss, Milvus 2.5 prend en charge plusieurs méthodes de quantification sur HNSW pour répondre aux besoins de différents scénarios : SQ (Scalar Quantizers), PQ (Product Quantizer) et PRQ (Product Residual Quantizer). SQ et PQ sont les plus courants ; SQ offre de bonnes performances en matière d'interrogation et de vitesse de construction, tandis que PQ offre un meilleur rappel pour un même taux de compression. De nombreuses bases de données vectorielles utilisent couramment la quantification binaire, qui est une forme simple de quantification SQ.</p>
<p>PRQ est une fusion de PQ et d'AQ (Additive Quantizer). Par rapport au PQ, il nécessite des temps de construction plus longs pour offrir un meilleur rappel, en particulier à des taux de compression élevés, selon la compression binaire.</p>
<h4 id="Clustering-Compaction-Beta" class="common-anchor-header">Compaction par regroupement (Beta)</h4><p>Milvus 2.5 introduit le compactage par regroupement pour accélérer les recherches et réduire les coûts dans les grandes collections. En spécifiant un champ scalaire comme clé de compactage, les données sont redistribuées par plage afin d'optimiser le stockage et la récupération. Agissant comme un index global, cette fonctionnalité permet à Milvus d'élaguer efficacement les données lors des requêtes basées sur les métadonnées de clustering, améliorant ainsi les performances de recherche lorsque des filtres scalaires sont appliqués.</p>
<p>Pour plus d'informations, reportez-vous à la section <a href="/docs/fr/clustering-compaction.md">Compaction de clustering</a>.</p>
<h3 id="Other-Features" class="common-anchor-header">Autres fonctionnalités</h3><h4 id="Streaming-Node-Beta" class="common-anchor-header">Nœud de streaming (Beta)</h4><p>Milvus 2.5 introduit un nouveau composant appelé nœud de streaming, qui fournit des services de journalisation en avance sur l'écriture (WAL). Cela permet à Milvus d'atteindre un consensus avant et après les canaux de lecture et d'écriture, ce qui débloque de nouvelles caractéristiques, fonctionnalités et optimisations. Cette fonctionnalité est désactivée par défaut dans Milvus 2.5 et sera officiellement disponible dans la version 3.0.</p>
<h4 id="IPv6-Support" class="common-anchor-header">Prise en charge d'IPv6</h4><p>Milvus prend désormais en charge IPv6, ce qui permet d'étendre la connectivité et la compatibilité du réseau.</p>
<h4 id="CSV-Bulk-Import" class="common-anchor-header">Importation en masse CSV</h4><p>Outre les formats JSON et Parquet, Milvus prend désormais en charge l'importation directe en masse de données au format CSV.</p>
<h4 id="Expression-Templates-for-Query-Acceleration" class="common-anchor-header">Modèles d'expression pour l'accélération des requêtes</h4><p>Milvus prend désormais en charge les modèles d'expression, ce qui améliore l'efficacité de l'analyse des expressions, en particulier dans les scénarios comportant des expressions complexes.</p>
<h4 id="GroupBy-Enhancements" class="common-anchor-header">Améliorations de GroupBy</h4><ul>
<li><strong>Taille de groupe personnalisable</strong>: Ajout de la prise en charge de la spécification du nombre d'entrées renvoyées pour chaque groupe.</li>
<li><strong>Recherche hybride par groupe</strong>: Prise en charge de la recherche hybride GroupBy basée sur plusieurs colonnes de vecteurs.</li>
</ul>
<h4 id="Iterator-Enhancements" class="common-anchor-header">Améliorations de l'itérateur</h4><ul>
<li><strong>Support MVCC</strong>: Les utilisateurs peuvent désormais utiliser des itérateurs sans être affectés par les modifications ultérieures des données telles que les insertions et les suppressions, grâce au contrôle de concordance multi-version (MVCC).</li>
<li><strong>Curseur persistant</strong>: Milvus prend désormais en charge un curseur persistant pour QueryIterator, ce qui permet aux utilisateurs de reprendre l'itération à partir de la dernière position après un redémarrage de Milvus sans avoir à redémarrer l'ensemble du processus d'itération.</li>
</ul>
<h3 id="Improvements" class="common-anchor-header">Améliorations</h3><h4 id="Deletion-Optimization" class="common-anchor-header">Optimisation de la suppression</h4><p>Amélioration de la vitesse et réduction de l'utilisation de la mémoire pour les suppressions à grande échelle en optimisant l'utilisation des verrous et la gestion de la mémoire.</p>
<h4 id="Dependencies-Upgrade" class="common-anchor-header">Mise à jour des dépendances</h4><p>Mise à jour vers ETCD 3.5.16 et Pulsar 3.0.7 LTS, corrigeant les CVE existantes et améliorant la sécurité. Note : La mise à jour vers Pulsar 3.x n'est pas compatible avec les versions précédentes 2.x.</p>
<p>Pour les utilisateurs qui disposent déjà d'un déploiement Milvus fonctionnel, vous devez mettre à niveau les composants ETCD et Pulsar avant de pouvoir utiliser les nouvelles caractéristiques et fonctions. Pour plus de détails, voir <a href="/docs/fr/upgrade-pulsar-v3.md">Mise à niveau de Pulsar de 2.x à 3.x.</a></p>
<h4 id="Local-Storage-V2" class="common-anchor-header">Stockage local V2</h4><p>Introduction d'un nouveau format de fichier local dans Milvus 2.5, améliorant l'efficacité du chargement et des requêtes pour les données scalaires, réduisant la surcharge de mémoire et jetant les bases des optimisations futures.</p>
<h4 id="Expression-Parsing-Optimization" class="common-anchor-header">Optimisation de l'analyse des expressions</h4><p>Amélioration de l'analyse des expressions par la mise en place d'un cache pour les expressions répétées, la mise à niveau d'ANTLR et l'optimisation des performances des clauses <code translate="no">NOT IN</code>.</p>
<h4 id="Improved-DDL-Concurrency-Performance" class="common-anchor-header">Amélioration des performances en matière de simultanéité des DDL</h4><p>Optimisation des performances de simultanéité des opérations DDL (Data Definition Language).</p>
<h4 id="RESTful-API-Feature-Alignment" class="common-anchor-header">Alignement des fonctionnalités de l'API RESTful</h4><p>Alignement des fonctionnalités de l'API RESTful avec d'autres SDK pour plus de cohérence.</p>