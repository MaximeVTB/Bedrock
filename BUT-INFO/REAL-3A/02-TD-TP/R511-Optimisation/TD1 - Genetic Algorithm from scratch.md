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

1. Avec la même seed, on obtient toujours la même population au début et le même résultat à la fin. Avec une seed aléatoire, le résultat change à chaque exécution.

11. Avec MAX_NFE = 5 * indsize, le programme s'arrête plus tôt. Il fait moins d'évaluations, donc il a moins de temps pour trouver la meilleure solution. Ici, il arrive à 19 au lieu de 20.

13. L'affichage permet de voir si la fitness augmente pendant les générations. On voit que les individus ont de plus en plus de 1 jusqu'à atteindre 20.

14. Le fichier CSV garde les résultats de chaque génération : la moyenne, le minimum et le maximum des fitness. Avec Excel, on peut faire un graphique pour voir l'évolution.

15. On peut changer la taille du tournoi, la probabilité de croisement et la probabilité de mutation. Ces valeurs changent la vitesse à laquelle l'algorithme trouve une bonne solution.

> [!warning] À finir
> - [ ] Finir Q3.

Question 3.

## Difficultés rencontrées

- 

## Liens

- [[Accueil R511-Optimisation]]
