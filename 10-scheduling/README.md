# Lesson 10 — Advanced Kubernetes Scheduling

## Objectives

Understand how Kubernetes controls Pod placement using labels, affinity rules, taints and tolerations.

## Concepts covered

- Node Selector: exact Node label matching.
- Node Affinity: flexible required and preferred scheduling rules.
- Taints and Tolerations: restricting access to dedicated Nodes.
- Pod Affinity: scheduling related workloads together.
- Pod Anti-Affinity: separating workloads for high availability.

## Practical experiments

- Scheduling Pods using Node labels.
- Comparing required and preferred affinity.
- Investigating untolerated taints.
- Scheduling Pods using matching tolerations.
- Testing strict Anti-Affinity on a single-node cluster.
- Troubleshooting a blocked rolling update caused by existing Pods' required Anti-Affinity rules.

## Key takeaways

- Required constraints can cause Pods to remain Pending.
- Preferred constraints influence scheduling without strictly blocking it.
- Tolerations permit scheduling but do not guarantee Node placement.
- IgnoredDuringExecution means affinity rules do not trigger eviction when conditions change after scheduling.
- Existing Pods' required Anti-Affinity rules can block new Pods.
- Combining scheduling mechanisms enables dedicated Node pools and workload separation.

## Production use cases

- Dedicated GPU Node pools.
- High availability.
- Workload isolation.
- Reducing inter-application network latency.
- Optimizing resource placement.

## Troubleshooting commands

- `kubectl get pods -o wide`
- `kubectl describe pod <pod-name>`
- `kubectl get nodes --show-labels`
- `kubectl describe node <node-name>`
- `kubectl get events`

## Environment

Minikube, Kubernetes, kubectl and Nginx.
