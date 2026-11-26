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

| Commande             | Effet                                                                       |
| -------------------- | --------------------------------------------------------------------------- |
| `pwd`                | Affiche où tu es (print working directory)                                  |
| `ls`                 | Liste les fichiers du dossier (condensé, noms uniquement)                   |
| `ls -l`              | Liste avec détails (droits, propriétaire, taille, date...)                  |
| `ls -a`              | Liste aussi les fichiers cachés (dont le nom commence par `.`)              |
| `ls --color=auto -r` | Colore les noms selon le type + ordre inverse (z→a)                         |
| `ls -lat`            | Format long + cachés + du plus récent au plus ancien (tri par date)         |
| `ls -latr`           | Format long + cachés + du plus ancien au plus récent (tri par date inversé) |
| `cd nom`             | Entre dans le dossier `nom`                                                 |
| `cd ..`              | Remonte d'un dossier                                                        |
| `cd ~`               | Va dans ton dossier personnel                                               |
| `cd /`               | Va à la racine                                                              |
| `mkdir nom`          | Crée un dossier                                                             |
| `touch nom`          | Crée un fichier vide                                                        |
| `cat nom`            | Affiche le contenu d'un fichier                                             |
| `rm nom`             | Supprime un fichier                                                         |

### Les options (flags) de `ls`

| Option | Signification |
| --- | --- |
| `-l` | **l**ong : format détaillé (droits, propriétaire, groupe, taille, date) |
| `-a` | **a**ll : affiche aussi les fichiers cachés (dont le nom commence par `.`) |
| `-t` | **t**ime : trie par date de modification (le plus récent en premier) |
| `-r` | **r**everse : inverse l'ordre du tri (z→a au lieu de a→z, ou ancien→récent) |

> Les options se combinent : `ls -lat` = `-l` + `-a` + `-t`. Ajouter `-r` donne `-latr` (tri inversé).

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

> Astuce mémotechnique : on lit toujours de gauche à droite : type → propriétaire → groupe → autres.



![[Slides BUT3 - TD2.pdf]]

Qualité de développement — Cours 2 : Filtres et outils avancés du shell

## Les tubes ou « pipes » (`|`)
Le symbole `|` (appelé « tube » ou « pipe ») est utilisé pour relier 2 commandes (ou plus) entre elles.
- **Principe** : La sortie standard (`STDOUT`) de la commande de gauche est utilisée comme entrée standard (`STDIN`) de la commande de droite.
- **Syntaxe** : `Commande 1 | Commande 2 | Commande 3`
  - `Commande 1` doit écrire vers `STDOUT`.
  - `Commande 2` doit lire `STDIN` et écrire vers `STDOUT`.
  - `Commande 3` doit lire `STDIN`.

---

## FIND : une recherche approfondie
La commande `find` permet de retrouver des fichiers à partir de certains critères dans un répertoire.
- **Syntaxe** : `find <répertoire de recherche> <critères de recherche>`

### Critères de recherche principaux
| Option / Critère | Signification |
| :--- | :--- |
| `-name` | Recherche sur le nom du fichier (ex: `find /usr -name "*toto*.c" -print`) |
| `-type` | Recherche sur le type (`d` = répertoire, `c` = caractère, `f` = fichier normal) |
| `-user` | Recherche sur le propriétaire du fichier |
| `-mtime n` | Recherche suivant la date de dernière modification (ex: `find / -mtime 3 -print`) |
| `-perm` | Recherche selon les droits (ex: `-perm 755`) |

