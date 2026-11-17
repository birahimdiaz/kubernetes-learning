# Lesson 4 — Multi-Application Kubernetes Ingress

## Objective
Deploy two Nginx applications on Minikube and expose them through a single Ingress Controller using path-based routing.

## Architecture

```text
Client
  |
  v
Ingress Controller (demo.local)
  |
  +-- /app1 --> app1-service --> App 1 Pods (2)
  |
  +-- /app2 --> app2-service --> App 2 Pods (2)
```

## Kubernetes Resources

- **Deployments:** Manage two replicas of each application.
- **Services:** Provide internal ClusterIP endpoints for the applications.
- **Ingress:** Routes HTTP requests according to URL paths.
- **ConfigMaps:** Provide custom HTML content to each Nginx application.

## Commands

```bash
kubectl apply -f apps.yaml
kubectl apply -f services.yaml
kubectl apply -f ingress.yaml

kubectl get deployments
kubectl get pods
kubectl get svc
kubectl get ingress
```

## Testing

```bash
curl -H "Host: demo.local" http://127.0.0.1:8080/app1
curl -H "Host: demo.local" http://127.0.0.1:8080/app2
```

## Results

- `/app1` returns Application 1.
- `/app2` returns Application 2.
- Both applications are accessible through one Ingress Controller.

## Key Takeaways

- One Ingress can route requests to multiple Services.
- ClusterIP Services provide internal access to Pods.
- Path-based routing allows multiple applications to share one hostname.
- ConfigMaps can inject configuration into containers.

