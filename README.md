# Kubernetes Ops Box

Kubernetes Ops Box is the docker image with necessary tools for kubernetes operations including build, template, package, lint, analyze and security audit. This Kubernetes Ops Box is especially made to do operations in kubernetes that brings set of standards together on develop and managing kubernetes environment.

The repository contains three different docker images

* Base - k8s-ops
    * This image contains kubectl, kubeadm, terraform, helm and etc.
* EKS - k8s-ops:eks
    * This contains the base tools and AWS CLI to do aws cloud cli operations
* AKS - k8s-ops:aks
    * This contains the base tools and Azure CLI to do azure cloud cli operations

## How to pull image?

1. Create a github personal access token with read packages permission.
2. Login in docker using below command.
   ```
   docker login -u <github_user_name> -p <personal_access_token>
   ```
3. Pull the required images.
   ```
   docker pull docker.pkg.github.com/ksivamuthu/cei-k8s-ops/k8s-ops:latest
   ```

## How to run the image?

1. Run the image with the below command.

 ```bash
 docker run -it -v /var/run/docker.sock:/var/run/docker.sock -v /YOUR_LOCAL_FOLDER/.kube:/root/.kube docker.pkg.github.com/ksivamuthu/cei-k8s-ops/k8s-ops:latest
 ```
 
2. If you want to connect with EKS, run the image with the below command

```bash

 docker run -it -v /var/run/docker.sock:/var/run/docker.sock -v /YOUR_LOCAL_FOLDER/.kube:/root/.kube -v /YOUR_LOCAL_FOLDER/.aws:/root/.aws docker.pkg.github.com/ksivamuthu/cei-k8s-ops/k8s-ops-eks:latest
```
