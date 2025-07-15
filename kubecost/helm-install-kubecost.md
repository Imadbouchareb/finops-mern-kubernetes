# 🧩 Installation de Kubecost via Helm

Ce guide décrit comment installer **Kubecost** dans un cluster Kubernetes local (Minikube) à l’aide d’Helm.

---

## 🛠️ Prérequis

- Helm installé (`helm version`)
- Minikube démarré (`minikube start`)
- `kubectl` configuré pour le cluster Minikube (`kubectl config current-context`)

---

## 📥 1. Ajouter le dépôt Helm Kubecost

```bash
helm repo add kubecost https://kubecost.github.io/cost-analyzer/
helm repo update
