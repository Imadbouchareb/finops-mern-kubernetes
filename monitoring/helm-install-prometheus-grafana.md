# Installation de Prometheus & Grafana via Helm

## 🎯 Objectif
Déployer l’outil de monitoring complet `kube-prometheus-stack`, qui inclut :
- Prometheus (collecte de métriques)
- Grafana (visualisation)
- Alertmanager (alertes)

## 📦 Étapes d'installation

### 1. Ajouter le dépôt Helm

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
