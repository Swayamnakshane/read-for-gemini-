# read-for-gemini-

Here's an updated `README.md` for your "Advanced Gemini Clone" project, incorporating the same structure and setup as the "EasyShop" README you provided:

```markdown
# 💬 Advanced Gemini Clone

![Gemini Clone Logo](public/assets/readme-banner.png)

An advanced GEMINI Clone built with Next.js, featuring enhanced functionalities and faster response times.

[![Next.js](https://img.shields.io/badge/Next.js-14.1.0-black?style=flat-square&logo=next.js)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0.0-blue?style=flat-square&logo=typescript)](https://www.typescriptlang.org/)
[![NextAuth](https://img.shields.io/badge/NextAuth-5.0.0-yellow?style=flat-square&logo=nextauth)](https://next-auth.js.org/)
[![Zustand](https://img.shields.io/badge/Zustand-4.0.0-green?style=flat-square&logo=redux)](https://github.com/pmndrs/zustand)
[![Framer Motion](https://img.shields.io/badge/Framer%20Motion-5.0.0-purple?style=flat-square&logo=framer)](https://www.framer.com/motion/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [License](#license)

## Overview

This project is an advanced recreation of the GEMINI AI platform, leveraging Next.js as a full-stack React framework. It incorporates all core functionalities of the actual GEMINI while providing natural, optimized responses that outperform the original in terms of speed.

## Features

![Gemini Features](public/assets/gemini-features.png)

### Authentication and State Management
- 🔐 Robust authentication using Next Auth v5
- 🔄 Efficient state management with Zustand

### User Interface and Experience
- ✨ Micro-animations powered by Framer Motion
- 🎨 Custom in-house components for UI flexibility
- 🌓 Dark and light mode toggle
- 📱 Fully responsive design for both desktop and mobile

### Chat Functionality
- 💬 Advanced chat features including rename, delete, and pin
- 🗣️ Text-to-speech and speech-to-text capabilities
- 🔗 Share chats and copy to clipboard
- ⏹️ Abort functionality for stopping responses
- 🖼️ Chat with images, including mobile support
- 🔄 Response modification and regeneration

### Advanced Features
- 🎭 Prompt Gallery for model-specific outputs
- ✏️ Edit Prompt functionality
- 🌈 Syntax highlighting for code outputs
- 💡 Random prompt suggestions on homepage

## Technology Stack

- **Frontend Framework**: Next.js (React)
- **Authentication**: Next Auth v5
- **State Management**: Zustand
- **Animations**: Framer Motion
- **UI Components**: Custom dev-components
- **Theming**: Next Themes

## PreRequisites

> [!IMPORTANT]  
> Before you begin setting up this project, make sure the following tools are installed and configured properly on your system:

### 1. Install Terraform
* Install Terraform  
#### Linux & macOS
```bash
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update && sudo apt-get install terraform
```
### Verify Installation
```bash
terraform -v
```

### 2. Install AWS CLI
AWS CLI (Command Line Interface) allows you to interact with AWS services directly from the command line.

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip
unzip awscliv2.zip
sudo ./aws/install
```

```bash
aws configure
```

> #### This will prompt you to enter:<br/>
- **AWS Access Key ID:**<br/>
- **AWS Secret Access Key:**<br/>
- **Default region name:**<br/>
- **Default output format:**<br/>

> [!NOTE]  
> Make sure the IAM user you're using has the necessary permissions. You’ll need an AWS IAM Role with programmatic access enabled, along with the Access Key and Secret Key.

## Getting Started

Follow these steps to get your infrastructure up and running using Terraform:

### 1. Clone the Repository:
First, clone this repo to your local machine:
```bash
git clone https://github.com/yourusername/dev-gemini-clone.git
cd terraform
```

### 2. Generate SSH Key Pair:
Create a new SSH key to access your EC2 instance:
```bash
ssh-keygen -f terra-key
```
This will prompt you to create a new key file named terra-key.

### 3. Private Key Permission:
Change your private key permission:
```bash
chmod 400 terra-key
```

### 4. Initialize Terraform:
Initialize the Terraform working directory to download required providers:
```bash
terraform init
```

### 5. Review the Execution Plan:
Before applying changes, always check the execution plan:
```bash
terraform plan
```

### 6. Apply the Configuration:
Now, apply the changes and create the infrastructure:
```bash
terraform apply
```
> Confirm with `yes` when prompted.

### 7. Access Your EC2 Instance:
After deployment, grab the public IP of your EC2 instance from the output or AWS Console, then connect using SSH:
```bash
ssh -i terra-key ubuntu@<public-ip>
```

### 8. Update your kubeconfig:
To interact with your EKS cluster, execute the following command:
```bash
aws eks --region eu-west-1 update-kubeconfig --name gemini-cluster
```

### 9. Check your cluster:
```bash
kubectl get nodes
```

## Jenkins Setup Steps

### 1. Open Jenkins in Browser:
> Use your public IP with port 8080:
> **http://<public_IP>:8080**

### 2. Install Essential Plugins:
- **Docker Pipeline**
- **Pipeline View**

### 3. Set Up Docker & GitHub Credentials in Jenkins (Global Credentials):
- GitHub Credentials:
  - Go to: **Jenkins → Manage Jenkins → Credentials → (Global) → Add Credentials**
  - Use:
    - **Kind**: `Username with password`
    - **ID**: `github-credentials`

## Argo CD Setup

### 1. Install Argo CD:
```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### 2. Access Argo CD GUI:
```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443 --address=0.0.0.0 &
```

## Deploy Your Application in Argo CD GUI:
Follow the steps to create and sync the app through the Argo CD interface.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```

This README follows the same structure as the "EasyShop" README, detailing setup, deployment, and technology used for the "Advanced Gemini Clone" project, while maintaining a similar layout and readability. Let me know if you'd like to make any changes or additions!
