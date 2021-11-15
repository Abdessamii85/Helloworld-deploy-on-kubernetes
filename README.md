# Application Deployment on Kubernetes using Jenkins

## Technologies
Docker: application containerization
Kubernetes: for deployment, scaling, and management of containerized applications.
Jenkins: for automatic integrations and deployments(CI/CD).
Python: web application for Home task 
helm : package manager for kubernetes

## Project Scope

This repository describes steps to perform continous Rolling deployment on a kubernetes cluster using  Jenkins server.

this project deploy the [hello-world](https://github.com/Abdessamii85/hello-world.git) application and use images from dockerhub registry [here](https://hub.docker.com/r/abdessamii/user-py)

# resilence of the application

for more resilence of the application
- A [Horizontal Pod Autoscaler](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) was configured  to to ensure that Kubernetes scales the number of Pods when the cpu usage exceed  80%
- A [Pod Disruption Budget](https://kubernetes.io/docs/tasks/run-application/configure-pdb/) also added to allow higher availability in maintenace windows

# Test localy

the application can be tested loccaly with [Lightweight Kubernetes k3s](https://rancher.com/docs/k3s/latest/en/) for exemple 

Install K3S 

```bash
curl -sfL https://get.k3s.io | sh -
```
Acces the cluster 

```bash
export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
kubectl get pods --all-namespaces
helm ls --all-namespaces
```
Deploy hellowworld

```bash
helm upgrade --install helloworld ./helloworld
```
## Pipeline Prerequisites

The slave Jenkins needs to have the following software istalled :

- [helm](https://helm.sh/) : The package manager for Kubernetes
- [kubectl](https://kubernetes.io/fr/docs/tasks/tools/install-kubectl/) : kubectl CLI

In the Jenkins UI we need to add a secret file credential with the kubeconfig on it.

## Continuous deployment Pipeline

- this pipeline will deploy abdessamii/user-py using a helm chart 
- Integration test 
  ```bash
   kubectl rollout status --timeout=60s deployment helloworld
  ```
- send a email notification with the CD result





