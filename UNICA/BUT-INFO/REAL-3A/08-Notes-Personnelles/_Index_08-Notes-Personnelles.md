# Notes personnelles

> [!abstract] Dossier : Notes personnelles
> Notes libres, brouillons et réflexions personnelles.

## Notes

- Informations générales : [[Parcours REAL]]
- Contacts enseignants : [[Informations administratives]]
- Stages : [[Informations stages BUT 3]]
- SAE : [[Details des SAE]]
- Calendrier : [[Calendrier]]
- Dates des stages : ![[WhatsApp Image 2026-09-04 at 07.41.27.jpeg]]

---

> [!note] Contenu déplacé
> Les notes de cours ont été déplacées vers leur module respectif :
> - **Automatisation de la chaîne de production (R507)** : [[Cours 1 - Automatisation chaîne de production|Module R507 — Cours 1]]
> - **Modélisations mathématiques (R512)** : [[TD1 - Simulation|Module R512 — TD1 Simulation]]
> - **Qualité algorithmique (R504)** : [[Accueil R504-Qualite-Algorithmique|Module R504 — Qualité algorithmique]]
> - **Qualité de développement (R508)** : [[Accueil R508-Qualite-Developpement|Module R508 — Qualité de développement]]
> - **Optimisation (R511)** : [[TD1 - Genetic Algorithm from scratch|Module R511 — TD1 Genetic Algorithm]]
> - **Programmation avancée (R505)** : [[Cours 1 - Développement autour d'un broker MQTT|Module R505 — Cours 1 (broker MQTT)]] et [[TP1 - Programmation Avancee|TP1 — Broker MQTT]]
> - **Virtualisation (R509)** — Cours conteneurs : [[Cours 1 - Conteneurs et virtualisation]]
> - **Qualité de développement (R508)** — TD1 UNIX : [[TD1 - Répertoires et fichiers UNIX]]
> - **Qualité algorithmique (R504)** — TD1 terminaison/invariants : [[TD1 - Terminaison et invariants de boucle]]
> - **Optimisation (R511)** — TD 8 queens : [[TD2 - 8 Queens Problem]]
> - **Programmation avancée (R505)** — TP2 Kafka : [[TP2 - Collecte Traitement Donnees Kafka|Module R505 — TP2 Collecte Traitement Donnees Kafka]]
> - **Virtualisation (R509)** — TD2 : [[TD1 - Virtualisation avancee|Module R509 — TD2]]



TD2 pour le cours R504 

# NOTIONS DE COMPLEXITÉ

![[td_2_complexite.pdf]]



NOUVEAU COURS POUR R508:

![[Slides BUT3 - TD3-4 - Conte_regex_conte 1.pdf]]




Nouveau TD pour le cours R511 Optimisation:

![[BIC_TP2.pdf]]


## Exercice 1
1. Fait
2. Fait

## Exercice 2
1. L'entier passé à run() (par exemple 1000) définit tout simplement le nombre maximal d'évaluations autorisé avant que l'algorithme ne s'arrête.

2. - Les valeurs des deux variables de décision de la meilleure solution actuelle (`bestSolution.variables[0]` et `variables[1]`).
	La valeur de l'objectif correspondant pour la fonction d'Ackley (`bestSolution.objectives[0]`).





TD2 EX4 
![[TP2_Exercice4_STAT.pdf]]


NOUVEAU TD R507 SWARM 
TD3 -   Docker Swarm et passage à l'échelle
![[TP3.pdf]]



TD4 - R509 virtualisation avancee 



TD 2 Suite R504 Qualite algorithmique - COMPLEXITÉ ET RÉCURSIVITÉ

![[td_2_complexite_suite.pdf]]

1. Ci-dessous, vous pouvez voir une capture d'ecran de ce que j'ai fait
![[Pasted image 20261005045220.png|700]]


2. Capture d'ecran qui montre ce que j'ai fait sur VS code
![[Pasted image 20261005050720.png|606]]


3. Illustration de l'arbre forme recursive pour calculer F(5)
![[Pasted image 20261005050601.png|605]]


4. Tableau comparatifs des temps d'executions des fonctions de fibonacci dependant de n

| valeur de n        | fibonacciIteratif | fibonacciRecursif       |
| ------------------ | ----------------- | ----------------------- |
| 10                 | instantanee       | instantanee             |
| 20                 | instantanee       | instantanee             |
| 30                 | instantanee       | instantanee             |
| 40                 | instantanee       | extremement rapide      |
| 45                 | instantanee       | 3-4 secondes a peu pres |
| par curiosite (50) | instantanee       | 35 secondes             |

5. 
**Cas de base :** T(0) = 1 et T(1) = 1

**Pour n $\ge$ 2 :** T(n) = T(n-1) + T(n-2) + 1

Pour calculer $F_n$ , on compte **1** appel pour la fonction elle-même, plus les **$T(n-1)$** et **$T(n-2)$** appels des deux fonctions enfants qu'elle lance.

  

C'est tout ce qu'il faut retenir ! On passe à la **page 1 (partie IA / question 1)** ?

Partie IA:

1. 
Prompt : « Donne-moi un algorithme pour calculer la suite de Fibonacci. »

- (a) Les algorithmes proposés sont-ils identiques ?

    Non. En utilisant **Gemini 2.5 Flash**, l'IA propose une réponse spécifique, tandis que d'autres camarades obtiennent une version récursive avec mémoïsation, une version itérative, ou même du pseudo-code pour expliquer la logique.

- (b) Quels langages de programmation sont utilisés ?

    Principalement Python et Java, ainsi que du pseudo-code.

- (c) Les algorithmes proposés sont-ils récursifs ou itératifs ?

    On retrouve un mélange des deux : des versions itératives classique, récursives naïves ou récursives optimisées avec mémoïsation.

- (d) Les réponses indiquent-elles la complexité des algorithmes ?

    Généralement oui (souvent $\mathcal{O}(n)$ pour l'itératif / mémoïsation et $\mathcal{O}(2^n)$ pour le récursif naïf), mais la complexité spatiale en mémoire est parfois oubliée.

- (e) Les réponses contiennent-elles des erreurs ou des limites ?

    Oui : les versions récursives naïves ne préviennent pas des risques de dépassement de pile (StackOverflow) et les implémentations Java / Python omettent souvent le risque de dépassement de capacité d'un entier (int/long) pour de très grandes valeurs de $n$.


2. Fonctionnement :

3. L'IA utilise un tableau memo pour sauvegarder les résultats déjà calculés.
    
4. Avant de faire un calcul récursif, la méthode vérifie if (memo[n] != 0). Si la valeur est déjà connue, elle la renvoie immédiatement au lieu de refaire le calcul.
    
5. Si la valeur n'est pas connue, elle calcule $F_{n-1} + F_{n-2}$, stocke la réponse dans memo[n], puis la renvoie.




CREE UN NOUVEAU COURS R510 - Nouveaux paradigmes de bases de données

NOUVEAU TD POUR CE COURS:

# TD1 – Les limites du SQL

## Exercice 1 : Limites des modèles relationnels

### a) Problèmes rencontrés en période de forte affluence

- **Goulot d'étranglement sur les écritures (`RELEVE`) :** Avec une émission de données toutes les 30 secondes par vélo en circulation, la table `RELEVE` subit un volume d'insertions simultanées extrêmement élevé. Cela entraîne de la contention I/O sur le disque et des verrous au niveau du SGBD.
    
- **Dégradation du temps de réponse :** L'application doit afficher l'écran d'accueil en moins de 200 ms. La saturation du processeur et de la bande passante disque par les écritures massives de la table `RELEVE` ralentit l'exécution des requêtes `SELECT` d'affichage du profil.
    
- **Explosion du volume de la base :** La table `RELEVE` grandit très rapidement, ce qui alourdit les index et dégrade les performances globales de PostgreSQL.
    

### b) Requête SQL de l'écran d'accueil

SQL

```
SELECT 
    a.nom,
    a.prenom,
    v.nom_ville,
    ab.type AS type_abonnement,
    t.horodatage_debut AS date_dernier_trajet,
    t.distance_km
FROM ABONNE a
JOIN VILLE v ON a.code_ville = v.code_ville
LEFT JOIN ABONNEMENT ab ON a.id_abonne = ab.id_abonne
LEFT JOIN TRAJET t ON a.id_abonne = t.id_abonne
WHERE a.id_abonne = :id_abonne_courant
ORDER BY t.horodatage_debut DESC
LIMIT 1;
```

**Nombre de jointures :** La requête comporte **3 jointures** (`VILLE`, `ABONNEMENT`, `TRAJET`).

### c) Classification des tables selon leur profil d'accès

- **Lues très souvent et modifiées rarement :** `VILLE`, `ABONNEMENT`, `STATION`, `ABONNE`.
    
- **Écrites massivement et lues rarement :** `RELEVE`.
    
- **Lues et écrites à fréquence comparable :** `TRAJET`, `VELO`.
    

### d) Problèmes des tables `RELEVE` et `ABONNE` au regard des 5V

- **Table `RELEVE` (Vélocité et Volume) :**
    
    - **Vélocité :** Ingestion en continu d'un flux d'écritures à haute fréquence (un relevé toutes les 30 secondes par vélo).
        
    - **Volume :** Accumulation rapide de millions de lignes.
        
- **Table `ABONNE` (Variété et Flexibilité) :**
    
    - **Schéma rigide (_Schema-on-write_) :** Toute évolution du profil utilisateur (ex : ajout de préférences, connecteurs externes) impose une modification de structure (`ALTER TABLE`), complexe et bloquante sur un SGBDR en production.
        

### e) Préconisation et anticipation lors de la conception

- **Recommandation :** Adopter une architecture **Polyglot Persistence** (persistance polyglotte).
    
    - Conserver **PostgreSQL** pour le cœur de métier transactionnel (`ABONNE`, `ABONNEMENT`, `TRAJET`, `STATION`, `VILLE`).
        
    - Migrer `RELEVE` vers une base **NoSQL Orientée Séries Temporelles ou Colonnes** (ex : _TimescaleDB_, _InfluxDB_, _Cassandra_) pour gérer l'ingestion massive, et utiliser une base **Clé-Valeur** (ex : _Redis_) pour stocker la dernière position en temps réel d'un vélo.
        
- **Pourquoi y penser dès la conception ?** Un modèle relationnel pur atteint rapidement ses limites sur l'ingestion de flux de données (_streaming_). Corriger l'architecture a posteriori implique une refonte de code lourde, coûteuse et à risque d'interruption de service.
    

### f) Table problématique lors du passage au NoSQL

- **Table concernée :** `ABONNEMENT` (ainsi que `TRAJET`).
    
- **Raison :** Cette table nécessite des **garanties TRANSACTIONNELLES strictes (ACID)** et une **cohérence forte**. Elle est directement liée aux paiements et aux droits d'accès. La _cohérence éventuelle_ souvent utilisée en NoSQL est inacceptable ici (risque de double facturation ou d'accès non autorisé).
    

## Exercice 2 : Choisir le NoSQL

### a) Qualification des 3V par projet

|**Projet**|**Volume**|**Vélocité**|**Variété**|
|---|---|---|---|
|**Projet 1 : Capteurs de qualité de l'air**|**Fort**|**Moyenne à Forte**|**Faible**|
|**Projet 2 : Paie des agents municipaux**|**Faible**|**Faible**|**Faible**|
|**Projet 3 : Signalement citoyen**|**Moyen**|**Moyenne**|**Forte**|
|**Projet 4 : Archives de la médiathèque**|**Fort**|**Faible**|**Forte**|

### b) V dominant par projet

- **Projet 1 :** **Volume** (cumul massif de séries temporelles sur 5 ans).
    
- **Projet 3 :** **Variété** (données hétérogènes : texte libre, photos, géolocalisation, catégories évolutives).
    
- **Projet 4 :** **Variété** (métadonnées très différentes selon la nature du document).
    
- **Projet sans V dominant :** Le **Projet 2 (Paie des agents)**. Tous les V y sont faibles. Le facteur déterminant est la **Véracité / conformité ACID**, et non les caractéristiques du Big Data.
    

### c) Correction sur le volume du Projet 1

L'énoncé de la question mentionne 180 000 données par erreur (chiffre correspondant au Projet 4).

Le volume réel de données généré par le Projet 1 sur 5 ans se calcule ainsi :

$$\text{1 200 capteurs} \times 6 \text{ mesures/min} \times 60 \text{ min} \times 24 \text{ h} \times 365 \text{ jours} \times 5 \text{ ans} \approx \mathbf{189,2 \text{ millions de relevés}}$$

- **Problématique :** C'est l'accumulation temporelle massive de données qui pose problème. Un SGBDR classique saturera rapidement en espace et en temps de requête sans mécanisme de partitionnement avancé.
    

### d) Recommandations techniques

- **Projet 1 (Capteurs air) :** **NoSQL (Séries Temporelles / Orienté Colonnes)**.
    
    - _Justification :_ Adapté pour l'écriture en masse et le stockage de séries temporelles (_TimescaleDB_, _InfluxDB_, _Cassandra_) sans besoin de traitement temps réel complexe.
        
- **Projet 2 (Paie agents) :** **Relationnel (SQL)**.
    
    - _Justification :_ Volume faible, besoins stricts d'intégrité, de transactions ACID, et d'auditabilité sur 50 ans.
        
- **Projet 3 (Signalement citoyen) :** **NoSQL Orienté Document + Stockage Objet**.
    
    - _Justification :_ Un SGBD Document (_MongoDB_) permet de gérer la flexibilité des catégories et la géolocalisation. Les photos sont stockées sur un stockage objet (ex : _S3_, _MinIO_).
        
- **Projet 4 (Archives médiathèque) :** **NoSQL Orienté Document + Moteur de recherche**.
    
    - _Justification :_ Base document (_MongoDB_) pour la structure variable des métadonnées, couplée à un moteur de recherche (_Elasticsearch_) pour la recherche plein texte.


# TD2 - R510 NoSQL

![[TD2 R510.pdf]]

Ex.1
a. privilegier la disponibilitee au detriment de la coherence en cas de probleme reseau : ils ont reserve le meme siege

b. C sacrifie

c. Si on avait sacrifie A, on n'aurait pas pu reserver (erreur) ou seulement sur l'un des deux

d. AP : Catalogue
   CP:  Reservations

e. AP: ici
   CA: base relationnelle

f. Non c'est une panne, pas de coupure reseau.
Non.
D'un point de vue utilisateur: Non

Ex.2

|     | Propriete  | ?                     |
| --- | ---------- | --------------------- |
| 1   | Atomicite  |                       |
| 2   | Coherence  |                       |
| 3   | Isolation  |                       |
| 4   | Durabilite |                       |
| 5   | Aucune     | interface utilisateur |
| 6   |            |                       |
| 7   |            |                       |


f.

|                              | ACID/BASE |                        |
| ---------------------------- | --------- | ---------------------- |
| Paiement des billets         | ACID      |                        |
| Catalogue des concerts       | BASE      |                        |
| Panier du visiteur           | ACID      | Reservation temporaire |
| Stock des sieges disponibles | ACID      |                        |
| Avis des spectateurs         | BASE      |                        |
| Historique de navigation     | BASE      |                        |


Ex.3

| a                      | Famille de Sharding | ?                                                    |
| ---------------------- | ------------------- | ---------------------------------------------------- |
| Journaux de navigation | annuaire            | Volume ++, acces simples, lecture parallele          |
| Paniers des visiteurs  | hachage             | on accede a un element pas de requete par intervalle |
| Billets vendus         | intervalle          | requetes par intervalle                              |
| Catalogue des concerts | aucune/hachage      | pau de donnees                                       |

b.

--- 

NOUVELLE MATIERE ET NOUVEAU TP3 - R510 NOUVEAU PARADIGMES 

![[TD3 R510.pdf]]

--- 

## Exercice 1
a.![[Pasted image 20261022084541.png]]

b. ![[Pasted image 20261022084639.png]]

c. ![[Pasted image 20261022084755.png]]

d. ![[Pasted image 20261022085052.png]]

## Exercice 2

a.![[Pasted image 20261022085436.png]]

b.![[Pasted image 20261022085752.png]]

c. Pour une sessions sa permet de filtrer/retirer les sessions inutilisées depuis un certain temps.
Pour le cache sa retire les donnees obsoletes.

d. PERSIST ma_session

## Exercice 3

![[Pasted image 20261022090925.png]]

![[Pasted image 20261022090935.png]]


## Exercice 4

![[Pasted image 20261022092849.png]]

