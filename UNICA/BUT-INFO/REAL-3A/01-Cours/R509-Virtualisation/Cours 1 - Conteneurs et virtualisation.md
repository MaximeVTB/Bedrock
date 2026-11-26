---
type: cours
module: R509-Virtualisation
semaine: 
date: 
status: à-voir
tags:
  - but-info
  - real
  - cours
  - virtualisation
  - conteneurs
---
# Cours 1 - Conteneurs et virtualisation

> [!info] Informations
> - **Module** : Virtualisation (R509)
> - **Enseignant** : 
> - **Date** : 
> - **Salle** : 

---

## Définition : Conteneur

Un conteneur est une unité d'application qui regroupe son code et toutes ses dépendances pour que l'application s'exécute rapidement et de manière fiable d'un environnement informatique à un autre. Contrairement à une machine virtuelle, un conteneur partage le noyau (kernel) du système d'exploitation hôte avec les autres conteneurs, ce qui le rend beaucoup plus léger et plus performant.

## Caractéristiques principales

- **Léger** : pas de système d'exploitation complet à embarquer, seulement les dépendances de l'application
- **Portable** : fonctionne de la même manière sur n'importe quelle machine disposant du moteur d'exécution de conteneurs (ex. Docker)
- **Isolé** : chaque conteneur possède son propre espace de noms (namespace) pour les processus, le réseau et le système de fichiers
- **Ordonnançable** : peut démarrer, stopper, déplacer et reproduire en quelques secondes

## Exemple d'utilisation

Une application web Java conteneurisée avec Docker peut être déployée sur un serveur local, dans le cloud ou en production sans se soucier des différences de configuration entre les machines.

## Liens

- [[Accueil R509-Virtualisation]]