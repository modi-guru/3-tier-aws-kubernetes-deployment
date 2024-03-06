--

# Three-Tier Application Deployment on AWS using Kubernetes and Docker

## Description

This project demonstrates how to deploy a three-tier application on AWS using Kubernetes (k8s) and Docker. It covers the setup from the initial IAM configuration and EC2 setup, through the installation of necessary tools like AWS CLI, Docker, kubectl, and eksctl, to the creation of an EKS cluster and the deployment of a full-stack application with AWS Load Balancer.

## Prerequisites

- An AWS account
- A local machine with AWS CLI v2, Docker, kubectl, and eksctl installed

## Installation & Configuration

### Step 1: IAM Configuration

1. Create a user `eks-admin` with `AdministratorAccess`.
2. Generate Security Credentials: Access Key and Secret Access Key.

### Step 2: EC2 Setup

1. Launch an Ubuntu instance in your favorite region (e.g., us-west-2).
2. SSH into the instance from your local machine.

### Step 3: Install AWS CLI v2

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip
unzip awscliv2.zip
sudo ./aws/install -i /usr/local/aws-cli -b /usr/local/bin --update
aws configure
```

### Step 4: Install Docker

```bash
sudo apt-get update
sudo apt install docker.io
docker ps
sudo chown $USER /var/run/docker.sock
```

### Step 5: Install kubectl

```bash
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin
kubectl version --short --client
```

### Step 6: Install eksctl

```bash
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version
```

### Step 7: Setup EKS Cluster

```bash
eksctl create cluster --name three-tier-cluster --region us-west-2 --node-type t2.medium --nodes-min 2 --nodes-max 2
aws eks update-kubeconfig --region us-west-2 --name three-tier-cluster
kubectl get nodes
```

### Step 8: Run Manifests

```bash
kubectl create namespace workshop
kubectl apply -f .
kubectl delete -f .
```

### Step 9: Install AWS Load Balancer

```bash
# Commands for installing AWS Load Balancer
```

### Step 10: Deploy AWS Load Balancer Controller

```bash
# Commands for deploying AWS Load Balancer Controller
```

## Usage

- How to deploy your Docker containers in the Kubernetes cluster.
- How to access your application through the AWS Load Balancer.

## Contributing

Contributions are what make the open-source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

## License

Distributed under the MIT License. See `LICENSE` for more information.

## Acknowledgements

- List any references or third-party resources you might have used.

---

This template provides a comprehensive guide to setting up and deploying a three-tier application on AWS using Kubernetes and Docker. You might need to adjust the content to match your project's specifics better, such as adding more detailed usage instructions, specifying the application's architecture, or providing additional setup details.
