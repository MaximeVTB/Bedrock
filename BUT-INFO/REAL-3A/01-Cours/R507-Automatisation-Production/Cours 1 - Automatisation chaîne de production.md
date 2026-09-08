---
type: cours
module: R507-Automatisation-Production
semaine: 1
date: 2026-09-08
status: fait
tags:
  - but-info
  - real
  - cours
  - R507
---

# Cours 1 — Automatisation de la chaîne de production

![[Cours1-Automatisationchainedeprod.pdf]]

## Objectif de l'intégration continue

- Livrer rapidement aux clients les changements apportés à une solution logicielle
- Tout en garantissant / maintenant / améliorant sa qualité

Pour livrer et mettre à jour rapidement du logiciel, il faut pouvoir faire de l'itératif et incrémental :
- Avoir une architecture cassée et buildée
- Méthodologie présente pour optimiser le temps
  - Cela réduit le temps d'interventions manuelles et automatise la livraison/maintenance

Observer/analyser le comportement de son logiciel.

---

## Différentes versions/phases du build de son logiciel

![[Pasted image 20260908021953.png]]

---

## Définition

> Une méthode de développement logiciel dans laquelle le logiciel est reconstruit et testé à chaque modification apportée par un programmeur.

---

## Comment mettre en place l'IC (Intégration Continue)

1. Un dépôt de code source
2. Un mécanisme pour construire automatiquement du logiciel
3. Une « plateforme » pour exécuter des tests
4. Un outil qui fait la glue entre 1, 2, et 3 (Jenkins, GitHub Action, GitLab Runner)

---

## DevOps

- **Dev** — Développement
- **Ops** — Opérations

![[Pasted image 20260908023152.png]]

---

## Contenu du module

1. Déploiement continu (avec Docker et Docker-compose)
2. Configuration Management (avec Ansible)
3. Techniques de mise à jour et de passage à l'échelle (avec Docker Swarm)
4. Monitoring d'application (avec Prometheus)

---

## Le projet — Technologies

Tant qu'on respecte les contraintes/consignes, nous sommes libres de choisir les technologies de notre choix.

- <font color="#ff0000">Cela veut aussi dire que vous devez être un maximum autonome sur les problèmes liés à vos choix technos (i.e., le prof connaît pas toutes les technos!).</font>
- Les choix des technos doivent être un minimum motivés et une architecture adaptée doit être proposée

![[Pasted image 20260908024021.png]]
