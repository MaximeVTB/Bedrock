---
type: recapitulatif
module: R508-Qualite-Developpement
semaine:
date: 2026-09-21
status: termine
tags:
  - but-info
  - real
  - cours
  - recap
  - qualite-developpement
---

![[Slides BUT3 - TD3-4 - Conte_regex_conte 2.pdf]]

##  1. Introduction au Shell Unix

Le **Shell** est un programme d’interprétation de commandes. C'est l'interface textuelle (le « chef d’orchestre ») qui permet d'interagir directement avec le système Linux.

> [!NOTE] Rôle du Shell
> 
> - Interpréter les commandes saisies par l'utilisateur.
>     
> - Lancer des outils et programmes.
>     
> - Manipuler des répertoires (« boîtes ») et des fichiers (« objets »).
>     
> - **Automatiser des tâches répétitives** en combinant les instructions.
>     

### Les principales familles de Shell

- **C Shell** : Syntaxe inspirée du langage C.
    
- **Bourne Shell** (`sh`) : Historique des systèmes Unix.
    
    - `bash` (_Bourne-Again SHell_) : Le plus courant et le plus utilisé aujourd'hui.
        
    - `zsh` : Syntaxe plus complète, gère des structures de données complexes.
        

##  2. Écriture des Premiers Scripts Shell

Un script Shell est un fichier exécutable dont le nom se termine généralement par l’extension `.sh`.

### Structure de base

1. **L’entête (Shebang)** : Indique obligatoirement quel interprète exécutera le script :
    
    ```
    #!/bin/bash
    ```
    
    _(Le fichier doit ensuite être rendu exécutable via la commande `chmod`)._
    
2. **Les commentaires** : Commencent par `#` (sauf la première ligne du shebang). Ils sont ignorés par le Shell et servent à documenter le code.
    
3. **Commandes internes vs externes** :
    
    - **Internes** : Intégrées directement dans l'interpréteur (ex: `cd`, `echo`, ou les structures de contrôle `if`, `for`, `while`).
        
    - **Externes** : Programmes situés dans les répertoires `/bin` ou `/usr/bin` (ex: `ls`, `mkdir`, `cp`, `rm`) nécessitant la création d’un processus.
        

##  3. Variables, Entrées et Calculs

### La commande `echo`

Sert à afficher du texte ou le contenu d'une variable :

```
echo "Bonjour tout le monde"
echo -n "Texte sans retour à la ligne automatique"
```

### Les types de variables

- **Variables utilisateur** : Tiroirs privés de l'utilisateur (ex: `a`, `my_var`).
    
- **Variables prédéfinies du Shell** : Décrivent l'état du système (`USER`, `HOSTNAME`, `PATH`, `PS1`).
    
- **Paramètres positionnels d'un script** :
    
    - `$0` : Nom du script exécuté.
        
    - `$1` à `$9` : 1er, 2ème... 9ème argument (au-delà : `${10}`).
        
    - `$*` ou `$@` : Ensemble des arguments.
        
    - `$#` : Nombre d'arguments.
        
    - `$?` : Code de retour de la dernière commande (`0` = succès, `≠ 0` = erreur).
        

### Affectations et calculs

- **Affectation simple** : `a=12` _(⚠️ Aucun espace toléré autour du `=`)_.
    
- **Lecture clavier (`read`)** :
    
    ```
    read -p "Entrez votre prénom : " prenom
    ```
    
- **Calculs arithmétiques (`let` ou expansion moderne)** :
    
    ```
    let x=5+3
    # Équivalent moderne recommandé :
    x=$((5+3))
    ```
    
- **Stocker le résultat d'une commande** :
    
    ```
    date_actuelle=$(date)
    ```
    

##  4. Redirections et Traitements par Lots

Un programme manipule trois flux standards :

- `0` : **`stdin`** (Entrée standard / Clavier)
    
- `1` : **`stdout`** (Sortie standard / Écran)
    
- `2` : **`stderr`** (Sortie d'erreur / Écran)
    

### Syntaxe des redirections

- **Rediriger la sortie standard** vers un fichier (écrase le contenu) :
    
    ```
    ls -l > list.txt
    ```
    
- **Ajouter la sortie standard** à la fin d'un fichier (append) :
    
    ```
    ls -l >> list.txt
    ```
    
- **Rediriger la sortie d'erreur** vers un fichier :
    
    ```
    ls tmp 2> err.txt
    ```
    
- **Fusionner les flux** (stdout et stderr dans la même cible) :
    
    ```
    ls fichiers.txt >& 1
    # ou version moderne :
    ls fichiers.txt &> fichier.out
    ```
    
- **Rediriger l'entrée standard** depuis un fichier au lieu du clavier :
    
    ```
    read ligne < fichier.txt
    ```
    

##  5. Tubes (`Pipes`) et Filtres

Le **pipe** (`|`) connecte directement la sortie standard (`stdout`) d'une commande sur l'entrée standard (`stdin`) d'une autre, sans passer par un fichier intermédiaire.

```
cat /etc/passwd | cut -d ":" -f 1 | sort
```

### Commandes et Filtres Essentiels

|   |   |
|---|---|
|**Commande**|**Rôle principal**|
|**`cat`**|Affiche le contenu de fichiers sur la sortie standard.|
|**`more` / `less`**|Affiche un flux ou un fichier page par page.|
|**`cut`**|Découpe et extrait des portions de lignes (ex: délimiteur `-d`, champ `-f`).|
|**`tr`**|Traduit ou supprime des caractères.|
|**`wc`**|Compte les lignes (`-l`), mots (`-w`) ou caractères (`-c`).|
|**`sort`**|Trie les lignes par ordre alphabétique (par défaut).|
|**`uniq`**|Supprime les lignes consécutives identiques.|

##  6. Recherche Avancée : `grep`

`grep` est un moteur de recherche textuel qui analyse ligne par ligne un flux ou un fichier à la recherche d'un motif (_pattern_).

> [!WARNING] Attention `grep` recherche une **chaîne de caractères** et non un mot entier par défaut.

### Syntaxe et Options courantes

```
grep [options] "chaine_recherchee" fichier.txt
```

- `-v` : Inverse la recherche (affiche les lignes _ne contenant pas_ la chaîne).
    
- `-l` : Affiche uniquement les noms des fichiers contenant le motif.
    
- `-s` : Masque les messages d'erreur.
    

### Expressions régulières associées

- `^` : Début de ligne.
    
- `$` : Fin de ligne.
    
- `.` : Caractère quelconque.
    
- `*` : L'élément précédent est présent 0, 1 ou plusieurs fois.
    
- `[]` : Un des caractères compris entre les crochets.