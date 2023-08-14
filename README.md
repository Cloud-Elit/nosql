<a name="_toc86414358"></a><a name="_toc90890749"></a><a name="_toc90894788"></a><a name="_toc90895222"></a><a name="_toc117089977"></a>Bases de données NoSQL
1. ####### <a name="_toc86414359"></a><a name="_toc90895223"></a>**Définition**
Une base de données NoSQL est un système de gestion de données non relationnel qui, contrairement aux SGBDRs, ne nécessite pas de schéma fixe. Il n’y a donc pas de notion de "jointures" ce qui permet le stockage distribué des données et facilite ainsi la mise à l’échelle. Le terme NoSQL (pour Not only SQL) a été initialement utilisé par Carl Strozzi en 1998. Strozzi suggère que « *comme le mouvement NoSQL actuel s’écarte complètement du modèle relationnel ; il aurait dû être appelé de manière plus appropriée "NoREL"* » [Strozzi, 98].

Un SGBDR traditionnel utilise la syntaxe SQL pour écrire, lire, modifier et supprimer des données. En revanche, un système de base de données NoSQL englobe un large éventail de technologies de base de données qui peuvent stocker des données structurées, semi-structurées, non-structurées et polymorphes. En outre, lorsque le volume de données devient énorme, le temps de réponse d’une base de données relationnelle devient lent, contrairement à une base NoSQL. C’est pour ces deux principales raisons (hétérogénéité et volumétrie) que le concept des bases de données NoSQL est devenu populaire auprès des géants de l’Internet. Une base de données NoSQL répond à quatre caractéristiques :