### Options avancées et actions
- Redirection des erreurs : `find -name "*release*" 2>/dev/null`
- Exécution d'une commande sur les résultats :
  - `find -name core -exec rm {} \;` (exécute sans demander)
  - `find -name core -ok rm {} \;` (demande confirmation avant d'exécuter)

---

## GREP : filtrer des données
La commande `grep` est essentielle pour rechercher du texte ou des motifs (via des expressions régulières) dans des fichiers.
- **Exemples** : 
  - `grep "texte" nomfichier`
  - `grep alias .bashrc`

### Options principales de `grep`
| Option | Signification |
| :--- | :--- |
| `-i` | Ne pas tenir compte de la casse (majuscules / minuscules) |
| `-n` | Connaître les numéros de lignes correspondants |
| `-v` | Inverser la recherche : ignorer/exclure les lignes correspondant au motif |
| `-r` | Rechercher récursivement dans tous les fichiers et sous-dossiers |

---

## Utiliser grep avec des expressions régulières (Regex)
| Caractère spécial | Signification |
| :--- | :--- |
| `.` | Caractère quelconque |
| `^` | Début de ligne |
| `$` | Fin de ligne |
| `[]` | Un des caractères situés entre les crochets |
| `?` | L'élément précédent est optionnel (présent 0 ou 1 fois) |
| `*` | L'élément précédent peut être présent 0, 1 ou plusieurs fois |
| `+` | L'élément précédent doit être présent 1 ou plusieurs fois |
| `\|` | Ou |
| `()` | Groupement d'expressions |

---

## SORT : trier les lignes
La commande `sort` permet de trier le contenu d'un fichier texte.
- **Exemple** : `sort noms.txt`

### Options principales
| Option | Signification |
| :--- | :--- |
| `-o` | Écrire le résultat dans un fichier cible |
| `-r` | Trier en ordre inverse (décroissant) |
| `-R` | Trier aléatoirement |
| `-n` | Trier des nombres (ordre numérique) |

---

## WC : compter le nombre de lignes, mots et octets
`wc` signifie **word count**. Sans paramètre, il renvoie le nombre de lignes, de mots et d'octets.
- **Exemple** : `wc noms.txt` (renvoie par ex: `8 8 64 noms.txt`)

### Options principales
| Option | Signification |
| :--- | :--- |
| `-l` | Compter uniquement le nombre de lignes (`lines`) |
| `-w` | Compter uniquement le nombre de mots (`words`) |
| `-c` | Compter le nombre d'octets (`bytes`) |
| `-m` | Compter le nombre de caractères |

---

## UNIQ : supprimer les doublons
Permet de détecter ou de supprimer les lignes en double (souvent utilisé après un `sort`).
- **Exemples** :
  - `uniq doublons.txt` (affiche le résultat sans filtrage consécutif global si non trié)
  - `uniq doublons.txt sans_doublons.txt`

### Options principales
| Option | Signification |
| :--- | :--- |
| `-c` | Compter le nombre de fois que la ligne est présente (préfixe les lignes du compte) |
| `-d` | Afficher uniquement les lignes présentes en double |

---

## CUT : couper une partie d'un fichier
Permet d'extraire des portions de lignes (par caractères ou par délimiteur).

### 1. Couper selon le nombre de caractères (`-c`)
- `cut -c 2-5 noms.txt` : extrait du 2e au 5e caractère.
- `cut -c-3 noms.txt` : extrait du début jusqu'au 3e caractère.
- `cut -c 3- noms.txt` : extrait du 3e caractère jusqu'à la fin de la ligne.

### 2. Couper selon un délimiteur (`-d` et `-f`)
Idéal pour les fichiers CSV ou tabulés.
- `-d` : indique le délimiteur (ex: `,`).
- `-f` : indique le numéro du ou des champs à couper (`field`).
- **Exemple** : `cut -d ',' -f 1 notes.csv` extrait la première colonne (les noms) d'un fichier CSV de notes.

---

## TR : transformation de caractères
Permet de substituer, presser ou supprimer des éléments pris dans l'entrée standard. Deux chaînes de caractères sont généralement données en argument.
- **Exemple** : `tr '\t' ' '` (remplace les tabulations par des espaces)

### Options principales
| Option | Signification |
| :--- | :--- |
| `-c` | Inverse la recherche (tous les caractères non spécifiés dans la 1re chaîne sont convertis) |
| `-s` | Presse les séquences répétées d'un même caractère en une seule occurrence |
| `-d` | Supprime les caractères spécifiés |

---

## HEAD et TAIL : visualiser le début ou la fin d'un fichier

### HEAD (début de fichier)
- `head -c 1000 /etc/passwd` : Édite à l'écran les 1000 premiers caractères.
- `head -n 10 /etc/passwd` : Édite les 10 premières lignes.

### TAIL (fin de fichier)
- `tail -c 15 /etc/passwd` : Édite les 15 derniers caractères.
- `tail -n 5 /etc/passwd` : Édite les 5 dernières lignes.
- `tail +5 -n /etc/passwd` : Édite la fin du fichier à partir de la 5e ligne.

---

## En résumé
- **`grep`** : Recherche des mots ou motifs (via expressions régulières avec `egrep`) dans un fichier.
- **`sort`** : Trie des lignes de texte (alphabétique ou numérique avec `-n`).
- **`wc`** : Compte les lignes, mots et octets.
- **`uniq`** : Gère et supprime les doublons.
- **`cut`** : Extrait des portions de colonnes ou de caractères.
- **Tubes (`|`)** : Permettent d'enchaîner ces commandes pour créer de puissants pipelines de traitement de données sous Linux.

