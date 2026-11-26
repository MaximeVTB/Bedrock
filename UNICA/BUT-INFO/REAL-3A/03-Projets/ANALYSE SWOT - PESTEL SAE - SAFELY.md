
# Analyses Stratégiques — Projet SAFELY

Ce document regroupe les analyses **PESTEL** et **SWOT** du dispositif **SAFELY** (bracelet de sécurité autonome, géolocalisé avec capteurs biométriques et connectivité GSM/BLE), accompagnées d'une recommandation pour votre présentation devant un jury.

---

## 1. Analyse PESTEL

L'analyse PESTEL étudie les facteurs macro-environnementaux pouvant impacter le projet SAFELY.

### **P — Politique**
* **Soutien aux politiques de sécurité publique :** Volonté gouvernementale forte de lutter contre les agressions, les violences faites aux femmes et d'améliorer la sécurité urbaine.
* **Intégration avec les services d'urgence :** Besoin d'accords ou de passerelles d'homologation avec les autorités publiques (police, gendarmerie, secours).
* **Contexte réglementaire télécoms :** Dépendance vis-à-vis des politiques nationales d'attribution des fréquences réseau et d'accès aux cartes SIM/eSIM.

### **E — Économique**
* **Inclusion financière (Mobile Money) :** Prise en compte des moyens de paiement locaux (**Orange Money**, **MTN Mobile Money**), facilitant l'adoption dans les zones à faible bancarisation.
* **Pouvoir d'achat et modèle d'abonnement :** Nécessité d'adapter le prix du bracelet matériel et le tarif mensuel de l'abonnement au pouvoir d'achat de la cible.
* **Coûts d'infrastructure :** Impact de l'inflation sur les composants électroniques (puces GSM, capteurs PPG) et les frais d'itinérance/connectivité cellulaire.

### **S — Socioculturel**
* **Sentiment d'insécurité croissant :** Demande en hausse pour des solutions personnelles d'assistance rapide (pour les femmes, les seniors, les travailleurs isolés, les étudiants).
* **Acceptabilité des wearables de sécurité :** Évolution positive des mentalités envers les objets connectés portables, perçus comme des éléments rassurants.
* **Sensibilité à la stigmatisation :** Le bracelet doit ressembler à un accessoire du quotidien pour ne pas désigner le porteur comme une cible vulnérable.

### **T — Technologique**
* **Connectivité hybride (BLE + GSM/SMS) :** Autonomie fonctionnelle garantissant la transmission d'alertes même en l'absence de smartphone ou de couverture réseau haut débit.
* **Fiabilité des capteurs biométriques :** Avancées sur les capteurs de fréquence cardiaque (PPG) et accéléromètres pour réduire le taux de faux positifs (chutes, stress).
* **Gestion de l'énergie :** Enjeu crucial de l'optimisation de la batterie pour un appareil fonctionnant en transmission GSM continue ou périodique.

### **E — Écologique**
* **Recyclabilité et gestion des e-déchets :** Alignement avec les directives environnementales (DEEE, RoHS) concernant les batteries au lithium et l'électronique.
* **Consommation énergétique :** Conception à faible consommation pour prolonger la durée de vie globale du produit et espacer les recharges.

### **L — Légal & Réglementaire**
* **Protection des données personnelles (RGPD / Lois locales) :** Gestion très stricte des données de géolocalisation et de santé (fréquence cardiaque).
* **Consentement préalable :** Obtention obligatoire du consentement des contacts de confiance (ex: validation via SMS comme stipulé dans la US19).
* **Normes matérielles et radio :** Respect des réglementations d'émissions d'ondes (ex: marquage CE, certification FCC) pour les appareils portés au poignet.

---

## 2. Analyse SWOT

L'analyse SWOT résume les forces, faiblesses, opportunités et menaces propres au projet SAFELY.

| FORCES (Strengths) | FAIBLESSES (Weaknesses) |
| :--- | :--- |
| • Autonomie réseau (GSM/SMS sans smartphone)<br>• Multiples modes de déclenchement (SOS, Voix, Cardio)<br>• Paiements adaptés au marché (Mobile Money)<br>• Réseau communautaire (répondants de proximité) | • Coût de production et de connectivité cellulaire<br>• Risque de faux positifs (cardiaque/chutes)<br>• Dépendance à l'autonomie de la batterie<br>• Image de marque et notoriété à construire |

