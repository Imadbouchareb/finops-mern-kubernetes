# 💡 FinOps Kubernetes - Dockerisation, Déploiement et Optimisation

## 👥 Membres du groupe
- Imad Bouchareb
- Asma Lounissi
- Walid Hallouche

## 🎯 Objectif du projet

Ce projet vise à :

- Dockeriser une application MERN (MongoDB, Express, React, Node).
- Déployer cette application dans un cluster Kubernetes local (Minikube).
- Intégrer des outils FinOps comme **Kubecost**, **Prometheus** et **Grafana** pour analyser et optimiser les coûts.
- Produire un rapport FinOps avec des recommandations d’optimisation.

---

## 🔗 Application utilisée

- **Repo GitHub** : [https://github.com/balajihambeere/mern-stack-real-world-example-app](https://github.com/balajihambeere/mern-stack-real-world-example-app)
- **Structure de l’app** :
  - `client/` : Frontend React
  - `api/` : Backend Express + Node
  - Base de données : MongoDB

---

## 🐳 Dockerisation

### 📂 Dockerfile créés
- `api/Dockerfile`
- `client/Dockerfile`
- MongoDB : image officielle utilisée via Docker Compose

### 🔧 docker-compose.yml
Un fichier `docker-compose.yml` a été créé pour tester l’ensemble localement avant Kubernetes.

---

## ☸️ Déploiement Kubernetes

### 📂 Fichiers YAML (dans le dossier `k8s/`)
- Deployments
- Services
- PersistentVolumeClaims pour Mongo
- ConfigMap & Secret
- Ingress

### ✅ Commandes utilisées
```bash
kubectl apply -f k8s/
kubectl get pods,services
minikube service <service-name>

📦 Intégration de Kubecost
Installation via Helm :
bash
Copier
Modifier
helm repo add kubecost https://kubecost.github.io/cost-analyzer/
helm install kubecost kubecost/cost-analyzer --namespace kubecost --create-namespace
kubectl port-forward -n kubecost deployment/kubecost-cost-analyzer 9090
📸 Voir les captures dans captures/overview-kubecost*.png

📈 Intégration Prometheus + Grafana
Installation via Helm :
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install prometheus prometheus-community/kube-prometheus-stack --namespace monitoring --create-namespace

🔒 Récupération mot de passe Grafana :
kubectl --namespace monitoring get secrets prometheus-grafana -o jsonpath="{.data.admin-password}" | base64 -d ; echo

🎯 Dashboards ajoutés dans Grafana :

- Utilisation CPU / RAM par pod
- Requests vs Limits
- Vue namespace + composants actifs

📊 Analyse FinOps via Kubecost
🔍 Données relevées :
Indicateur	      Résultat initial	   Résultat final
Kubernetes Costs	0,03 $US	           4,79 $US
Total Costs	      0,03 $US	           4,79 $US
Possible Savings	1,81 $US/mo	         1,96 $US/mo
Cluster Efficiency	0 %	               0 %

💡 Recommandations FinOps :
🔧 Réduction des requests CPU/RAM

🧹 Nettoyage des workloads inactifs

💾 Optimisation des disques et PV inutilisés

🔄 Passage à ClusterIP pour services internes

🐳 Utilisation d’images plus légères (ex : node:alpine)

📂 Arborescence du projet
mern-blog/
├── api/                       # Backend Node
├── client/                    # Frontend React
├── docker-compose.yml
├── README.md
├── k8s/                       # Fichiers YAML Kubernetes
├── kubecost/
│   └── helm-install-kubecost.md
├── monitoring/
│   └── helm-install-prometheus-grafana.md
├── captures/
│   ├── overview-kubecost.png
│   ├── overview-kubecost1.png
│   └── ...
├── rapport-finops.md