- **Non-Relationnelle** : il ne doit pas y avoir de jointures entre les tables et il n’y a pas d’obligation que les enregistrements d’une même table aient tous les mêmes attributs.
- **Sans-Schéma** : il ne doit pas y avoir de schémas fixes ou, s’ils existent, ils doivent être assouplis (données semi-structurées).
- **API Simple** : une base de données NoSQL doit offrir des interfaces faciles à utiliser pour le stockage et l’interrogation de données (les plus courants sont les API REST).
- **Distribuée** : le stockage et l’analyse de données dans une base de données NoSQL doivent être distribués sur plusieurs nœuds d’un Cluster. Cela permettra la mise à l’échelle et le basculement automatique (tolérance aux pannes). 
1. ####### <a name="_toc86414360"></a><a name="_toc90895224"></a>**Types de bases de données NoSQL**
Les bases de données NoSQL sont principalement classées en quatre types selon si elles sont basées sur (i) des paires clé-valeur, (*ii*) des colonnes, (*iii*) des documents ou (*iv*) des graphes. Chaque catégorie a ses caractéristiques et ses limites uniques et aucune n’est meilleure pour résoudre tous les problèmes. Le choix d’une base plutôt qu’une autre est fait en fonction des exigences de chaque projet. Dans la suite de cette section nous présentons brièvement chaque type de bases de données NoSQL ainsi que le théorème CAP, une des principales notions à tenir en considération lors du choix d’une base de données NoSQL.
1. ## <a name="_toc90895225"></a>Les bases de données NoSQL basées sur une paire "clé-valeur"
Ces bases de données sont conçues pour gérer (lire et écrire) de très gros volumes de données à grande vitesse. Les valeurs sont stockées dans des tables de hachage et sont accessibles via une clé unique. Elles peuvent être de n’importe quel type d’objet binaire (texte, vidéo, document JSON, etc.). Pour assurer l’évolutivité et la disponibilité, les données sont partitionnées et répliquées sur un cluster. Toutefois, ce type de bases de données ne prend souvent pas en charge les transactions. Parmi ces bases de données on trouve Redis[^1] et Riak[^2].
1. ## <a name="_toc90895226"></a>Les bases de données NoSQL orientées "colonnes"
Les bases de données orientées colonnes stockent les données dans des tables avec des lignes et des colonnes, tout comme les SGBDRs, mais la différence c’est que les noms et les formats des colonnes peuvent changer d’une ligne à une autre dans une même table. Généralement, ces bases de données regroupent les colonnes associées dans des colonnes "larges" ce qui permet à une requête d’extraire des données associées en une seule opération. Cela permet également d’offrir des performances élevées sur les requêtes d’agrégation, comme COUNT, MIN, MAX, AVG, SUM etc., car les données sont disponibles dans une même large colonne (par exemple, la famille de colonnes présentée précédemment dans HBase). Parmi ces bases de données on trouve HBase et Cassandra[^3].
1. ## <a name="_toc90895227"></a>Les bases de données NoSQL orientées "documents"
Les bases de données orientées documents stockent les données sous forme de documents JSON, BSON (Binary JSON) ou XML. Chaque valeur, qui est un document, est accessible via une clé unique mais peut être également récupéré à travers des requêtes qui cherchent dans le document lui-même. Ainsi, pour permettre une récupération rapide sans connaître la clé, les champs les plus populaires du document doivent être indexés. Les documents peuvent avoir la même structure ou des structures différentes ; au sein d’un même document, les blocs de données peuvent avoir des structures similaires ou différentes. Parmi ces bases de données on trouve MongoDB[^4] et CouchDB[^5].
1. ## <a name="_toc90895228"></a>Les bases de données NoSQL orientées "graphes"
Les bases de données orientées graphes utilisent des structures de graphe pour stocker, mapper et interroger des relations entre les données. Les graphes représentent les données sous forme de nœuds, d’arêtes et de propriétés. Les nœuds correspondent aux instances ou aux entités de données qui représentent tout objet à gérer (une personne, un compte, une localisation, un message, etc.). Les arêtes représentent les relations entre les nœuds ; chaque relation a un sens qui peut être unidirectionnel ou bidirectionnel. Chaque nœud et chaque arête ont chacun un identifiant unique. Enfin, les propriétés représentent des informations descriptives associées aux nœuds et, dans certains cas, les arrêtes. Parmi ces bases de données on trouve Neo4J[^6] et OrientDB[^7].
1. ####### <a name="_toc86414361"></a><a name="_toc90895229"></a>**Théorème CAP**
Le théorème CAP, connu également sous le nom du théorème de brasseur, a été introduit par Fox et Brewer [Fox, 99]. Ce théorème indique qu’il est impossible pour un magasin de données distribué d’offrir plus de deux garanties parmi trois : la cohérence C (pour Consistency), la disponibilité A (pour Availability) et la tolérance au partitionnement P (pour Partition Tolerance). La cohérence des données stockées sur un magasin de données distribué exige que tous les utilisateurs voient les mêmes valeurs et en même temps, quel que soit le nœud auquel ils se connectent et quel que soit le nœud ayant réalisé la dernière écriture. La disponibilité exige que tout utilisateur autorisé qui fait une requête obtienne une réponse dans les délais convenus quel soit l’état du système (nœuds non accessibles, maintenance, …). Enfin, la tolérance au partitionnement signifie que le système doit continuer à fonctionner même s’il y a des pannes sur des nœuds de la plateforme distribuée.

Comme illustré dans la Figure 1, chaque base de données NoSQL répond à deux propriétés du théorème CAP :

- Cohérence et tolérance au partitionnement : on y trouve HBase, MongoDB et Redis.
- Cohérence et disponibilité : on y trouve OrientDB et Neo4J.
- Disponibilité et tolérance au partitionnement : on y trouve Cassandra, Riak et CouchDB.

3

*Figure 1. Classification des bases de données NoSQL selon le théorème CAP*


[^1]: https://redis.io/
[^2]: https://riak.com/
[^3]: https://cassandra.apache.org/
[^4]: https://www.mongodb.com/
[^5]: http://couchdb.apache.org/
[^6]: https://neo4j.com/
[^7]: https://orientdb.com/