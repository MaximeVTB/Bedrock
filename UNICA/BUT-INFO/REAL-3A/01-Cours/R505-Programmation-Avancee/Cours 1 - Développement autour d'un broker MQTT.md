---
type: cours
module: R505-Programmation-Avancee
semaine: 1
date: 2026-09-09
status: à-voir
tags:
  - but-info
  - real
  - cours
  - iot
  - mqtt
  - broker
---

# Cours 1 - Développement autour d'un broker MQTT

> [!info] Informations
> - **Module** : Programmation avancée (R505)
> - **Enseignant** :
> - **Date** : 2026-09-09
> - **Salle** :

---

## IoT (Internet of Things)

Décomposition du sigle IoT:

- **I** — **Internet** : La communication entre l'objet et ses données valorisées. Protocoles réseau : HTTP, MQTT, CoAP, LoRaWAN, Zigbee, BLE...
- **o** — **of** : La glue entre les deux. Développement logiciel et plateforme pour réaliser des services, du développement, de l'analyse de données.
- **T** — **Things** : Les objets connectés eux-mêmes — capteurs, actionneurs, microcontrôleurs (Arduino, ESP32, Raspberry Pi…) qui interagissent avec le monde physique.

### Architecture typique d'un système IoT

1. **Couche perception** — Capteurs / actionneurs (température, luminosité, mouvement…)
2. **Couche réseau** — Protocole de communication (Wi-Fi, LoRa, NB-IoT, Zigbee…)
3. **Couche plateforme** — Collecte, stockage et traitement des données (broker MQTT, cloud, edge computing…)
4. **Couche application** — Services et interfaces utilisateur (tableaux de bord, alertes, automatisation…)

### Protocoles clés

| Protocole | Type | Usage principal |
| --- | --- | --- |
| MQTT | Publish/Subscribe | Messaging léger, très utilisé en IoT |
| CoAP | REST | Protocole REST pour dispositifs contraints |
| HTTP | REST | Usage généraliste, plus lourd |
| LoRaWAN | LPWAN | Longue portée, faible consommation |
| Zigbee | Mesh local | Domotique, réseau maillé court portée |
| BLE | Court portée | Périphériques personnels, beacon |

### Concepts importants

- **Edge computing** : Traitement des données proche de l'objet (latence réduite, moins de bande passante)
- **Digital twin** : Jumeau numérique d'un objet physique pour simulation et monitoring
- **MQTT Broker** : Serveur central de messagerie (ex : Mosquitto, HiveMQ)
- **Retained message / QoS** : Options MQTT pour garantir la livraison ou conserver le dernier état

## Supports de communication & Protocoles dans l'IoT

3 niveaux de communications :

### 1. Couche liaison de données (Data Link / Physical)

Signaux numériques — communication physique entre appareils.

| Technologie                    | Portée | Débit            | Consommation       | Usage typique                                       |
| ------------------------------ | ------ | ---------------- | ------------------ | --------------------------------------------------- |
| **Bluetooth Low Energy (BLE)** | ~10 m  | 1 Mbps           | Très faible        | Montres, capteurs wearables, beacons                |
| **Zigbee**                     | ~100 m | 250 kbps         | Très faible        | Domotique, réseau maillé (philips hue, clashasters) |
| **Z-Wave**                     | ~30 m  | 100 kbps         | Très faible        | Domotique spécifique                                |
| **Wi-Fi (802.11)**             | ~50 m  | jusqu'à 9.6 Gbps | Élevée             | Maison connectée, débit important                   |
| **LoRa**                       | ~15 km | 0.3-50 kbps      | Très faible        | Agriculture, ville intelligente, tracking           |
| **Sigfox**                     | ~50 km | 100 bps          | Extrêmement faible | Capteurs très basse consommation                    |
| **NB-IoT**                     | ~25 km | ~200 kbps        | Faible             | Réseau cellulaire LPWAN                             |
| **LTE-M (Cat-M1)**             | ~15 km | 1 Mbps           | Modérée            | Applications mobiles IoT                            |
| **NFC**                        | ~10 cm | 424 kbps         | N/A (passif)       | Paiement, identification, tag                       |

