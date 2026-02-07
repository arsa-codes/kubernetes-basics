# 🎯 Orchestration avec Kubernetes

## Description
Ce projet démontre les bases de l'orchestration de conteneurs dans un cluster Kubernetes (compatible Minikube / Kind).

## Contenu du dépôt
- `namespace.yaml` : Création d'un espace isolé `rncp-k8s`.
- `deployment.yaml` : Déploiement de l'application Nginx.
- `service.yaml` : Exposition interne des Pods.
- `ingress.yaml` : Règle de routage pour l'accès externe.
- `config.yaml` : Gestion des variables (ConfigMap) et mots de passe (Secret).

## Concepts Clés (Bloc RNCP)

### 📦 Pods
L'unité de base de Kubernetes. Dans ce projet, le Pod contient le conteneur Nginx. Les Pods sont éphémères (si un meurt, il est remplacé).

### 🌐 Services
Abstraction qui définit un ensemble logique de Pods et une politique pour y accéder.
- Le `service.yaml` assure que même si les IP des Pods changent, l'application reste accessible via une IP fixe interne (ClusterIP).

### 🔑 ConfigMap / Secret
Séparation de la configuration et du code :
- **ConfigMap** : Pour les données non sensibles (ex: `APP_ENV=production`).
- **Secret** : Pour les données sensibles (ex: mots de passe DB), stockées en base64.

### 📈 Scalabilité
Définie dans `deployment.yaml` via la ligne `replicas: 3`.
Kubernetes maintient en permanence 3 instances de l'application actives pour gérer la charge et assurer la haute disponibilité.

## Déploiement (Local)
```bash
kubectl apply -f namespace.yaml
kubectl apply -f config.yaml
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f ingress.yaml
```
