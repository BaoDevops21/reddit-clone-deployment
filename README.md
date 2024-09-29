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

### Step 3: Install Docker on Both Servers
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
