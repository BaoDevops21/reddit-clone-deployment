# Reddit Clone Deployment on Kubernetes

## Overview
This project demonstrates how to deploy a Reddit clone web application on a Kubernetes cluster using Minikube and Docker. It covers the entire process from setting up the CI and Deployment servers to deploying and accessing the application via the Internet.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation](#installation)
  - [Step 1: Provision EC2 Instances](#step-1-provision-ec2-instances)
  - [Step 2: Clone the Code on CI-Server](#step-2-clone-the-code-on-ci-server)
  - [Step 3: Install Docker on Both Servers](#step-3-install-docker-on-both-servers)
  - [Step 4: Install Minikube and kubectl on Deployment Server](#step-4-install-minikube-and-kubectl-on-deployment-server)
  - [Building the Docker Image](#building-the-docker-image)
  - [Step 5: Kubernetes Deployment](#step-5-kubernetes-deployment)
  - [Step 6: Accessing the Application](#step-6-accessing-the-application)
- [Troubleshooting](#troubleshooting)

## Prerequisites
- **AWS Account**: For provisioning EC2 instances.
- **Docker**: Installed on both CI and Deployment servers.
- **Minikube**: Installed on the Deployment server.
- **kubectl**: Installed on the Deployment server.

## Installation

### Step 1: Provision EC2 Instances
1. Create two instances:
   - **CI-Server**: Ubuntu, t2.micro
   - **Deployment Server**: Ubuntu, t2.medium

### Step 2: Clone the Code on CI-Server
```bash
# Clone the code repository on your CI-Server from GitHub
git clone https://github.com/BaoDevops21/reddit-clone
Step 3: Install Docker on Both Servers
bash
Copy code
# On both servers, run:
sudo apt-get update
sudo apt-get install docker.io -y
sudo usermod -aG docker $USER
newgrp docker
Step 4: Install Minikube and kubectl on Deployment Server
bash
Copy code
# Run the following commands:
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
sudo snap install kubectl --classic
minikube start --driver=docker
Building the Docker Image
Create a Dockerfile in the project directory:
Dockerfile
Copy code
FROM node:19-alpine3.15
WORKDIR /reddit-clone
COPY . /reddit-clone
RUN npm install
EXPOSE 3000
CMD ["npm", "run", "dev"]
Build the image:
bash
Copy code
docker build . -t your-dockerhub-username/reddit-clone
Push the image to Docker Hub:
bash
Copy code
docker login
docker push your-dockerhub-username/reddit-clone
Step 5: Kubernetes Deployment
Create a K8s directory:
bash
Copy code
mkdir K8s
cd K8s
Create a Deployment.yml file:
yaml
Copy code
apiVersion: apps/v1
kind: Deployment
metadata:
  name: reddit-clone-deployment
  labels:
    app: reddit-clone
spec:
  replicas: 2
  selector:
    matchLabels:
      app: reddit-clone
  template:
    metadata:
      labels:
        app: reddit-clone
    spec:
      containers:
      - name: reddit-clone
        image: your-dockerhub-username/reddit-clone
        ports:
        - containerPort: 3000
Apply the deployment:
bash
Copy code
kubectl apply -f Deployment.yml
Verify the deployment:
bash
Copy code
kubectl get deployments
Step 6: Accessing the Application
Create a Service.yml file:
yaml
Copy code
apiVersion: v1
kind: Service
metadata:
  name: reddit-clone-service
  labels:
    app: reddit-clone
spec:
  type: NodePort
  ports:
  - port: 3000
    targetPort: 3000
    nodePort: 31000
  selector:
    app: reddit-clone
Apply the service:
bash
Copy code
kubectl apply -f Service.yml
Get the service details:
bash
Copy code
kubectl get services
Access the application:
bash
Copy code
minikube service reddit-clone-service --url
Troubleshooting
No space left on device: Clean up Docker images, containers, and volumes.
Unable to access the application: Ensure that the appropriate ports are open in the AWS security group.
