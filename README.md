# Reddit Clone Deployment on Kubernetes

## Overview
This project demonstrates how to deploy a Reddit clone web application on a Kubernetes cluster using Minikube and Docker. It covers the entire process from setting up the CI and Deployment servers to deploying and accessing the application via the Internet.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Building the Docker Image](#building-the-docker-image)
- [Kubernetes Deployment](#kubernetes-deployment)
- [Accessing the Application](#accessing-the-application)
- [Ingress Setup](#ingress-setup)
- [Troubleshooting](#troubleshooting)
- [License](#license)

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
Clone the code repository on your CI-Server from [GitHub](https://github.com/BaoDevops21)

## Step 3: Install Docker on Both Servers
On both servers, run:
```bash
sudo apt-get update
sudo apt-get install docker.io -y
sudo usermod -aG docker $USER
newgrp docker

## Step 4: Install Minikube and kubectl on Deployment Server
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
sudo snap install kubectl --classic
minikube start --driver=docker


## Step 5: Building the Docker Image

Create a Dockerfile in the project directory
FROM node:19-alpine3.15
WORKDIR /reddit-clone
COPY . /reddit-clone
RUN npm install
EXPOSE 3000
CMD ["npm", "run", "dev"]

Exit and save file.

Build the docker build . -t your-dockerhub-username/reddit-clone
Push the image to Docker Hub:


## Step 6: Push the image to Docker Hub:
docker login
docker push your-dockerhub-username/reddit-clone

## Step 7 Kubernetes Deployment
