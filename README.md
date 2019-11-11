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

## Tools

### Docker CLI, Kubectl, KubeAdm

This *k8s-ops-box* includes docker cli, kubectl and kubeadm installed. It still uses host docker to build the images. You've to mount docker.sock when you are running this box to give access to docker-cli to build the images.

### Dev tools

This *k8s-ops-box* comes with necessary dev tools or command line tools that requires kubernetes operations. It has vim editor, jq for JSON parsing, curl for requests, git for version control, unzip/tar for unzipping files and python3/pip installed for basic operations.

### Kube Shell

An integrated shell for working with the Kubernetes CLI is installed in this *k8s-ops-box* and that's the main entrypoint of the docker image. This kube-shell includes auto completion, fish style command support and other cool features. This is one of the must have tool when you are using lot of kubectl commands to query your cluster.

![](https://camo.githubusercontent.com/6dd81f81976c3abf550dddbed8dcc1fa93d86595/687474703a2f2f692e696d6775722e636f6d2f6466656c6b4b722e676966)

### Hadolint

Do you want to lint your dockerfile? Hadolint is the superpower lint tool that lints the docker file and suggests the best practices to follow and to avoid security issues.

```
hadolint <Dockerfile>
```
