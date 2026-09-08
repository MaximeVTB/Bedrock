---
type: cours
module: R508-Qualite-Developpement
semaine: 1
date: 2026-09-07
status: termine
tags:
  - but-info
  - real
  - cours
---

# Qualité de développement — Cours 1 : Environnement & interpréteur de commandes

## Contexte du cours

- Documentation & revue de codes

---

## L'interpréteur de commandes (le shell)

C'est le programme qui **écoute ce que tu tapes au clavier** et qui **exécute tes commandes**.

> Tu tapes une commande → il la lit → il la comprend (il « l'interprète ») → il la fait.

Exemples de commandes : `ls`, `cd`, `mkdir`... C'est lui qui les lance pour toi.

---

## Les chemins

Un **chemin** (path) = l'**adresse** d'un fichier ou d'un dossier sur le disque.

- **Chemin absolu** : part de la racine `/` (tout en haut du disque).
  Ex : `/home/etu/tp1`
- **Chemin relatif** : part de là où tu es actuellement.
  Ex : `../tp1` (remonte d'un dossier, puis va dans `tp1`)

### Symboles à connaître

| Symbole | Signification |
| --- | --- |
| `.` | Le dossier où tu es (= ici) |
| `..` | Le dossier parent (celui d'au-dessus) |
| `~` | Ton dossier personnel (home) |
| `/` | La racine du disque (tout en haut) |

---

## Commandes de base à savoir

| Commande | Effet |
| --- | --- |
| `pwd` | Affiche où tu es (print working directory) |
| `ls` | Liste les fichiers du dossier |
| `ls -l` | Liste avec détails (droits, taille, date...) |
| `ls -a` | Liste aussi les fichiers cachés |
| `cd nom` | Entre dans le dossier `nom` |
| `cd ..` | Remonte d'un dossier |
| `cd ~` | Va dans ton dossier personnel |
| `cd /` | Va à la racine |
| `mkdir nom` | Crée un dossier |
| `touch nom` | Crée un fichier vide |
| `cat nom` | Affiche le contenu d'un fichier |
| `rm nom` | Supprime un fichier |

---

## Les droits rwx

Chaque fichier / dossier a des **droits** qui disent **qui** peut faire **quoi**.

- **r** = read = **lire** le fichier (ou lister le dossier)
- **w** = write = **écrire / modifier**
- **x** = execute = **exécuter** (lancer un programme, ou entrer dans un dossier)

---

## Les 9 (ou 10) bits des droits

Avec `ls -l`, les droits s'affichent comme une chaîne de lettres.

### Le 1er caractère = le type

- `-` = fichier normal
- `d` = dossier (directory)

### Ensuite : 9 caractères = 3 groupes de 3, pour 3 « personnes »

1. **Le propriétaire** (user) → `rwx`
2. **Le groupe** (group) → `rwx`
3. **Les autres** (others) → `rwx`

Chaque lettre peut être remplacée par `-` si le droit n'est **pas** accordé.

### Exemple 1 : `-rwxr-xr--`

- `-` → fichier normal
- Propriétaire : `rwx` → peut tout faire (lire, écrire, exécuter)
- Groupe : `r-x` → peut lire et exécuter, mais pas écrire
- Autres : `r--` → peut seulement lire

### Exemple 2 : `drwxr-xr-x`

- `d` → dossier
- Propriétaire : `rwx` → peut tout faire
- Groupe : `r-x` → lire + exécuter, pas écrire
- Autres : `r-x` → lire + exécuter, pas écrire

> Astuce mnémotechnique : on lit toujours de gauche à droite : type → propriétaire → groupe → autres.