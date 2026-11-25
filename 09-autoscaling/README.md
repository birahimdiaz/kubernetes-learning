# Lesson 9 — Horizontal Pod Autoscaler (HPA)

## Objective

Understand and implement automatic horizontal scaling in Kubernetes based on CPU utilization.

## Architecture

Load Generator → Service → Application Pods

Kubelet → Metrics Server → HPA Controller → Deployment → ReplicaSet → Pods

## Configuration

| Parameter | Value |
|---|---|
| Initial replicas | 2 |
| Minimum replicas | 2 |
| Maximum replicas | 10 |
| CPU request | 100m |
| CPU limit | 500m |
| Target CPU utilization | 50% |

## Hands-on Experiments

- Deployed a CPU-intensive application.
- Created a ClusterIP Service.
- Configured HPA using the autoscaling/v2 API.
- Generated continuous HTTP traffic using BusyBox.
- Observed automatic scaling from 2 to 10 replicas.
- Stopped the load generator to test automatic scale-down.

## HPA Calculation

CPU utilization = (Actual CPU usage / CPU request) × 100

Desired replicas = ceil(Current replicas × Current utilization / Target utilization)

## Troubleshooting

Initially, HPA displayed unknown CPU utilization and reported FailedGetResourceMetric errors.

Verified:

- Metrics Server availability.
- Metrics API availability.
- Application Pod readiness.
- CPU metrics using kubectl top pods.

Metrics subsequently became available, although the exact root cause of the initial failure was not confirmed.

## Useful Commands

```bash
kubectl get hpa
kubectl get hpa -w
kubectl describe hpa hpa-demo
kubectl top pods -l app=hpa-demo
kubectl get pods -l app=hpa-demo
kubectl delete pod load-generator
```

## Key Takeaways

- HPA scales the number of Pods, not Nodes.
- CPU utilization is calculated relative to CPU requests, not limits.
- HPA targets resource efficiency as well as application performance.
- Kubernetes Services distribute traffic among available Pods.
- Scale-down stabilization prevents unnecessary scaling fluctuations.
- HPA can work alongside Cluster Autoscaler or Karpenter.
- A Pending Pod does not necessarily indicate insufficient resources.
