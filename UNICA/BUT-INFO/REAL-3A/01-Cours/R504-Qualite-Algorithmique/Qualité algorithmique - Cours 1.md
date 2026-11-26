---
type: cours
module: R504-Qualite-Algorithmique
semaine: 1
date: 2026-09-07
status: termine
tags:
  - but-info
  - real
  - cours
---

# Qualité algorithmique — Cours 1 : Notions de base & complexité

> [!info] Programme national
> QUALITé ALGO — Réfléchir aux meilleures manières de réfléchir à un algo
> 
> - 2h TD par semaine jusqu'au 2 Nov.
> - DS final : 9 Nov.

---

## Définition d'un algorithme

> **Algo** : suite finie et séquentielle de règles que l'on applique à un nombre fini de données en respectant une chronologie respectée.

## 3 problèmes fondamentaux

1. **Complexité** — combien de temps va-t-il atteindre le résultat escompté ?
2. **Calculabilité** — existe-t-il des tâches pour lesquelles il n'existe aucun algorithme ?
3. **Correction** — l'algorithme fait-il ce qu'il est censé faire ?

## Préconditions & Postconditions

**Préconditions** — quels types de données sont traitées ? (chaîne, entiers, etc.) + quelles conditions sur les données ? (entiers positifs, non nuls, tableaux triés...)

**Postconditions** — que renvoie le code après exécution.

> **Assertions** : propriété liant les données d'entrée et les variables des méthodes.

---

## Complexité en espace

- La place nécessaire pour stocker les données.
- Si `l` contient $n$ éléments, on dit : **complexité en espace de l'ordre de $n$**.

## Complexité en temps

- **Temps CPU** : dépend de la machine.
- **Temps de l'algo** : mesures indépendantes de la machine.

Exemple : on fait au plus `len(l)` passages dans la boucle while.
- Taille des données : $n = \text{len}(l)$
- Opération effectuée dans la boucle : une comparaison d'entiers
- Complexité en temps dans le **meilleur des cas** : 1 (quand `e` est l'élément d'indice 0)
- Recherche de 6 dans {3,4,6,10,34} → 2
- Recherche de 31 dans {3,4,6,10,34} → -1

---

## Notions de complexité (notations asymptotiques)

![[WhatsApp Image 2026-09-07 at 03.54.45.jpeg|674]]

### Grand O ($O$) : Pire des cas / Borne supérieure

- La fonction $f(n)$ ne grandira jamais plus vite que $g(n)$ (à une constante près $C$), à partir d'un certain seuil $n_0$.
- Utilisé pour définir le **pire scénario possible** ou la **limite maximale** de complexité (temps ou mémoire). Garantit que le programme ne sera pas plus lent que cette limite.
- **Exemple** : un tri à bulles est en $O(n^2)$ : au pire, il fera de l'ordre de $n^2$ opérations.

### Grand Oméga ($\Omega$) : Meilleur des cas / Borne inférieure

- La fonction $f(n)$ grandira au moins aussi vite que $g(n)$ (à une constante près $C$), pour $n$ suffisamment grand.
- Utilisé pour définir le **meilleur scénario possible** ou la **limite minimale** de complexité.
- **Exemple** : chercher un élément dans un tableau non trié prend au minimum $\Omega(1)$ (si l'élément est le premier du tableau).

### Grand Thêta ($\Theta$) : Cas moyen / Borne exacte

- La fonction $f(n)$ est encadrée par $g(n)$ à la fois au-dessus et en-dessous. $f(n)$ et $g(n)$ ont exactement le même ordre de grandeur asymptotique.
- Utilisé pour donner une **évaluation exacte** du comportement de l'algorithme quand pires et meilleurs cas sont du même ordre.
- **Exemple** : le tri fusion a une complexité garantie en $\Theta(n \log n)$.

---

## Recherche dichotomique (cas trié)

- Le même algo que dans le cas non trié, mais dès que l'on trouve un élément plus grand, on s'arrête.
- Utiliser le fait que les éléments sont ordonnés pour appliquer le paradigme **diviser pour régner**.

## Diviser pour régner

On considère un problème de taille $n$, qu'on découpe en $a$ sous-problèmes de taille $n/b$.

Le paradigme repose sur **3 étapes** :
1. **Diviser** : décomposer le problème initial en $a$ sous-problèmes de taille $n/b$
2. **Régner** (conquérir) : résoudre chaque sous-problème récursivement (cas de base = problème suffisamment petit pour être résolu directement)
3. **Combiner** : assembler les solutions des sous-problèmes pour obtenir la solution du problème initial

**Relation de récurrence** :
$$T(n) = a \cdot T\left(\frac{n}{b}\right) + f(n)$$

où :
- $a$ = nombre de sous-problèmes
- $n/b$ = taille de chaque sous-problème
- $f(n)$ = coût de la division + de la combinaison (hors récursion)

**Exemple : Recherche dichotomique**
- $a = 1$ (un seul sous-problème)
- $b = 2$ (on divise la taille par 2)
- $f(n) = O(1)$ (une seule comparaison)

Donc $T(n) = T(n/2) + O(1)$, soit $T(n) = O(\log n)$.

---

## PGCD — Plus Grand Commun Diviseur

Le PGCD de deux entiers $a$ et $b$ est le plus grand entier qui divise à la fois $a$ et $b$.

**L'idée** : tant que le 2e nombre n'est pas 0, on remplace $(a, b)$ par $(b, a \bmod b)$. Quand $b$ vaut 0, $a$ est le PGCD.

$$\text{PGCD}(a, b) = \begin{cases} a & \text{si } b = 0 \\ \text{PGCD}(b,\ a \bmod b) & \text{sinon} \end{cases}$$

**Exemple** : $\text{PGCD}(48, 18)$
- $48 \bmod 18 = 12$ → $(18, 12)$
- $18 \bmod 12 = 6$ → $(12, 6)$
- $12 \bmod 6 = 0$ → $(6, 0)$ → **PGCD = 6**

PGCD(x,y) = PGCD(a,b)

### Algorithme d'Euclide

- L'algo se termine si la condition d'arrêt de la boucle se réalise.
- **Condition d'arrêt** : $b = 0$
- Au départ $b$ diminue strictement à chaque passage (car $0 \le a \bmod b < b$). La « taille » du problème (b) décroît à chaque itération → on finit forcément par atteindre le cas $b = 0$.

**Correction** : l'algorithme d'Euclide est correct car on ne modifie jamais le PGCD en passant de $(a, b)$ à $(b, a \bmod b)$.

**Invariant de boucle** : $\text{PGCD}(a, b)$ reste constant à chaque itération.

**Preuve** : $\text{PGCD}(a, b) = \text{PGCD}(b, a \bmod b)$, car $a \bmod b = a - \lfloor a/b \rfloor \cdot b$ est une combinaison linéaire de $a$ et $b$ → mêmes diviseurs communs.

**Conclusion** : à la sortie, $b = 0$ et $\text{PGCD}(a, 0) = a$ → l'algo renvoie bien le PGCD de départ (préservé par l'invariant).

---

## Invariant de boucle

> On appelle **invariant de boucle** une propriété qui, si elle est vraie avant l'entrée dans une boucle, reste vraie après chaque passage dans cette boucle, et donc est vraie aussi à la sortie de cette boucle.
