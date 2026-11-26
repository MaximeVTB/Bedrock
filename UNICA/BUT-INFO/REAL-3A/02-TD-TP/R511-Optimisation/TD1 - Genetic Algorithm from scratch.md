---
type: td
module: R511-Optimisation
type_seance: TD
semaine:
date: 2026-09-08
status: à-faire
tags:
  - but-info
  - real
  - td
  - optimisation
  - genetic-algorithm
---

# TD1 - Genetic Algorithm from scratch

> [!info] Séance
> - **Module** : Méthodes d'optimisation pour l'aide à la décision (R511)
> - **Type** : TD
> - **Date** : 2026-09-08
> - **Groupe** : 

---

## Sujet / Enoncé

> Énoncé du TP (Genetic Algorithm from scratch in Python) :
> ![[BIC_TP1.pdf]]

## Travail à réaliser

- [x] Répondre aux questions du TP (Q1 à Q15)

## Réponses / Solutions

Exercice 2

1. Avec la même seed, on obtient toujours la même population au début et le même résultat à la fin. Avec une seed aléatoire, le résultat change à chaque exécution.

2. Avec MAX_NFE = 5 * indsize, le programme s'arrête plus tôt. Il fait moins d'évaluations, donc il a moins de temps pour trouver la meilleure solution. Ici, il arrive à 19 au lieu de 20.

3. L'affichage permet de voir si la fitness augmente pendant les générations. On voit que les individus ont de plus en plus de 1 jusqu'à atteindre 20.

4. Le fichier CSV garde les résultats de chaque génération : la moyenne, le minimum et le maximum des fitness. Avec Excel, on peut faire un graphique pour voir l'évolution.

5. On peut changer la taille du tournoi, la probabilité de croisement et la probabilité de mutation. Ces valeurs changent la vitesse à laquelle l'algorithme trouve une bonne solution.

> [!warning] À finir
> - [x] Finir Q3.

Exercice 3.

1,2, fait sur sur pycharm.

3. le problème de base c'est qu'on utilise np.argmax dans la sélection et le remplacement, ce qui pousse l'algorithme à maximiser le score. C'était parfait pour maxOnes, mais la fonction d'Ackley demande de minimiser vers 0. Du coup, l'algo cherche la pire solution possible au lieu de la meilleure. En plus de ça, 200 évaluations (MAX_NFE) c'est beaucoup trop court pour explorer l'espace continu, et 10 bits par variable donne un découpage trop brut pour tomber précisément sur (0,0)

4. Non j'arrive pas. le meilleur encodage sur 10 bits par variable approche x,y = +ou- 0.0048, avec Ackley ≈ 0.0208. La valeur exacte (0,0) reste inaccessible avec cette résolution, car zéro ne correspond pas à un entier dans le codage sur [−5,5]; augmenter le nombre de bits par variable permet de s’en rapprocher davantage. Pour corriger ça, il faudrai basculer en np.argmin dans tout le code, monter MAX_NFE à 5,000 ou 10,000, et passer à 40 bits au total (20 bits par variable) pour gagner en précision. 


## Difficultés rencontrées

- pas evident pour l'exercice 3 car je comprends pas ou je met le script exactement...
- 2 eme soucis je vois pas comment remplacer la fonction correctement.


## Liens

- [[Accueil R511-Optimisation]]
