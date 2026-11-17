# Lesson 3 — Kubernetes Ingress

## Objective
Configure an Ingress to route HTTP traffic to an Nginx application running on Minikube.

## Concepts learned
- Ingress defines HTTP/HTTPS routing rules.
- An Ingress Controller implements these rules.
- Ingress routes traffic to Kubernetes Services.
- Host-based routing allows multiple applications to share an entry point.

## Architecture
Client → Ingress Controller → Service → Pods

## Commands

```bash
minikube addons enable ingress
kubectl apply -f 03-ingress/nginx-ingress.yaml
kubectl get ingress
kubectl describe ingress nginx-ingress
kubectl port-forward -n ingress-nginx service/ingress-nginx-controller 8080:80
```

## Testing

```bash
curl -H "Host: nginx.local" http://127.0.0.1:8080/
```

## Expected result
The Nginx welcome page is returned through the Ingress Controller.

## Reference
https://kubernetes.io/docs/concepts/services-networking/ingress/
