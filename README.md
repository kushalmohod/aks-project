# aks-project

📁 Project Structure
aks-demo-project/
│
├── app/
│   ├── index.html
│   └── Dockerfile
│
├── k8s/
│   ├── deployment.yaml
│   └── service.yaml
│
├── .gitignore
├── README.md
📄 1. app/index.html
<!DOCTYPE html>
<html>
<head>
  <title>AKS Demo</title>
</head>
<body>
  <h1>Hello from AKS 🚀</h1>
  <p>Served from: <span id="host"></span></p>

  <script>
    document.getElementById("host").innerText = window.location.hostname;
  </script>
</body>
</html>
📄 2. app/Dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
📄 3. k8s/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: aks-demo
spec:
  replicas: 2
  selector:
    matchLabels:
      app: aks-demo
  template:
    metadata:
      labels:
        app: aks-demo
    spec:
      containers:
      - name: aks-demo
        image: <your-dockerhub-username>/aks-demo-app
        ports:
        - containerPort: 80
📄 4. k8s/service.yaml
apiVersion: v1
kind: Service
metadata:
  name: aks-demo-service
spec:
  type: LoadBalancer
  selector:
    app: aks-demo
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
📄 5. .gitignore
node_modules
.env
.DS_Store
📄 6. README.md
# AKS Demo Project 🚀

This project demonstrates deploying a simple web application on Azure Kubernetes Service (AKS) with automatic load balancing.

## 📦 Tech Stack
- Docker
- Kubernetes
- Azure Kubernetes Service (AKS)

## 🚀 Steps to Run

### 1. Build & Push Docker Image
```bash
docker build -t aks-demo-app ./app
docker tag aks-demo-app <your-dockerhub-username>/aks-demo-app
docker push <your-dockerhub-username>/aks-demo-app
2. Deploy to AKS
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
3. Get External IP
kubectl get service
📈 Features
Load balancing using Kubernetes Service (LoadBalancer)
Scalable pods
Simple Nginx-based app
🧠 Learning Outcome
Understanding AKS deployment
Kubernetes services & scaling
Azure Load Balancer integration
📄 Author

Your Name
Kushal

---

# 🚀 Kaise Upload kare GitHub pe?

```bash
git init
git add .
git commit -m "Initial AKS project"
git branch -M main
git remote add origin <your-repo-url>
git push -u origin main
