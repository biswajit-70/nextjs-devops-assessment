# Next.js DevOps Assessment

Containerized Next.js application deployed using Docker, GitHub Actions, and Kubernetes (Minikube).

## 📋 Project Structure
```
nextjs-devops-assessment/
├── .github/workflows/docker-build-push.yml
├── k8s/
│ ├── deployment.yaml
│ └── service.yaml
├── app/
├── public/
├── Dockerfile
├── .dockerignore
└── README.md
```

## 🚀 Setup Instructions

### Prerequisites
- **Node.js 18+**
- **Docker**
- **Minikube** (for local Kubernetes)
- **kubectl**

### 1. Clone Repository
```bash
git clone https://github.com/biswajit-70/nextjs-devops-assessment.git
cd nextjs-devops-assessment
```
### 2. Local Development
```bash
# Install dependencies
npm install
```
### Run development server
```
npm run dev
```
Access: http://localhost:3000

### 3. Docker Build & Run
bash
Build image
```
docker build -t nextjs-app .
```
### Run container
```
docker run -d -p 3000:3000 nextjs-app
```
Access: http://localhost:3000

## ⚙️ Deployment Steps for Minikube
### 1. Start Minikube Cluster
```bash
minikube start --driver=docker
minikube status
kubectl get nodes
```
### 2. Deploy Application
### Apply Kubernetes manifests
```
kubectl apply -f k8s/
```
### Verify deployment
```
kubectl get deployments, pods, services
```
### 3. Check Status
```
kubectl get pods -w
```
### View logs
```
kubectl logs -l app=nextjs-app
```
### Detailed info
```
kubectl describe deployment nextjs-app
```
## 🌐 How to Access Deployed Application

- Method 1: Minikube Service (Recommended)
```bash
minikube service nextjs-service --url
# Output: http://192.168.49.2:32415
```
- Method 2: Port Forwarding
```bash
kubectl port-forward service/nextjs-service 8080:80
```
Access: http://localhost:8080

- Method 3: Direct Access
```bash
kubectl get service nextjs-service
# Use NodePort with Minikube IP
```
## 🔄 CI/CD Pipeline
Automated on push to main branch:

- ✅ Builds Docker image

- ✅ Pushes to GitHub Container Registry

- ✅ Tags: latest + commit SHA

Image Location: ghcr.io/biswajit-70/nextjs-app:latest

### 🛠️ Useful Commands
Kubernetes Management
```bash
# Scale application
kubectl scale deployment nextjs-app --replicas=3
```
-  View all resources
```
kubectl get all
```

```bash
# Check pod issues
kubectl describe pod <pod-name>
```
-  View service details
```
kubectl describe service nextjs-service
```
- Restart Minikube
```
minikube stop && minikube start
```
## ✅ Verification Steps
Local: ```npm run dev``` → http://localhost:3000

Docker: ```docker run -d -p 3000:3000 nextjs-app``` → http://localhost:3000

Kubernetes: ```minikube service nextjs-service --url``` → Access via provided URL

## 🧹 Cleanup
-  Delete resources
```
kubectl delete -f k8s/
```
- Stop Minikube
```
minikube stop
```
-  Delete cluster
```
minikube delete
```

- Repository: https://github.com/biswajit-70/nextjs-devops-assessment
- Container Image: ghcr.io/biswajit-70/nextjs-app:latest
