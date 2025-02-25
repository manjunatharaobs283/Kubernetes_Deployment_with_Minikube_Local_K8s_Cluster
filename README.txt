Kubernetes Deployment with Minikube (Local K8s Cluster)
🎯 Objective:
Deploy a containerized application to Minikube (local Kubernetes).
Automate deployments using GitHub Actions.
🛠️ Tools Used:
Minikube
Docker
Kubectl

🔹 Step 1: Install Minikube
📌 Install on macOS/Linux
brew install minikube
minikube start

📌 Install on Ubuntu
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube start


🔹 Step 2: Write a Kubernetes Deployment File
📌 Create deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: node-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: node-app
  template:
    metadata:
      labels:
        app: node-app
    spec:
      containers:
        - name: node-app
          image: my-node-app
          ports:
            - containerPort: 3000

📌 Deploy to Minikube
kubectl apply -f deployment.yaml
kubectl get pods

✅ App is running on Kubernetes locally! 🎉

🔹 Step 3: Automate Kubernetes Deployment with GitHub Actions
📌 Create mkdir -p .github/workflows 
Vim .github/workflows/k8s-deploy.yml
name: Kubernetes Deployment
on: [push]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set Up Minikube
        run: minikube start

      - name: Deploy to Kubernetes
        run: kubectl apply -f deployment.yaml

📌 Push the Code to GitHub
git add .
git commit -m "Added Minikube Deployment"
git push origin main

✅ GitHub Actions now deploys the app to local Kubernetes! 🎉

🚀 Final Summary
📌 These DevOps projects run completely locally without any cloud provider!
🔹 Project 1: CI/CD with GitHub Actions & Docker → (Deploy Locally)
🔹 Project 2: Infrastructure as Code (Terraform & VirtualBox) → (Local VMs)
🔹 Project 3: Kubernetes Deployment → (Minikube)
