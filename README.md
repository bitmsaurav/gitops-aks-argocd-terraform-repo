# Deploying ArgoCD on Azure Kubernetes Service (AKS) using Terraform By Saurav kunal DevopesExpert

## Introduction
This guide provides step-by-step instructions to deploy ArgoCD on AKS using Terraform, facilitating a GitOps workflow on Azure.

## Prerequisites
- **Kubectl**: Installed. Download here: [kubectl for Windows](https://dl.k8s.io/release/v1.28.9/bin/windows/amd64/kubectl.exe)
- **Azure CLI**: Installed and authenticated with `az login`.
- **AKS Credentials (AKS is up and running)**: Obtain with `az aks get-credentials --resource-group myAksResourceGroup --name myAksCluster`.
- **Visual Studio Code Base64 Decode and Encode Extension**: Installed for handling base64 decodings. Will be used to decode the initial ArgoCD admin password.

## Terraform Workflow
```bash
# Step 1: Initialize your Terraform workspace
terraform init

# Step 2: Generate and show an execution plan
terraform plan

# Step 3: Apply the changes required to reach the desired state of the configuration
terraform apply
#After that run the commnd
kubectl get svc -n argocd(for checking the service is running or not)
# Step 4: Retrieve the ArgoCD default admin(username) password and decode it using Base64 extension
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}"
#After this above coomand open one text file in vscode past that and right click base 64->base64decode once decode is happen that is ur Argocd password. for me tvADtDex2HRupoMp password for argo cd.admin is user
# Step 5: Destroy all resources created by the Terraform configuration
terraform destroy
```

Helpful Terraform Links:
- [Terraform Language Documentation](https://www.terraform.io/docs/language/index.html)
- [Resource: azure_registry](https://registry.terraform.io/namespaces/Azure)

