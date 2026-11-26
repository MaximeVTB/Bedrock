---
type: td
module: R508-Qualite-Developpement
type_seance: TD
semaine: 
date: 
status: à-faire
tags:
  - but-info
  - real
  - td
  - qualite-developpement
  - unix
---

# TD1 - Répertoires et fichiers UNIX

> [!info] Séance
> - **Module** : Qualité de développement (R508)
> - **Type** : TD
> - **Date** : 
> - **Groupe** : 

---

## Sujet / Enoncé

![[01-Fichiers Répertoires Gestion Avancée_EX 1.pdf]]

# 1. Répertoires et fichiers sous UNIX

## Ex1 : Lister le contenu de votre répertoire personnel

1. `ls`
2. `ls -l`
3. `ls -a`
4. `ls --color=auto -r`
5. `ls -lat`
6. `ls -latr`

## Ex2 : Répertoires

1. `mkdir envinfo1`
2. `mkdir envinfo1/td3 envinfo1/td4 envinfo1/td5`
3. `cd envinfo1`
4. `mkdir td6 td7 td8`
5. À la 2, tu es dans ton répertoire personnel, donc tu dois donner le chemin complet... Mais à la 4, tu es déjà dans `envinfo1`, donc tu donnes juste les noms sans chemin.
6. `mkdir -p eval/qcm1 eval/qcm2`

## Ex3 : Arborescence et chemin

1. `cd eval/qcm1`
2. `cd` me fait me retrouver dans mon répertoire personnel (`~`, le home)
3. `cd envinfo1/eval/qcm1`
	- La commande n'est pas la même, car un chemin relatif dépend de là où je me trouve
	- À la question 1 tu étais dans `envinfo1`, maintenant tu es dans le home, donc il faut un chemin relatif plus long
4. `cd /home/envinfo1`
5. `echo $HOME`
6. 
- Absolu (racine) : `cd /home/envinfo1/eval`
- Absolu (depuis le home) : `cd ~/envinfo1/eval`
- Relatif (depuis qcm1) : `cd`

## Ex4 : Fichiers et répertoires

1. `touch controle1.txt controle2.txt controle3.txt`
2. `mkdir controles`
3. `mv controles examens`
4. `mv controle1.txt`
5. `cd examens` et ensuite executer `cp * ../qcm1`
6. `cd ../qcm1` et puis `touch question1.txt question2.txt question3.txt`

## Ex5 : Suppression de répertoire et de fichiers

1. Ça ne fonctionne pas car `rmdir` ne supprime que les répertoires vides
2. `rmdir ../qcm2` (qcm2 est vide, donc `rmdir` fonctionne)
3. `cd .. && cp -r qcm1 qcm2`
4. `cd qcm2`
5. `rm controle*`
6. `touch .reponses.txt`
7. `ls -la`
8. `rm -r ../qcm1`

## Ex6 : Joker

1. `touch ../eval/qcm1.txt ../eval/Qcm2.doc ../eval/QCm3.txt ../eval/QCM4.doc`
2. `ls ../eval/Q*`
3. `??`
4. `ls ../eval/*.txt`
5. `rm ../eval/q* ../eval/Q*`

## Ex7 : Pour conclure, on utilise un peu tout


## Difficultés rencontrées

- 

## Liens

- [[Accueil R508-Qualite-Developpement]]