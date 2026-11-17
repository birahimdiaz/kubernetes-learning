# Lesson 5 — Kubernetes ConfigMaps & Secrets

## Objective

Learn how to separate application configuration from container images using Kubernetes ConfigMaps and Secrets.

## Concepts learned

- **ConfigMap:** stores non-sensitive configuration.
- **Secret:** stores sensitive values such as passwords and tokens.
- **envFrom:** injects ConfigMap and Secret values as environment variables.
- **Rollout restart:** recreates Pods so they can receive updated environment variables.

## Commands

```bash
kubectl apply -f configmap.yaml
kubectl create secret generic app-secret --from-literal=DB_PASSWORD='demo-password-123'
kubectl apply -f deployment.yaml
kubectl get pods -l app=config-demo
kubectl logs deployment/config-demo
kubectl rollout restart deployment/config-demo
```

## Key takeaways

ConfigMaps and Secrets help separate configuration from application code.

Environment variables sourced from ConfigMaps or Secrets are loaded when a container starts. Updating these values does not automatically update the environment of an existing container.

Kubernetes Secrets require appropriate RBAC permissions and encryption-at-rest configuration for stronger protection.

## Security

Never commit real passwords, API tokens, or kubeconfig credentials to a public GitHub repository.
