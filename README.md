# Projet Kubernetes & Docker : Movie App

Ce projet est une application de gestion de films micro-services, conteneurisée avec Docker et orchestrée via Kubernetes (AKS).


## 📋 Description

L'objectif principal est la démonstration de la conteneurisation et de l'orchestration de conteneurs. L'application se compose de trois services interconnectés :
- **Frontend** : Interface utilisateur (Node.js/Express)
- **Backend** : API de gestion des films (Node.js/Express)
- **Base de données** : MySQL pour le stockage des données

## 🏗 Architecture

Le projet est structuré comme suit :
- `Movie_app/` : Code source de l'application
  - `frontend/` : Service web
  - `backend/` : Service API
- `Deploiements/` : Manifests Kubernetes (.yaml) pour le déploiement sur AKS

## 🚀 Déploiement

### Prérequis
- Docker
- Cluster Kubernetes (AKS recommandé)
- `kubectl` configuré

### Installation via Kubernetes (AKS)

1. **Appliquer les configurations** (Secrets & ConfigMaps) :
   ```bash
   kubectl apply -f Deploiements/backend-deployment.yaml
   # Assurez-vous que les ConfigMap et Secret sont inclus ou appliquez-les séparément si divisés
   ```

2. **Déployer la base de données** :
   ```bash
   kubectl apply -f Deploiements/mysql-deployment.yaml
   kubectl apply -f Deploiements/mysql-service.yaml
   ```

3. **Déployer le Backend** :
   ```bash
   kubectl apply -f Deploiements/backend-deployment.yaml
   kubectl apply -f Deploiements/backend-service.yaml
   ```

4. **Déployer le Frontend** :
   ```bash
   kubectl apply -f Deploiements/frontend-deployment.yaml
   kubectl apply -f Deploiements/frontend-service.yaml
   ```

### 🌍 Accès à l'application

Une fois déployé sur AKS, le service frontend est exposé via un LoadBalancer.
Récupérez l'adresse IP publique pour accéder à l'application :

```bash
kubectl get service frontend-service
```
L'application sera accessible à l'adresse IP externe listée (EXTERNAL-IP) sur le port 80.

## 🛠 Développement Local (Docker Compose)

Pour tester localement sans Kubernetes :

```bash
cd Movie_app
docker-compose up --build
```
L'application sera accessible sur `http://localhost:80`.
