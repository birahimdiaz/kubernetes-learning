# Lesson 7 — Kubernetes Health Checks

## Objective

Understand how Kubernetes monitors application health using **Liveness, Readiness, and Startup Probes**.

## 1. Key Concepts

| Probe | Purpose | Failure Behavior |
|---|---|---|
| Liveness | Checks whether the application is still healthy | Restarts the container after the failure threshold |
| Readiness | Checks whether the application can receive traffic | Removes the Pod from normal Service traffic |
| Startup | Checks whether the application has finished starting | Restarts the container after the failure threshold |

## 2. Hands-on Lab

We deployed Nginx with two replicas and configured three HTTP health checks.

```yaml
startupProbe:
  httpGet:
    path: /
    port: 80
  periodSeconds: 5
  failureThreshold: 12

readinessProbe:
  httpGet:
    path: /
    port: 80
  periodSeconds: 5
  failureThreshold: 3

livenessProbe:
  httpGet:
    path: /
    port: 80
  periodSeconds: 10
  failureThreshold: 3
```

## 3. Experiments

### Experiment 1 — Readiness Probe Failure

Changed the readiness path from `/` to `/not-found`.

**Observed:**
- The new Pod remained `Running` but showed `0/1 Ready`.
- The container did not restart.
- The two old healthy Pods remained available during the rolling update.

**Lesson:** Readiness controls whether a Pod can receive Service traffic.

### Experiment 2 — Liveness Probe Failure

Configured the liveness path as `/not-found` to simulate an unhealthy application.

**Expected behavior:** After repeated failures, Kubernetes restarts the container.

### Experiment 3 — Startup Probe Failure

Changed the startup path to `/not-found`.

**Observed:**

```text
READY   STATUS    RESTARTS
0/1     Running   1
```

The container restarted after the Startup Probe reached its failure threshold.

**Lesson:** Startup Probes protect slow-starting applications from premature liveness checks.

## 4. Rolling Updates

During our experiments, we observed three Pods even though the Deployment specified two replicas.

This happened because Kubernetes uses a RollingUpdate strategy with `maxSurge`.

The two healthy Pods remained available while the new Pod failed its health checks.

## 5. Useful Commands

```bash
kubectl apply -f nginx-health.yaml
kubectl get pods -l app=nginx-health
kubectl describe pod -l app=nginx-health
kubectl get events --sort-by=.lastTimestamp
kubectl rollout status deployment/nginx-health
kubectl logs deployment/nginx-health
```

## 6. DevOps Takeaways

- `Running` does not necessarily mean `Ready`.
- Readiness failures do not directly restart containers.
- Liveness failures can trigger container restarts.
- Startup Probes delay Liveness and Readiness checks until startup succeeds.
- Incorrect health checks can block Kubernetes rolling updates.
- Health checks are essential for application reliability in production.

## 7. Real-world Use Case

On AWS EKS, health checks help ensure that applications remain available during deployments, application failures, and recovery operations.

**Key principle:** Kubernetes needs reliable health signals to manage application availability effectively.
