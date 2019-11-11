# Kubernetes Ops Box

Kubernetes Ops Box is the docker image with necessary tools for kubernetes operations including build, template, package, lint, analyze and security audit. This Kubernetes Ops Box (#k8s-ops-box) is especially made to do operations in kubernetes that brings set of standards together on develop and managing kubernetes environment.

The repository contains three different docker images

* Base - k8s-ops
    * This image contains kubectl, kubeadm, terraform, helm and etc.
* EKS - k8s-ops:eks
    * This contains the base tools and AWS CLI to do aws cloud cli operations
* AKS - k8s-ops:aks
    * This contains the base tools and Azure CLI to do azure cloud cli operations
