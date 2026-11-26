---
type: td
module: R504-Qualite-Algorithmique
type_seance: TD
semaine: 
date: 
status: à-faire
tags:
  - but-info
  - real
  - td
  - qualite-algorithmique
---

# TD1 - Terminaison et invariants de boucle

> [!info] Séance
> - **Module** : Qualité algorithmique (R504)
> - **Type** : TD
> - **Date** : 
> - **Groupe** : 

---

## Sujet / Enoncé

![[td_1_correction.pdf]]

Suite du TD :
![[td_1_correction_suite.pdf]]

## Réponses / Solutions

### 1.1 Terminaison d'un algorithme : les convergents

Pour prouver qu'un algorithme se termine sur toute entrée, il faut montrer qu'une **condition de terminaison** est forcément atteinte. Méthodes :
- **Boucle** : utiliser un **convergent** — la variable du test de boucle converge vers la valeur qui interrompt la boucle.
- **Récursivité** : montrer que la suite des arguments récursifs converge vers le **cas de base**.

### 1.2 Prouver que l'algorithme calcule toujours le résultat attendu : les invariants de boucle

**Invariant de boucle** $P(j)$ (avec $j$ = numéro d'itération) :
- Vrai à l'entrée ($j = 0$ ou $j = 1$)
- Si $P(j)$ vrai, alors $P(j+1)$ vrai (passage prouvé par récurrence)
- À la dernière itération, $P(j)$ implique la **correction du résultat**

Pour un algorithme récursif → preuve par **récurrence** sur les appels récursifs.

### Convergent : une boucle simple

1. L'algorithme se termine quand `i <= 0`

## Difficultés rencontrées

- 

## Liens

- [[Accueil R504-Qualite-Algorithmique]]