### 2. Couche réseau (Network / Transport)

Protocoles d'adressage et de routage — acheminer les données de l'objet au serveur.

| Protocole | Rôle | Détails |
| --- | --- | --- |
| **IPv4 / IPv6** | Adressage | IPv6 nécessaire pour le nombre d'objets connectés (2¹²⁸ adresses) |
| **6LoWPAN** | Adaptation IPv6 | Encapsulation IPv6 sur réseaux bas débit (Zigbee, BLE…) |
| **UDP** | Transport | Léger, sans connexion — adapté aux objets contraints |
| **TCP** | Transport | Fiable, oriented connexion — utilisé par MQTT |
| **RPL** | Routage | Protocole de routage pour réseaux maillés contraints (LLN) |
| **Thread** | Protocole réseau | Réseau maillé basé sur IPv6, créé par Google/Nest |

### 3. Couche application (Application)

Protocoles de messagerie et d'échange de données — comment les données sont échangées entre l'objet et la plateforme.

| Protocole | Modèle | Détails |
| --- | --- | --- |
| **MQTT** | Publish/Subscribe | Léger, TCP, QoS configurable, broker central (Mosquitto, HiveMQ). Standard IoT. |
| **CoAP** | REST (UDP) | Protocole REST pour dispositifs contraints, très léger, supporte Observe (push). |
| **HTTP/HTTPS** | REST (TCP) | Standard web, plus lourd, adapté aux objets avec plus de ressources. |
| **WebSocket** | Full-duplex | Communication bidirectionnelle en temps réel, bon pour les dashboards. |
| **AMQP** | Publish/Subscribe | Messaging robuste pour l'entreprise, plus lourd que MQTT. |
| **LwM2M** | REST/Object | Protocole de gestion à distance des objets (firmware update, monitoring). |

### Résumé visuel des couches

```
┌─────────────────────────────────────────────┐
│        3. Couche APPLICATION                │
│    MQTT / CoAP / HTTP / WebSocket / AMQP    │
├─────────────────────────────────────────────┤
│        2. Couche RÉSEAU / TRANSPORT         │
│    IPv6 / 6LoWPAN / UDP / TCP / RPL         │
├─────────────────────────────────────────────┤
│        1. Couche LIAISON (Physical)         │
│    BLE / Zigbee / LoRa / Wi-Fi / NB-IoT     │
└─────────────────────────────────────────────┘
```

## Frameworks de communication pour les données

### Mosquitto - MQTT
- **Broker** MQTT — modèle **publish/subscribe** centralisé.
- Léger, idéal pour l'IoT et les objets à ressources contraintes.
- Supporte **QoS** (0, 1, 2) et **retained messages**.

### Apache Kafka
- **Plateforme de streaming de données** distribuée, modèle **publish/subscribe**.
- Basé sur un **log distribué** (topics partitionnés) — **haut débit**, temps réel.
- **Retention** : les messages sont conservés et replayables (pas éphémères).

### Orchestrateur ZooKeeper
- **Service de coordination distribué** (métadonnée, état des clusters).
- Utilisé historiquement par **Kafka** (leader d'élection, suivi des consommateurs).
- Structure en **znodes** ; remplacé progressivement par KRaft.

### (Bonus) Autres frameworks du domaine

| Framework | Type | Usage |
| --- | --- | --- |
| **EMQX** | Broker MQTT | Broker MQTT SaaS/self-hosted, extensible et scalable |
| **RabbitMQ** | Message broker (AMQP) | Messaging flexible, routage par exchange/queue |
| **HiveMQ** | Broker MQTT | Broker MQTT distribué, professional |
| **NATS** | Messaging | Léger, faible latence, cloud natif |
| **VerneMQ** | Broker MQTT | Broker MQTT distribué, en Erlang |

## Liens

- [[Accueil R505-Programmation-Avancee]]
- [[TP1 - Programmation Avancee]]