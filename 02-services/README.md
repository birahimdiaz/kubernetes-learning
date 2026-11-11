# Lesson 2 — Kubernetes Services

## Objective
Expose an Nginx Deployment using a Kubernetes NodePort Service.

## Concepts learned
- A Service provides a stable network endpoint for Pods.
- A NodePort Service exposes an application through a port on Kubernetes Nodes.
- A Service selector identifies the Pods that receive traffic.
- EndpointSlices track the backend endpoints associated with a Service.

## Commands
```bash
kubectl apply -f 02-services/nginx-service.yaml
kubectl get services
kubectl get endpointslices -l kubernetes.io/service-name=nginx-service
minikube service nginx-service --url
```

## Architecture
Client → NodePort Service → Nginx Pods

## Expected result
The Nginx welcome page is accessible through the Service URL.
