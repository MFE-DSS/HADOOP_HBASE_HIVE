# HADOOP_HBASE_HIVE
aperçu détaillé de la manière dont Hive interagit avec Hadoop, HBase, et Spark, et une compréhension des relations et dépendances entre ces technologies.

### HDFS (Hadoop Distributed File System)
**Distributed Storage:**
- **Intérêt Technologique** : Permet de stocker de très grandes quantités de données de manière répartie sur plusieurs machines, ce qui est crucial pour le traitement de données massives.
- **Spécificité** : Divise les fichiers en blocs qui sont distribués à travers un cluster, garantissant un haut degré de disponibilité et de fiabilité.
- **Enjeux** : Gestion efficace de la distribution des données et des besoins en matériel.

**Fault Tolerance:**
- **Intérêt Technologique** : Assure la continuité du service même en cas de panne matérielle en répliquant les données sur plusieurs nœuds.
- **Spécificité** : Utilise un modèle de réplication pour tolérer les défaillances matérielles.
- **Enjeux** : Maximisation de la résilience sans compromettre l'efficacité, balancement des charges entre réplication et coût du stockage.

### MapReduce
**Batch Processing:**
- **Intérêt Technologique** : Permet le traitement de grandes quantités de données de manière efficace et automatisée.
- **Spécificité** : Divise les tâches en étapes de mappage et de réduction, transformant les données en parallèle.
- **Enjeux** : Optimisation des ressources utilisées lors des phases de traitement batch, gestion des tâches longues.

**Shuffle:**
- **Intérêt Technologique** : Facilite l’échange de données entre les tâches de mappage et de réduction.
- **Spécificité** : Affecte de manière significative la performance, nécessitant une gestion soignée des entrées-sorties.
- **Enjeux** : Réduction des coûts I/O grâce à une optimisation des processus de shuffle.

### HBase
**NoSQL:**
- **Intérêt Technologique** : Adapté aux scénarios où besoin d'un traitement rapide sur des structures de données non relationnelles.
- **Spécificité** : Architecture orientation colonnes, flexible et évolutive.
- **Enjeux** : Support de la montée en charge et de la faiblesse latence lors des accès.

**Columnar Store:**
- **Intérêt Technologique** : Idéal pour les requêtes analytiques longitudinales sur de vastes datasets.
- **Spécificité** : Stocke les données par colonnes pour une compression et une lecture rapide.
- **Enjeux** : Maximisation des performances de lecture et d'écriture, maintien de la cohérence en temps réel.

### Hive
**Data Warehousing:**
- **Intérêt Technologique** : Simplifie l'analyse de grandes volumétries de données par le biais du SQL.
- **Spécificité** : Interface SQL (HiveQL) pour effectuer des requêtes sur des données stockées dans HDFS.
- **Enjeux** : Équilibrer le besoin de rapidité d'exécution et la complexité des requêtes, intégration avec d'autres outils analytiques.

**HiveQL:**
- **Intérêt Technologique** : Rapprochement des analystes traditionnels des environnements Big Data.
- **Spécificité** : Offre une syntaxe SQL pour manipuler les données, facilitant l'accessibilité de ces technologies non-SQL.
- **Enjeux** : Améliorer la performance des requêtes et l’intégration avec les moteurs de calcul moderne comme Spark.

### SparkSQL/Tez (dans le contexte Hive)
**In-Memory:**
- **Intérêt Technologique** : Amélioration significative des temps d'exécution par rapport aux disques dus à la persistance des données en mémoire.
- **Spécificité** : Maintient les données en mémoire, réduisant grandement le temps de latence lors des traitements complexes.
- **Enjeux** : Gestion efficace de la mémoire, besoin d’un matériel potentiellement coûteux.

**DAG Execution:**
- **Intérêt Technologique** : Permet une exécution optimisée des tâches grâce à l’ordonnancement intelligent des dépendances des tâches.
- **Spécificité** : Utilise un modèle de graphe acyclique dirigé pour gérer le workflow des données de manière dynamique.
- **Enjeux** : Gestion des dépendances complexes entre les tâches, augmentation du parallélisme pour maximiser les ressources.

### Hyperparamètres et Intérêts à la Marges des Autres Technologies Big Data
Chaque de ces technologies offre des hyperparamètres qui permettent de maximiser l’efficacité selon les besoins précis :

**HDFS:**
- Paramètres comme `dfs.replication`, la taille des blocs pour l’équilibrage entre performance et coût de stockage.

**MapReduce:**
- Des tailles de mémoire pour les tâches Map et Reduce (`mapreduce.map.memory.mb`), configuration du nombre de réductions (`mapreduce.reduce.tasks`) pour un équilibrage optimal.

**HBase:**
- `hbase.regionserver.handler.count` pour régler le nombre de threads affectés pour le traitement des requêtes et le `memstore` pour la gestion de la mémoire vive.

**Hive:**
- `hive.execution.engine` pour choisir entre MapReduce, Tez, ou Spark, `hive.exec.parallel` pour activer l'exécution parallèle.

**SparkSQL:**
- `spark.sql.shuffle.partitions` pour optimiser le regroupement en fonction de la taille des données, gestion des cache par `spark.sql.inMemoryColumnarStorage.compressed`.

