# Lesson 8 — Kubernetes Resource Requests & Limits

## Objective
Understand Kubernetes resource allocation, scheduling, CPU throttling, and memory limits.

## Key Concepts

| Concept | Description |
|---|---|
| CPU Request | CPU capacity considered by the scheduler |
| CPU Limit | Maximum CPU quota enforced through throttling |
| Memory Request | Memory capacity considered by the scheduler |
| Memory Limit | Memory usage threshold that can trigger OOMKilled |
| Metrics Server | Provides CPU and memory usage metrics |

## Hands-on Experiments

### 1. Resource Monitoring
- Deployed Nginx with CPU and memory requests and limits.
- Enabled the Minikube Metrics Server addon.
- Monitored Pods using `kubectl top pods`.

### 2. CPU Throttling
- Created a CPU-intensive BusyBox container.
- Configured a CPU limit of `100m`.
- Observed CPU usage around `108m`.
- Confirmed throttling by observing an increasing `nr_throttled` counter.

### 3. Kubernetes Scheduling
- Inspected Node resource allocation.
- Created a Pod requesting more CPU than the Node could provide.
- Explored how insufficient resources affect scheduling.

## Useful Commands

```bash
kubectl top nodes
kubectl top pods
kubectl describe node minikube
kubectl describe pod <pod-name>
kubectl get pods
kubectl get events --sort-by=.lastTimestamp
```

## DevOps Takeaways

- Requests influence scheduling; limits constrain consumption.
- CPU throttling slows applications without necessarily restarting them.
- Exceeding memory limits can cause OOMKilled.
- Pods can remain Pending because of insufficient requested resources.
- Metrics Server provides resource metrics but is not a replacement for Prometheus.

