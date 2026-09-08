---
type: accueil
universite: IUT Nice Côte d'Azur — Site de Sophia Antipolis
formation: BUT Informatique — Parcours Réalisation d'Applications (R)
annee: 3ème année (Semestres 5 & 6)
annee_debut: 2026-09-04
status: en-cours
deadline: 2027-06-30
---

# BUT INFO — Réalisation d'Applications — 3e année

> [!info] IUT Nice Côte d'Azur — Site de Sophia Antipolis
> Formation **BUT Informatique**, parcours **Réalisation d'Applications (Real)**.
> Année universitaire **2026-2027**.

---

## 1. Organisation des dossiers

| N°  | Dossier                                              | Contenu                            |
| --- | ---------------------------------------------------- | ---------------------------------- |
| 01  | [[_Index_01-Cours\|Cours]]                           | Notes de cours par module (R5xx)   |
| 02  | [[_Index_02-TD-TP\|TD / TP]]                         | Travaux dirigés et pratiques       |
| 03  | [[_Index_03-Projets\|Projets]]                       | SAE et projets personnels          |
| 04  | [[_Index_04-Stages-Alternance\|Stages / Alternance]] | Stage de fin de BUT, alternance    |
| 05  | [[_Index_05-Examens\|Examens]]                       | Contrôles, partiels, rattrapages   |
| 06  | [[_Index_06-Dossiers-Actions\|Dossiers & Actions]]   | Démarches, dossiers à rendre       |
| 07  | [[_Index_07-Administratif\|Administratif]]           | Emploi du temps, scolarité, badges |
| 08  | [[_Index_08-Notes-Personnelles\|Notes personnelles]] | Notes libres, brouillons           |

---

## 2. Suivi général

> [!tip] Automatique
> Les tableaux ci-dessous se mettent à jour dès que tu remplis les propriétés d'une note (type, module, deadline, status...). Aucun tri manuel à faire.

### 2.0 — Informations générales

- [[Parcours REAL|Informations sur le parcours REAL]]

### 2.1 — Cours

```dataview
TABLE regexreplace(module, "-", " - ") AS "Cours", date AS "Date", status AS "État"
FROM "UNICA/BUT-INFO/REAL-3A/01-Cours"
WHERE type = "cours"
SORT module ASC
```

### 2.2 — SAE & Projets

```dataview
TABLE titre_projet AS "SAE / Projet", deadline AS "Livraison", status AS "État"
FROM "UNICA/BUT-INFO/REAL-3A"
WHERE contains(file.tags, "#sae") OR type = "sae" OR type = "projet"
SORT deadline ASC
```

### 2.3 — Examens & Contrôles

```dataview
TABLE module AS "Module", date AS "Date", heure AS "Heure", salle AS "Salle", status AS "État"
FROM "UNICA/BUT-INFO/REAL-3A"
WHERE type = "examen"
SORT date ASC
```

### 2.4 — Dossiers & Administratif

```dataview
TABLE titre AS "Titre", deadline AS "Échéance", destinataire AS "Destinataire", status AS "État"
FROM "UNICA/BUT-INFO/REAL-3A"
WHERE type = "dossier" OR type = "admin"
SORT status ASC, deadline ASC
```

---

## 3. Mes modules (Semestre 5)

| Module | Intitulé | Dossier |
| --- | --- | --- |
| SAE 3 | Projet / SAE de semestre | [[SAE 5 - Exemple\|Voir]] |
| R501 | Initiation au management d'une équipe de projet | [[Accueil R501-Management-Projet\|Accueil]] |
| R504 | Qualité algorithmique | [[Accueil R504-Qualite-Algorithmique\|Accueil]] |
| R505 | Programmation avancée | [[Accueil R505-Programmation-Avancee\|Accueil]] |
| R507 | Automatisation de la chaîne de production | [[Accueil R507-Automatisation-Production\|Accueil]] |
| R508 | Qualité de développement | [[Accueil R508-Qualite-Developpement\|Accueil]] |
| R509 | Virtualisation avancée | [[Accueil R509-Virtualisation\|Accueil]] |
| R511 | Méthodes d'optimisation pour l'aide à la décision | [[Accueil R511-Optimisation\|Accueil]] |
| R512 | Modélisations mathématiques | [[Accueil R512-Modelisation-Math\|Accueil]] |
| R514 | Anglais | [[Accueil R514-Anglais\|Accueil]] |

---

## 4. Ma feuille de route

- [x] Récupérer l'emploi du temps → [[Emploi du temps]]
- [ ] Récupérer le calendrier universitaire → [[Calendrier]]
- [ ] Lister les modules et leurs codes
- [ ] Créer les notes de chaque module
- [ ] Noter les dates clés (examens, SAE, stage)

---

## 5. Liens utiles

- Site IUT Nice : https://iut.univ-cotedazur.fr
- Espace numérique de travail (ENT) : https://ent.univ-cotedazur.fr
- Emploi du temps : https://edt.univ-cotedazur.fr/portal/
- Groupe de TD : à compléter
- Numéro étudiant : à compléter
- Justificatif des absences : https://iut-scodoc.univ-cotedazur.fr/
- Support cours (Moodle) : https://lms.univ-cotedazur.fr/
- Status et reglement interieur : https://butinfo.univ-cotedazur.fr

---

## 6. Tags utilisés

- `#but-info` — toutes les notes du BUT INFO
- `#real` / `#r3a` — parcours Réalisation, 3ème année
- `#cours`, `#td`, `#tp`, `#sae`, `#examen`, `#dossier`, `#admin`