| OPPORTUNITÉS (Opportunities) | MENACES (Threats) |
| :--- | :--- |
| • Forte hausse de la demande d'équipements de sûreté<br>• Partenariats stratégiques (Opérateurs, Assurances)<br>• Déploiement dans d'autres zones géographiques | • Concurrence des montres connectées grand public<br>• Risques d'indisponibilité du réseau GSM local<br>• Évolution rapide du cadre légal sur les données |

### **Detail des Forces (Strengths)**
1. **Autonomie complète :** Fonctionnement autonome sans dépendre de la présence du smartphone grâce au module GSM/SMS.
2. **Déclenchement multi-modal :** Combinaison de bouton SOS, déclenchement vocal et détection automatique (fréquence cardiaque/immobilité).
3. **Ancrage local et accessibilité :** Intégration native des modes de paiement locaux (Orange Money, MTN Mobile Money).
4. **Modèle collaboratif :** Alerte transmise non seulement aux proches, mais aussi aux répondants de proximité.

### **Détail des Faiblesses (Weaknesses)**
1. **Autonomie de batterie limitée :** Le module cellulaire et la géolocalisation continue consomment de l'énergie.
2. **Gestion des faux positifs :** Risque d'alertes intempestives via les détections cardiaques ou vocales si l'algorithme n'est pas parfaitement calibré.
3. **Coût du matériel :** Intégrer un GPS, un modem GSM, une carte SIM et des capteurs de santé augmente le coût unitaire du bracelet.

### **Détail des Opportunités (Opportunities)**
1. **Expansion sur de nouveaux marchés :** Marché des personnes âgées (téléassistance), travailleurs isolés (PTI/DATI) ou enfants.
2. **Partenariats institutionnels :** Collaborations avec des compagnies d'assurance, des universités, des entreprises ou des ONG.
3. **Synergie avec les télécoms :** Partenariats avec des opérateurs (Orange, MTN) pour des forfaits M2M pré-intégrés.

### **Détail des Menaces (Threats)**
1. **Concurrence des Smartwatches :** Ajout direct de fonctionnalités SOS par les géants de la tech (Apple, Samsung).
2. **Pannes ou zones blanches de réseau :** Risque d'incapacité de transmettre l'alerte en l'absence complète de couverture réseau cellulaire.
3. **Contraintes réglementaires sur la santé :** Risque d'être reclassé comme « dispositif médical » en cas d'utilisation avancée des données physiologiques.

---

## 3. Quelle analyse privilégier devant un jury ?

### **Verdict : Utilisez le SWOT (avec une brève contextualisation PESTEL)**

* **Pourquoi le SWOT est le plus adapté ?**
  1. **Synthétique et direct :** Il permet d'expliquer la proposition de valeur de SAFELY en **1 ou 2 diapositives**.
  2. **Centré sur le produit :** Le jury cherche avant tout à comprendre pourquoi **votre bracelet** est meilleur que la concurrence et quels sont vos défis opérationnels.
  3. **Aligné avec vos User Stories :** Vous pouvez facilement relier vos forces (ex: *Autonomie GSM*) aux User Stories prioritaires du MVP (US61-63).

* **Comment l'amener intelligemment devant le jury ?**
  1. Consacrez **1 slide au SWOT** pour montrer la viabilité du projet.
  2. Utilisez le PESTEL simplement en **introduction** (1-2 phrases à l'oral) pour poser le cadre : *« Dans un contexte de besoin accru de sécurité (Socioculturel) et grâce aux réseaux cellulaires bas débit et au Mobile Money (Technologique & Économique), nous avons développé SAFELY... »*.

---

## 4. Sources & Références

Voici les sources et cadres de référence exploitables pour étayer ces analyses dans votre rapport ou présentation :

1. **Cadres méthodologiques :**
   * *Johnson, G., Scholes, K., & Whittington, R.* — **Stratégique (Exploring Corporate Strategy)** : Référence académique pour l'utilisation des matrices SWOT et PESTEL.
2. **Normes & Télécoms :**
   * **GSM Association (GSMA) — Mobile Economy Reports :** Données sur la couverture des réseaux cellulaires et l'adoption du Mobile Money (Orange Money, MTN Mobile Money).
   * **Normes IoT / BLE :** Spécifications Bluetooth SIG pour le Bluetooth Low Energy (BLE) et normes GSM M2M pour les objets connectés autonomes.
3. **Réglementation & Protection des données :**
   * **RGPD (Règlement Général sur la Protection des Données) :** Cadre légal sur la collecte de la géolocalisation et des données de santé personnelles.
