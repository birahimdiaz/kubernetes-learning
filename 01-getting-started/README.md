# Lesson 1 - First Kubernetes Deployment

## Objective
Deploy Nginx using Kubernetes and Minikube.

## Concepts
- Deployment: manages the desired application state.
- ReplicaSet: maintains the desired number of Pods.
- Pod: runs one or more containers.
- Node: machine that hosts Pods.

## Commands
kubectl apply -f nginx-deployment.yaml
kubectl get deployments
kubectl get replicasets
kubectl get pods -o wide
kubectl port-forward deployment/nginx 8080:80
