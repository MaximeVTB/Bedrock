
% DUKE-JONES(1) Version 1.0.0 | Manuel des Commandes de Jeux
% Maxime Vatble
% Novembre 2026

# NOM

duke-jones - Incarnez le célèbre aventurier des temps modernes dans une épopée palpitante.

# SYNOPSIS

**duke-jones** [\-hv] [\-d *niveau*] [\-s *fichier*] [\-g *mode*] [*commande*]

# DESCRIPTION

**Duke Jones** est un jeu vidéo d'aventure développé avec toute la rigueur et la structure requises pour garantir une expérience logicielle de qualité. Vous y incarnez Duke Jones, explorateur intrépide, à la recherche d'artefacts perdus à travers des ruines anciennes, des pièges mortels et des environnements high-tech.

Cette page de manuel détaille la ligne de commande pour lancer, configurer et administrer vos sessions de jeu directement depuis votre terminal Linux.

# OPTIONS

`-h`, `--help`
: Affiche l'aide détaillée, la liste des commandes et les raccourcis clavier disponibles en jeu.

`-v`, `--version`
: Affiche le numéro de version actuel du programme Duke Jones et quitte.

`-d`, `--difficulty` *niveau*
: Définit la difficulté de l'aventure. Les valeurs acceptées sont `facile`, `normal`, `expert` et `insane` (par défaut : `normal`).

`-s`, `--save` *fichier*
: Charge une partie sauvegardée existante depuis le chemin de fichier spécifié.

`-g`, `--graphics` *mode*
: Force le moteur d'affichage du jeu (`ascii`, `retro`, ou `modern`).

# EXEMPLES

Lancer une nouvelle partie en mode expert avec le moteur graphique rétro :
> `duke-jones --difficulty expert --graphics retro`

Charger une sauvegarde rapide :
> `duke-jones -s ~/.local/share/duke-jones/save_01.sav`

# FICHIERS

`~/.config/duke-jones/config.json`
: Fichier de configuration utilisateur (résolution, liaisons de touches, volume audio).

`~/.local/share/duke-jones/saves/`
: Répertoire par défaut contenant toutes vos sauvegardes de parties.

# BOGUES

Si vous trouvez des anomalies ou des comportements inattendus, merci de les remonter sur le dépôt Git officiel du projet.

# AUTEUR
Développé par Maxime Vatble