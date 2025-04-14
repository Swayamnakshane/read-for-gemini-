Here's an enhanced and more detailed setup guide for your hackathon project, based on the EasyShop README:

---

# 🚀 Advanced Gemini Clone - AI Platform with Continuous Deployment

[![Next.js](https://img.shields.io/badge/Next.js-14.1.0-black?style=flat-square&logo=next.js)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0.0-blue?style=flat-square&logo=typescript)](https://www.typescriptlang.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-8.1.1-green?style=flat-square&logo=mongodb)](https://www.mongodb.com/)
[![ArgoCD](https://img.shields.io/badge/ArgoCD-v2.6-blue?style=flat-square&logo=argo-cd)](https://argo-cd.readthedocs.io/)
[![AWS](https://img.shields.io/badge/AWS-EC2-orange?style=flat-square&logo=aws)](https://aws.amazon.com/)

Advanced Gemini Clone is a sophisticated AI platform built with Next.js 14, TypeScript, and MongoDB. It includes cutting-edge features for faster response times and enhanced functionalities, deployed with Jenkins, Terraform, AWS, and ArgoCD for smooth CI/CD workflows.

## ✨ Features

- 🔥 Advanced AI Algorithms and Models
- 🛠️ Fast Response Times with Optimized Data Pipelines
- 🌐 Real-time Data Sync across Platforms
- 🎨 Modern UI using Tailwind CSS
- 🔒 Secure Authentication with JWT
- 📈 Data Analytics & Reports Dashboard
- 🚀 Continuous Deployment via ArgoCD

## 🏗️ Architecture

### 1. **Presentation Tier (Frontend)**
- Next.js React Components
- Redux for State Management
- Tailwind CSS for Styling
- Client-Side Routing
- Real-Time UI Features

### 2. **Application Tier (Backend)**
- Next.js API Routes for Server-Side Logic
- AI Model Integration
- Authentication & Authorization via JWT
- Real-Time Data Processing with WebSockets

### 3. **Data Tier (Database)**
- MongoDB Database
- Mongoose ODM for Schema & Validation
- Data Ingestion Pipelines
- AI Model Training Data Storage

## PreRequisites

> Before setting up this project, ensure you have the following tools installed:

- [Terraform](https://www.terraform.io/)
- [AWS CLI](https://aws.amazon.com/cli/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [eksctl](https://eksctl.io/)
- [ArgoCD CLI](https://argo-cd.readthedocs.io/en/stable/cli_installation/)

## Setup & Initialization

### 1. **Install Terraform**
**Linux & macOS**
```bash
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update && sudo apt-get install terraform
```
### Verify Installation
```bash
terraform -v
```

### 2. **Install AWS CLI**
Install the AWS Command Line Interface to interact with AWS services:
```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip
unzip awscliv2.zip
sudo ./aws/install
```

```bash
aws configure
```

### 3. **Install eksctl CLI**
`eksctl` is a simple CLI tool for creating clusters on EKS:
```bash
curl --silent --location "https://github.com/weaveworks/eksctl/releases/download/v0.116.0/eksctl_Linux_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
```

### 4. **Install ArgoCD CLI**
```bash
curl -sSL https://github.com/argoproj/argo-cd/releases/download/v2.6.0/argocd-linux-amd64 -o /usr/local/bin/argocd
chmod +x /usr/local/bin/argocd
```

---

## Getting Started

1. **Clone the Repository:**
```bash
git clone https://github.com/<your-github>/advanced-gemini-clone.git
cd advanced-gemini-clone
```

2. **Generate SSH Key Pair for EC2 Access:**
```bash
ssh-keygen -f gemini-key
chmod 400 gemini-key
```

3. **Initialize Terraform:**
```bash
terraform init
```

4. **Review Execution Plan:**
```bash
terraform plan
```

5. **Apply Configuration to Deploy Resources:**
```bash
terraform apply
```
> Confirm with `yes` when prompted.

---

### **AWS EKS Setup**

1. **Configure AWS CLI:**
Ensure AWS CLI is properly configured to interact with your AWS account:
```bash
aws configure
```

2. **Create an EKS Cluster:**
```bash
eksctl create cluster --name gemini-cluster --region us-west-2 --nodes 3 --node-type t3.medium --ssh-access --ssh-public-key gemini-key --managed
```

3. **Update kubeconfig for EKS:**
```bash
aws eks --region us-west-2 update-kubeconfig --name gemini-cluster
```

4. **Check Cluster Nodes:**
```bash
kubectl get nodes
```

---

## Jenkins Setup

1. **Install Jenkins:**
```bash
sudo apt update
sudo apt install openjdk-11-jdk
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
echo "deb http://pkg.jenkins.io/debian/ jenkins.io/" | sudo tee -a /etc/apt/sources.list.d/jenkins.list
sudo apt update
sudo apt install jenkins
```

2. **Start Jenkins Service:**
```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

3. **Access Jenkins:**
Navigate to `http://<your-public-ip>:8080` to open Jenkins.

4. **Install Required Plugins:**
- Go to `Manage Jenkins → Manage Plugins → Available` and install:
  - Docker Pipeline
  - Pipeline: AWS
  - GitHub Integration

5. **Create Jenkins Pipeline for CI/CD:**
- Create a new pipeline job and configure the GitHub repository.
- Add your credentials for GitHub and DockerHub under `Manage Jenkins → Manage Credentials`.

---

## ArgoCD Setup

1. **Install ArgoCD in EKS:**
```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

2. **Access ArgoCD:**
Forward the port to access the ArgoCD UI:
```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443 --address=0.0.0.0 &
```
Navigate to `https://<bastion-ip>:8080` in your browser.

3. **Login to ArgoCD:**
Get the admin password:
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

4. **Create ArgoCD Application:**
- In the ArgoCD UI, create a new app by linking your Git repository that contains the Kubernetes manifests.

---

### **Continuous Deployment via Jenkins & ArgoCD**

1. **GitHub Webhook Configuration:**
Set up GitHub webhook to trigger Jenkins builds upon commits.

2. **Configure Jenkins Pipeline:**
- Make sure your Jenkins pipeline is correctly set to build and push images to Docker Hub.
- Trigger ArgoCD sync to automatically deploy updates.

---

## Final Deployment

Once the pipeline is set up and the repository is linked to ArgoCD, you will have automatic deployment to your EKS cluster each time you push changes.

---

## HTTPS & SSL Setup

1. **Set up Nginx Ingress Controller:**
```bash
kubectl create namespace ingress-nginx
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install nginx-ingress ingress-nginx/ingress-nginx --namespace ingress-nginx
```

2. **Install Cert-Manager:**
```bash
helm install cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version v1.12.0 --set installCRDs=true
```

3. **Create DNS Record:**
Point your domain to the LoadBalancer IP.

---

### **Congratulations!**

Your AI platform is now live with automated CI/CD. Enjoy building with the advanced Gemini Clone!

---

This enhanced README should give you the detailed steps you need for your hackathon project, combining the setup of Jenkins, AWS CLI, EKS, and ArgoCD. Let me know if you'd like any more adjustments!
