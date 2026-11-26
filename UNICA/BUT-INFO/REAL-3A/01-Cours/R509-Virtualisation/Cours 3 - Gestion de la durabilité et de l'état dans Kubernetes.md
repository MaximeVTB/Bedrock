---
type: cours
module: R509-Virtualisation
semaine: 
date: 2026-10-08
status: à-voir
tags:
  - but-info
  - real
  - cours
  - kubernetes
  - virtualisation
  - conteneurs
  - devops
---

# Cours 3 — Gestion de la durabilité et de l'état dans Kubernetes

> [!abstract] Objectif du cours
> Comprendre comment Kubernetes maintient la **stabilité**, la **santé** et la **persistance** des applications malgré la nature **éphémère** des conteneurs.

## Sommaire

- [[#1. Les conteneurs et les Pods sont éphémères]]
- [[#2. Gestion des crashs et auto-récupération]]
- [[#3. Santé du cluster et pods systèmes]]
- [[#4. Surveillance des applications — Probes]]
- [[#5. Gestion des ressources]]
- [[#6. Persistance des données — PV et PVC]]
- [[#7. StorageClass et provisionnement dynamique]]
- [[#8. Modes d'accès et types de stockage]]
- [[#9. StatefulSets et applications avec état]]
- [[#10. ConfigMaps et Secrets]]
- [[#11. Commandes importantes à retenir]]
- [[#12. Synthèse générale]]

---

# 1. Les conteneurs et les Pods sont éphémères

Dans Kubernetes, les **conteneurs sont éphémères**.

Cela signifie qu'un conteneur peut être **détruit puis recréé** à tout moment par le cluster.

Cette caractéristique permet à Kubernetes d'assurer une bonne **résilience**, mais elle pose une question importante :

> **Que deviennent les données et l'état de l'application lorsque le conteneur disparaît ?**

Kubernetes répond à cette problématique avec plusieurs mécanismes :

- la gestion du cycle de vie des Pods ;
- l'auto-récupération après un crash ;
- les **probes** pour surveiller la santé des applications ;
- les **requests** et **limits** pour gérer les ressources ;
- les **PV/PVC** pour conserver les données ;
- les **StatefulSets** pour les applications avec état ;
- les mécanismes de supervision du cluster.

---

# 2. Gestion des crashs et auto-récupération

## 2.1 Cycle de vie d'un Pod

Un **Pod** encapsule un ou plusieurs conteneurs.

Les conteneurs d'un même Pod partagent notamment le **réseau** et certains espaces de **stockage**.

Un Pod peut passer par plusieurs états :

| État | Signification |
|---|---|
| `Pending` | Le Pod a été accepté mais ses conteneurs ne sont pas encore démarrés. |
| `Running` | Les conteneurs sont lancés et fonctionnent. |
| `Succeeded` | Tous les conteneurs se sont terminés correctement. |
| `Failed` | Au moins un conteneur s'est arrêté avec une erreur. |
| `CrashLoopBackOff` | Un conteneur échoue et Kubernetes tente régulièrement de le redémarrer. |

### Commandes utiles

```bash
kubectl get pods -w
kubectl describe pod <nom>
kubectl logs <nom>
```

- `kubectl get pods -w` : surveille les changements d'état des Pods.
- `kubectl describe pod` : affiche les informations détaillées d'un Pod.
- `kubectl logs` : affiche les logs d'un conteneur.

---

## 2.2 Que se passe-t-il lors d'un crash ?

Lorsqu'un conteneur plante :

1. Le **kubelet** détecte l'échec.
2. Il consulte la politique de redémarrage.
3. Si la politique le demande, le conteneur est redémarré.
4. Kubernetes tente ainsi de rétablir le service.

Exemple :

```yaml
restartPolicy: Always
```

> [!tip] À retenir
> L'auto-récupération permet à Kubernetes de redémarrer automatiquement un conteneur défaillant.

---

## 2.3 Le rôle du kubelet et du runtime

Le **kubelet** est l'agent qui s'exécute sur chaque nœud Kubernetes.

Il est notamment chargé de faire fonctionner les conteneurs demandés par Kubernetes.

Pour créer et exécuter les conteneurs, le kubelet s'appuie sur un **runtime de conteneurs**, par exemple :

- **Containerd**
- **CRI-O**

Exemple avec Minikube :

```bash
minikube ssh
sudo ctr containers list
```

> [!info]
> Un conteneur peut parfois subsister temporairement après la suppression d'un Pod Kubernetes.

---

## 2.4 `CrashLoopBackOff`

`CrashLoopBackOff` apparaît lorsqu'un conteneur :

1. démarre ;
2. plante ;
3. est redémarré ;
4. replante ;
5. recommence plusieurs fois.

Kubernetes augmente progressivement le délai entre les tentatives de redémarrage.

Exemple d'événement :

```text
Warning  BackOff  kubelet  Back-off restarting failed container
```

### Causes possibles

- erreur dans l'application ;
- mauvaise configuration ;
- variable d'environnement manquante ;
- problème de connexion à une base de données ;
- commande de démarrage incorrecte ;
- ressources insuffisantes.

---

## 2.5 Que deviennent les données ?

Les fichiers présents directement dans le système de fichiers du conteneur sont **perdus lorsque le conteneur est supprimé**.

À l'inverse, les données placées sur un **volume persistant** peuvent être conservées.

```text
Conteneur
   │
   ├── fichiers internes → perdus lors de la suppression
   │
   └── volume persistant → données conservées
```

> [!warning] Point important
> Pour une base de données ou toute application importante, il ne faut pas compter sur le système de fichiers interne du conteneur pour conserver les données.

---

# 3. Santé du cluster et pods systèmes

## 3.1 Le namespace `kube-system`

Kubernetes possède un namespace particulier appelé :

```bash
kube-system
```

Pour voir les Pods présents dans ce namespace :

```bash
kubectl get pods -n kube-system
```

Il contient plusieurs composants essentiels au fonctionnement du cluster.

---

## 3.2 Les principaux composants

| Composant | Rôle |
|---|---|
| **CoreDNS** | Résolution interne des noms entre Pods et Services. |
| **etcd** | Base clé-valeur contenant l'état du cluster. |
| **kube-apiserver** | API du plan de contrôle ; valide et gère les objets Kubernetes. |
| **kube-scheduler** | Choisit sur quel nœud placer les Pods. |
| **controller-manager** | Exécute les boucles de réconciliation. |
| **kube-proxy** | Participe au routage du trafic entre Services et Pods. |
| **kindnet / Calico / Flannel** | Gestion du réseau entre les Pods. |
| **kubelet** | Agent exécutant les conteneurs sur les nœuds. |

> [!tip] Idée générale
> Le **plan de contrôle** décide et coordonne, tandis que les **nœuds** exécutent les workloads.

---

## 3.3 Les manifests statiques

Dans certaines installations, les composants du plan de contrôle sont définis sous forme de **manifests statiques**.

Avec Minikube :

```bash
minikube ssh
ls /etc/kubernetes/manifests
cat kube-apiserver.yaml
```

Le **kubelet** surveille ces manifests et gère localement les Pods correspondants.

> [!important]
> Les Pods statiques du plan de contrôle peuvent être gérés localement par le kubelet, indépendamment de la gestion classique par l'API server.

---

## 3.4 Monitoring avec un DaemonSet

Un **DaemonSet** permet de déployer un Pod sur les nœuds du cluster.

Il est donc adapté à des agents de monitoring ou de collecte de données.

Exemple avec **Glances** :

```yaml
apiVersion: apps/v1
kind: DaemonSet

metadata:
  name: glances

spec:
  selector:
    matchLabels:
      app: glances

  template:
    metadata:
      labels:
        app: glances

    spec:
      containers:
        - name: glances
          image: nicolargo/glances:latest
          ports:
            - containerPort: 61208

          volumeMounts:
            - mountPath: /var/run/docker.sock
              name: docker-sock

      volumes:
        - name: docker-sock
          hostPath:
            path: /var/run/docker.sock
```

Vérification :

```bash
kubectl get daemonsets
kubectl get pods -l app=glances -o wide
```

### Pourquoi un DaemonSet ?

```text
Cluster
│
├── Node 1 → Glances
├── Node 2 → Glances
└── Node 3 → Glances
```

Chaque nœud reçoit son agent.

---

# 4. Surveillance des applications — Probes

Un Pod peut être **Running** sans que l'application soit réellement fonctionnelle.

Kubernetes utilise donc des **probes**, ou sondes, pour vérifier la santé des conteneurs.

## 4.1 Les trois types de probes

| Probe | Question posée | Action principale |
|---|---|---|
| **Liveness** | « L'application est-elle encore vivante ? » | Redémarre le conteneur si le test échoue. |
| **Readiness** | « L'application peut-elle recevoir du trafic ? » | Retire temporairement le Pod du Service. |
| **Startup** | « L'application a-t-elle terminé son démarrage ? » | Permet de laisser du temps à l'application avant les autres sondes. |

### Différence essentielle

```text
Liveness
   ↓
Le conteneur est-il vivant ?
   ↓ NON
Redémarrage

Readiness
   ↓
Le conteneur est-il prêt ?
   ↓ NON
Plus de trafic envoyé au Pod

Startup
   ↓
L'application a-t-elle fini de démarrer ?
   ↓ NON
On attend avant les autres sondes
```

---

## 4.2 Endpoints de santé

Les applications utilisent souvent des endpoints dédiés :

| Endpoint | Utilisation | Rôle |
|---|---|---|
| `/healthz` | Liveness | Vérifie que l'application répond. |
| `/ready` ou `/readiness` | Readiness | Vérifie que l'application est prête. |
| `/metrics` | Monitoring | Expose des métriques pour des outils comme Prometheus ou Grafana. |

> [!note]
> Ces noms d'endpoints sont des conventions courantes. Kubernetes ne les impose pas.

---

## 4.3 Méthodes utilisées par les probes

| Méthode | Fonctionnement | Exemple |
|---|---|---|
| **HTTP GET** | Effectue une requête HTTP. | `/healthz` |
| **TCP Socket** | Vérifie qu'un port accepte une connexion. | `8080` |
| **Exec Command** | Exécute une commande dans le conteneur et vérifie son résultat. | `ps aux` |

---

## 4.4 Exemple de configuration

```yaml
livenessProbe:
  httpGet:
    path: /healthz
    port: 8080
  initialDelaySeconds: 10
  periodSeconds: 5

readinessProbe:
  tcpSocket:
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 5
```

### Paramètres importants

- `initialDelaySeconds` : temps d'attente avant le premier test.
- `periodSeconds` : fréquence des tests.
- `failureThreshold` : nombre d'échecs avant de considérer le test comme échoué.
- `successThreshold` : nombre de réussites nécessaires pour considérer le test comme réussi.

> [!warning]
> Des probes trop fréquentes ou mal configurées peuvent provoquer des redémarrages inutiles.

---

## 4.5 Exemple avec Flask

Application :

```python
from flask import Flask

app = Flask(__name__)

@app.route('/healthz')
def health():
    return 'OK', 200
```

Configuration Kubernetes :

```yaml
containers:
  - name: web
    image: myapp:latest

    ports:
      - containerPort: 5000

    livenessProbe:
      httpGet:
        path: /healthz
        port: 5000
      initialDelaySeconds: 5
      periodSeconds: 5
```

Si l'application Flask ne répond plus correctement, la liveness probe peut conduire Kubernetes à redémarrer le conteneur.

---

# 5. Gestion des ressources

Kubernetes doit partager les ressources d'un nœud entre plusieurs Pods.

Les principales ressources concernées sont :

- **CPU**
- **mémoire RAM**

Pour éviter qu'un Pod consomme toutes les ressources disponibles, on définit des **requests** et des **limits**.

---

## 5.1 Requests

Une `request` représente la quantité de ressources demandée au minimum par le conteneur.

Elle est notamment utilisée par le scheduler pour choisir un nœud adapté.

```yaml
resources:
  requests:
    cpu: "500m"
    memory: "256Mi"
```

---

## 5.2 Limits

Une `limit` définit le maximum de ressources autorisé pour le conteneur.

```yaml
resources:
  limits:
    cpu: "1"
    memory: "512Mi"
```

Exemple complet :

```yaml
resources:
  requests:
    cpu: "500m"
    memory: "256Mi"

  limits:
    cpu: "1"
    memory: "512Mi"
```

### CPU

```text
1 CPU = 1000m
500m = 0,5 CPU
```

Donc :

```text
500m = 50 % d'un cœur CPU
```

---

## 5.3 Que se passe-t-il en cas de dépassement ?

### Mémoire

Un dépassement de la limite mémoire peut provoquer l'arrêt du conteneur :

```text
OOMKilled
```

**OOM** signifie **Out Of Memory**.

### CPU

Un dépassement de la limite CPU provoque plutôt un **throttling** : le conteneur est ralenti.

Commande utile :

```bash
kubectl describe pod <nom>
```

On peut notamment rechercher les événements liés à :

- `OOMKilled`
- `Throttling CPU`

---

## 5.4 Surallocation

Kubernetes autorise une certaine **surallocation**.

Cela signifie que la somme des ressources demandées par les Pods peut être supérieure à la capacité physique immédiatement disponible.

Le scheduler doit alors organiser le placement des Pods en fonction des ressources disponibles.

---

## 5.5 Priorité des Pods

Kubernetes permet de définir des niveaux de priorité avec une **PriorityClass**.

Exemple :

```yaml
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass

metadata:
  name: high-priority

value: 1000
preemptionPolicy: PreemptLowerPriority
```

Puis dans un Pod :

```yaml
spec:
  priorityClassName: high-priority
```

Un Pod avec une priorité élevée peut préempter un Pod de priorité inférieure lorsque les ressources deviennent insuffisantes.

---

# 6. Persistance des données — PV et PVC

## 6.1 Pourquoi la persistance est nécessaire ?

Un Pod est éphémère.

Lorsqu'il est recréé, son système de fichiers interne est reconstruit à partir de l'image du conteneur.

Donc :

```text
Données dans le conteneur
        ↓
Suppression du Pod
        ↓
Données perdues
```

Pour conserver les données, Kubernetes utilise notamment :

- **PV — PersistentVolume**
- **PVC — PersistentVolumeClaim**

---

## 6.2 PV — PersistentVolume

Un **PersistentVolume** représente un espace de stockage disponible pour Kubernetes.

Exemple :

```yaml
apiVersion: v1
kind: PersistentVolume

metadata:
  name: pv-demo

spec:
  capacity:
    storage: 1Gi

  accessModes:
    - ReadWriteOnce

  hostPath:
    path: /data/demo
```

Ici, le stockage se trouve localement sur le nœud :

```text
/data/demo
```

---

## 6.3 PVC — PersistentVolumeClaim

Le **PVC** est une demande de stockage faite par une application.

```yaml
apiVersion: v1
kind: PersistentVolumeClaim

metadata:
  name: pvc-demo

spec:
  accessModes:
    - ReadWriteOnce

  resources:
    requests:
      storage: 1Gi
```

Vérification :

```bash
kubectl get pv,pvc
```

### Relation PV / PVC

```text
Application
     │
     ▼
    PVC
     │
     ▼
    PV
     │
     ▼
Stockage réel
```

Le Pod utilise généralement le **PVC**, et Kubernetes associe celui-ci à un **PV**.

---

## 6.4 Utiliser un PVC dans un Pod

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: demo-pod

spec:
  containers:
    - name: demo
      image: busybox
      command: ["sleep", "3600"]

      volumeMounts:
        - mountPath: /mnt/data
          name: demo-volume

  volumes:
    - name: demo-volume
      persistentVolumeClaim:
        claimName: pvc-demo
```

Le Pod voit le stockage dans :

```text
/mnt/data
```

Le stockage correspond ici au volume persistant demandé par :

```yaml
claimName: pvc-demo
```

---

# 7. StorageClass et provisionnement dynamique

## 7.1 Pourquoi utiliser une StorageClass ?

Créer manuellement chaque PV peut devenir difficile à gérer.

Kubernetes permet donc d'utiliser une **StorageClass** pour automatiser la création du stockage.

On parle de :

> **provisionnement dynamique**

---

## 7.2 Exemple de StorageClass

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass

metadata:
  name: standard

provisioner: k8s.io/minikube-hostpath

reclaimPolicy: Delete
volumeBindingMode: Immediate
```

La StorageClass indique notamment quel **provisioner** doit créer le stockage.

---

## 7.3 PVC dynamique

```yaml
apiVersion: v1
kind: PersistentVolumeClaim

metadata:
  name: pvc-dyn

spec:
  accessModes:
    - ReadWriteOnce

  resources:
    requests:
      storage: 2Gi

  storageClassName: standard
```

Ici, il n'est pas nécessaire de créer manuellement le PV.

```text
PVC
 ↓
StorageClass
 ↓
Provisioner
 ↓
PV créé automatiquement
```

---

## 7.4 Attention à la portabilité

Le provisionnement dynamique ne signifie pas automatiquement que le stockage est accessible depuis tous les nœuds.

### Stockage réseau

Exemples :

- NFS
- CephFS
- CSI Cloud

Le volume peut être accessible depuis plusieurs nœuds selon le backend et son mode d'accès.

### Stockage local

Un volume local reste lié à un nœud donné.

Il peut être géré avec des mécanismes comme :

- `nodeAffinity`
- `WaitForFirstConsumer`

> [!warning] À retenir
> Pour un cluster multi-nœuds, un stockage réseau partagé est généralement plus adapté lorsqu'une application doit retrouver ses données depuis différents nœuds.

---

## 7.5 Comparaison

| Aspect | PV/PVC statiques | StorageClass dynamique |
|---|---|---|
| Création du volume | Manuelle | Automatique |
| Association | Correspondance PV/PVC | Gérée par le provisioner |
| Portabilité | Limitée selon le stockage | Meilleure avec stockage réseau |
| Utilisation | Démonstration, environnement local | Cluster multi-nœuds, cloud |

---

# 8. Modes d'accès et types de stockage

## 8.1 Modes d'accès

| Mode | Signification | Exemple d'utilisation |
|---|---|---|
| `ReadWriteOnce` (**RWO**) | Lecture/écriture depuis un seul nœud | Base de données |
| `ReadOnlyMany` (**ROX**) | Lecture seule depuis plusieurs nœuds | Contenu statique |
| `ReadWriteMany` (**RWX**) | Lecture/écriture depuis plusieurs nœuds | NFS, CephFS |
| `ReadWriteOncePod` (**RWOP**) | Accès exclusif par un seul Pod | Cas sensibles |

> [!tip] Mémo
> **RWO** = un nœud en lecture/écriture  
> **ROX** = plusieurs nœuds en lecture seule  
> **RWX** = plusieurs nœuds en lecture/écriture  
> **RWOP** = un seul Pod

---

## 8.2 Sécurité et permissions

Les volumes peuvent être associés à un contexte de sécurité.

Exemple :

```yaml
securityContext:
  runAsUser: 1000
  fsGroup: 1000
```

Cela permet notamment de contrôler l'utilisateur utilisé par le processus et le groupe associé aux fichiers du volume.

---

## 8.3 Types de stockage

| Type | Description | Particularité |
|---|---|---|
| `hostPath` / `local` | Stockage local du nœud | Rapide mais non partagé |
| **NFS** | Stockage partagé sur le réseau | Compatible avec RWX |
| **CSI Driver** | Interface standard de stockage | Permet différents backends |
| **CephFS / RBD** | Stockage distribué | Haute disponibilité selon l'architecture |
| **Cloud storage** | Stockage fourni par un cloud | Provisionnement dynamique |

---

# 9. StatefulSets et applications avec état

## 9.1 Deployment ou StatefulSet ?

Les **Deployments** sont principalement adaptés aux applications **stateless**.

Exemples :

- serveur web ;
- API ;
- frontend ;
- application qui ne conserve pas son état localement.

Pour les applications ayant un état persistant, on utilise notamment les **StatefulSets**.

Exemples :

- bases de données ;
- services nécessitant une identité stable ;
- applications nécessitant des volumes persistants dédiés.

> [!important]
> Kubernetes orchestre les Pods et les volumes, mais ne gère pas à lui seul la cohérence interne d'une base de données.

La réplication, les transactions et la cohérence restent du ressort du **SGBD**.

---

## 9.2 Caractéristiques d'un StatefulSet

| Fonction | Description |
|---|---|
| **Identité stable** | Les Pods ont des noms stables et ordonnés (`app-0`, `app-1`, etc.). |
| **Volume dédié** | Chaque Pod peut avoir son propre PVC. |
| **Ordre contrôlé** | Création et suppression selon un ordre contrôlé. |
| **Stabilité** | Le nom et le volume sont conservés lors des recréations. |

---

## 9.3 Exemple : MariaDB

```yaml
apiVersion: apps/v1
kind: StatefulSet

metadata:
  name: mariadb

spec:
  serviceName: mariadb
  replicas: 1

  selector:
    matchLabels:
      app: mariadb

  template:
    metadata:
      labels:
        app: mariadb

    spec:
      containers:
        - name: mariadb
          image: mariadb:10.11

          env:
            - name: MYSQL_ROOT_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: mariadb-secret
                  key: root-password

          ports:
            - containerPort: 3306

          volumeMounts:
            - name: data
              mountPath: /var/lib/mysql

  volumeClaimTemplates:
    - metadata:
        name: data

      spec:
        accessModes:
          - ReadWriteOnce

        resources:
          requests:
            storage: 2Gi
```

---

## 9.4 `volumeClaimTemplates`

`volumeClaimTemplates` permet de créer automatiquement un PVC pour chaque Pod du StatefulSet.

Exemple :

```text
StatefulSet
│
├── mariadb-0
│      └── data-mariadb-0
│
├── mariadb-1
│      └── data-mariadb-1
│
└── mariadb-2
       └── data-mariadb-2
```

Si :

```yaml
replicas: 3
```

on obtient trois instances avec leurs propres volumes.

> [!warning]
> Plusieurs réplicas ne signifient pas automatiquement que MariaDB est répliquée ou cohérente.
>
> La réplication doit être configurée au niveau du SGBD, par exemple avec une solution adaptée comme **Galera** ou **Group Replication** selon le moteur et l'architecture.

Commandes utiles :

```bash
kubectl get statefulsets
kubectl get pods -l app=mariadb
kubectl get pvc | grep mariadb
```

Pour modifier le nombre de réplicas :

```bash
kubectl scale statefulset mariadb --replicas=3
```

---

# 10. ConfigMaps et Secrets

Kubernetes propose deux objets importants pour séparer la configuration de l'application :

- **ConfigMap**
- **Secret**

## 10.1 Secret

Un Secret peut contenir des informations sensibles, comme un mot de passe.

Exemple :

```yaml
apiVersion: v1
kind: Secret

metadata:
  name: mariadb-secret

type: Opaque

data:
  root-password: bXlzZWNyZXRwYXNzCg==
```

Dans le StatefulSet, le mot de passe peut ensuite être récupéré avec :

```yaml
env:
  - name: MYSQL_ROOT_PASSWORD
    valueFrom:
      secretKeyRef:
        name: mariadb-secret
        key: root-password
```

> [!important]
> Les Secrets servent à séparer les informations sensibles de la définition principale de l'application.

---

## 10.2 ConfigMap

Une **ConfigMap** permet de stocker des paramètres de configuration non sensibles.

Elle permet donc de séparer :

```text
Application
    │
    ├── Code
    │
    ├── ConfigMap → configuration
    │
    └── Secret → données sensibles
```

---

# 11. Commandes importantes à retenir

## Pods

```bash
kubectl get pods
kubectl get pods -w
kubectl describe pod <nom>
kubectl logs <nom>
```

## Pods du système

```bash
kubectl get pods -n kube-system
```

## DaemonSets

```bash
kubectl get daemonsets
kubectl get pods -l app=glances -o wide
```

## Stockage

```bash
kubectl get pv
kubectl get pvc
kubectl get pv,pvc
```

## StatefulSets

```bash
kubectl get statefulsets
kubectl get pods -l app=mariadb
kubectl get pvc | grep mariadb
kubectl scale statefulset mariadb --replicas=3
```

## Minikube / runtime

```bash
minikube ssh
sudo ctr containers list
```

---

# 12. Synthèse générale

## Les notions à connaître

### 1. Éphémérité

Les conteneurs peuvent être détruits et recréés.

**Donc :** les données stockées directement dans le conteneur ne doivent pas être considérées comme persistantes.

### 2. Auto-récupération

Le **kubelet** surveille les conteneurs et peut les redémarrer selon leur `restartPolicy`.

**Problème fréquent :**

```text
CrashLoopBackOff
```

### 3. Santé des applications

Les **probes** permettent de vérifier l'état réel d'une application.

```text
Liveness  → vivant ?
Readiness → prêt ?
Startup   → démarré ?
```

### 4. Ressources

Les ressources sont contrôlées avec :

```text
requests → ressources demandées / réservées
limits   → maximum autorisé
```

Un dépassement mémoire peut provoquer :

```text
OOMKilled
```

Un dépassement CPU peut provoquer du :

```text
throttling
```

### 5. Persistance

Pour conserver les données :

```text
Pod → PVC → PV → stockage
```

### 6. Provisionnement dynamique

Avec une `StorageClass` :

```text
PVC → StorageClass → Provisioner → PV
```

### 7. StatefulSet

Un **StatefulSet** est adapté aux applications ayant besoin d'une identité et/ou d'un stockage stable.

```text
StatefulSet
   │
   ├── Pod 0 → PVC 0
   ├── Pod 1 → PVC 1
   └── Pod 2 → PVC 2
```

### 8. Cohérence des données

Kubernetes orchestre l'infrastructure, mais **la cohérence interne d'une base de données reste gérée par le SGBD**.

---

# 🧠 Fiche de révision express

| Question | Réponse |
|---|---|
| Un conteneur Kubernetes est-il permanent ? | ❌ Non, il est éphémère. |
| Qui supervise les conteneurs sur un nœud ? | Le **kubelet**. |
| Quel runtime peut être utilisé ? | **Containerd** ou **CRI-O**. |
| Que signifie `CrashLoopBackOff` ? | Le conteneur plante et est redémarré avec des délais croissants. |
| Quelle probe déclenche un redémarrage ? | **Liveness**. |
| Quelle probe contrôle l'arrivée du trafic ? | **Readiness**. |
| Quelle probe protège le démarrage d'une application lente ? | **Startup**. |
| À quoi sert `request` ? | À indiquer les ressources demandées. |
| À quoi sert `limit` ? | À définir le maximum autorisé. |
| Que signifie `OOMKilled` ? | Le conteneur a été tué pour dépassement mémoire. |
| Quel objet représente un volume persistant ? | **PV**. |
| Quel objet demande du stockage ? | **PVC**. |
| Quel objet automatise le provisionnement ? | **StorageClass**. |
| Quel objet est adapté aux applications stateful ? | **StatefulSet**. |
| Un StatefulSet réplique-t-il automatiquement une BDD ? | ❌ Non. |
| À quoi sert un DaemonSet ? | Déployer un Pod sur les nœuds concernés. |
| Où se trouvent plusieurs composants système ? | Dans `kube-system`. |
| À quoi sert etcd ? | Stocker l'état du cluster sous forme clé-valeur. |
| À quoi sert CoreDNS ? | Résoudre les noms dans le cluster. |
| À quoi sert un Secret ? | Stocker des informations sensibles utilisées par les applications. |

---

# 🎯 À retenir pour l'examen

> **Kubernetes orchestre des conteneurs éphémères.**

Pour rendre une application fiable, il faut donc gérer :

```text
          KUBERNETES
              │
   ┌──────────┼──────────┐
   │          │          │
 Santé     Ressources  Persistance
   │          │          │
 Probes    Requests    PV/PVC
           Limits     StorageClass
                       │
                   StatefulSet
```

La logique générale du CM est donc :

**surveiller → récupérer → limiter → persister → orchestrer.**

---

## Liens

- [[Accueil R509-Virtualisation]]